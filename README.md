A docker image for running a dedicated server for the game [CS:GO](https://blog.counter-strike.net/). Configured to use the [Get5](https://github.com/splewis/get5/) plugin alongside [Metamod:Source](https://www.sourcemm.net/) and [Sourcemod](https://www.sourcemod.net/) to host a quick setup scrim server.

# How to use this image
## Simple usage (recommended)

Clone this repository locally:<br/>
```console
$ git clone https://github.com/FragSoc/csgo-server-scrim.git
```

Create a new directory for the game installation:
```console
$ mkdir -p $(pwd)/csgo-data
$ chmod 777 $(pwd)/csgo-data # Makes sure the directory is writeable by the unprivileged container user
```

**Make necessary edits to both the docker-compose.yml and custom_server_template.cfg.**
**Look at configuration section below for guidance.**

Run docker-compose up:<br/>
```console
$ docker-compose up
```

**The container will automatically update the game on startup, so if there is a game update just restart the container.**

# Configuration
##Custom server settings
Before you run the initial startup, you will need to edit the custom_server_template.cfg file within the same dirtectory. This will be used to overwrite the /cfg/server.cfg file each time the server starts.
Should you wish to make any edits once the server has been created, you can do so using the below command and the server will use them once restarted:
```console
$ docker exec -it *CONTAINER_NAME* nano /home/steam/custom_server_template.cfg
```

## Environment Variables
You can overwrite these values within the docker-compose file, below are the defaults: 
```dockerfile
SRCDS_PORT=27015 
SRCDS_TV_PORT=27020 
SRCDS_CLIENT_PORT=27005 
SRCDS_TOKEN=0 
METAMOD_VERSION=1.10 
SOURCEMOD_VERSION=1.10
```
**If you edit the ports you will need to adjust these within the docker-compose file also.**
## Additional config (to-do)
The image also contains a copy of the official ESL config files from [here](https://play.eslgaming.com/download/26251762/). You will need to disable the Get5 plugin however (to-do)

If you want to learn more about configuring a CS:GO server check this [documentation](https://developer.valvesoftware.com/wiki/Counter-Strike:_Global_Offensive_Dedicated_Servers#Advanced_Configuration).