# Instructions

## Installation

### Download or compile game binaries

You can download the game binary already compiled for your platform and the basic bot configuration for all the available languages in this [link](https://2017.halite.io/learn-programming-challenge/downloads-and-starter-kits/)

### Offline visualizer

The official visualizer is also available in the previous page, but you need to build it on your own and can be a little tricky. I've discover another visualizer called [chlorine](https://github.com/fohristiwhirl/chlorine) that allows you to see the game in a minimalists way but with much more useful information.

### Install docker

#### Linux

Most distributions already have docker in the package manager, so provably you can install docker with something like this command:

```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

> If you want detailed instructions, you can find it [here](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

Also is recommended to add your user to the docker group. Just to avoid typing sudo every time.

```sh
  sudo usermod -aG docker your-user
```

#### Windows

Instructions [here](https://docs.docker.com/docker-for-windows/install/)

> Docker for windows is problematic, I recommend to use a linux host whenever is possible.

## Local development

Basic usage requires only the path to the bot executable that you want to run. The following commands executes two instances of the same bot.

```sh
halite  "./cmd/MyBot/MyBot" "./cmd/MyBot/MyBot"
```

The halite binary offers help about the usage. just type  `halite --help`

### Visualization

The halite binary will generate files with the pattern `replay-*` that contain the information about the game in json.zstd format. The tool [Chlorine](#offline-visualizer) already provides a way to visualize the content. You can launch the application and drag-drop the replay file, or simply use the terminal command.

```sh
chlorine -o <path-to-file>
```

> You will be able to visualize the remote games that you [download](#finding-your-game-logs) from remote servers

## Remote

### Login

There is a shared account with privileges to access s3 bucket and RDS data. The credentials will be shared when requested.

> NOTE: right now there is no need to create multiple accounts, but take into account that your bot submission will be available for everyone to download. Also, you will be able to delete other submissions, so please, be careful and don't force us to create unique accounts :)

### Environment

When running in the server, the code will be executed inside a docker container. The equivalent command will be:

```sh
BOT=hbot
cat $BOT.tar.gz | gunzip | docker load 
halite (...) "docker run --rm -i $BOT:latest"
```

First, you need to build the directory giving a tag name to the image

```sh
docker build -t hbot:latest .
```

Now you can save/load the image as a .tar file with the save/load command

```sh
docker save hbot | gzip > hbot.tar
cat hbot.tar.gz | gunzip | docker load
```

> **it is important to keep the name of the tar the same as the name of the image. This is how the game manager will identify images.**

The good thing about this, is that the server can run any code without having all the dependencies installed.

### Submit a bot

The bot image must be uploaded to AmazonS3 bucket `s3://halite2/bots/` you can use the web interface or the [awscli]. I recommend to use the cli, as it is much faster and it is easy to integrate with test/build/deploy scripts.

```sh
# example submit a bot
aws s3 cp hbot.tar.gz s3://halite2/bots/
```

### Database

You will be able to run queries against the database using the web [editor](https://console.aws.amazon.com/rds/home?region=us-east-1#query-editor:) or the [awscli]

```sh
# example query players table from cli
aws rds-data execute-statement --secret-arn="arn:aws:secretsmanager:us-east-1:294919704567:secret:rds-db-credentials/cluster-37N3X5JRMMOX6HK32XKZO7Y6EQ/admin-7H38e9" --resource-arn="arn:aws:rds:us-east-1:294919704567:cluster:halitedb" --sql="select * from haliteTest.players;"
```

There are two main tables. The players table contains information about registered bots and the results table contains the results for each played game.

#### Finding your game logs

To check how your games are going you should check the results table filtering by your user.

```sql
SELECT *
FROM results
WHERE name='bot/hbot.tar.gz'
```

You can use the path provided in the columns logs and replay files to look for specific files in S3.

```sh
# example download replay file
aws s3 cp s3://halite2/replays/replay-xxxx-xxxx-xxxx.hlt ~/Downloads/
```

#### Check your ranking

Your ranking along with other metrics is stored in players table, you can find your data filtering by your bot name

```sql
SELECT *
FROM players
WHERE name='bot/hbot.tar.gz'
```

[awscli]: https://docs.aws.amazon.com/cli/latest/userguide/install-linux-al2017.html
