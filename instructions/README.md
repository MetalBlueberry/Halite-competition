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

## Simulation

### Local

Basic usage requires only the path to the bot executable that you want to run. The following commands executes two instances of the same bot.

```sh
halite  "./cmd/MyBot/MyBot" "./cmd/MyBot/MyBot"
```

The halite binary offers help about the usage.

```sh
~/Documents/Projects/Halite-competition$ halite --help

USAGE: 

   halite  [--log] [--no-compression] [--print-constants] [--constantsfile
           <path to file>] [-i <path to directory>] [-s <positive integer>]
           [-d <a string containing two space-seprated positive integers>]
           [-n <{1,2,3,4,5,6}>] [-r] [-t] [-o] [-q] [--] [--version] [-h]
           <Array of strings> ...


Where: 

   --log
     Always produce game logs, instead of only in case of errors

   --no-compression
     Disables compression for output files.

   --print-constants
     Print out the default constants and exit.

   --constantsfile <path to file>
     JSON file containing runtime constants to use.

   -i <path to directory>,  --replaydirectory <path to directory>
     The path to directory for replay output.

   -s <positive integer>,  --seed <positive integer>
     The seed for the map generator.

   -d <a string containing two space-seprated positive integers>, 
      --dimensions <a string containing two space-seprated positive
      integers>
     The dimensions of the map.

   -n <{1,2,3,4,5,6}>,  --nplayers <{1,2,3,4,5,6}>
     Create a map that will accommodate n players [SINGLE PLAYER MODE
     ONLY].

   -r,  --noreplay
     Turns off the replay generation.

   -t,  --timeout
     Causes game environment to ignore timeouts (give all bots infinite
     time).

   -o,  --override
     Overrides player-sent names using cmd args [SERVER ONLY].

   -q,  --quiet
     Runs game in quiet mode, producing machine-parsable output.

   --,  --ignore_rest
     Ignores the rest of the labeled arguments following this flag.

   --version
     Displays version information and exits.

   -h,  --help
     Displays usage information and exits.

   <Array of strings>  (accepted multiple times)
     Start commands for bots.


   Halite Game Environment
```

### Remote

When running in the server, the code will be executed inside a docker container. The equivalent command will be:

```sh
halite -d "240 160" "docker run --rm -i hbot" "docker run --rm -i hbot"
```

The good thing about this, is that the server can run any code without having all the dependencies installed.

## Visualization

The halite binary will generate files with the pattern `replay-*` that contain the information about the game in json.zstd format. The tool [Chlorine](#offline-visualizer) already provides a way to visualize the content. You can launch the application and drag-drop the replay file, or simply use the terminal command.

```sh
chlorine -o <path-to-file>
```
