# deploy

The bots must be encapsulated inside a docker container and will be run with the command

```sh

halite -d "240 160" "docker run --rm -i hbot" "docker run --rm -i hbot-go"
```