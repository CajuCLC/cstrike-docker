# Counter-Strike 1.6 Server Docker Image with Bots
![Docker Cloud Automated build](https://img.shields.io/docker/cloud/automated/cajuclc/cstrike-docker) ![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/cajuclc/cstrike-docker) ![Docker Image Size (tag)](https://img.shields.io/docker/image-size/cajuclc/cstrike-docker/latest) ![Docker Pulls](https://img.shields.io/docker/pulls/cajuclc/cstrike-docker)

This image is based on [SteamCMD Docker](https://developer.valvesoftware.com/wiki/SteamCMD#Docker). It also includes Metamod, AMX Mod, DProto and Podbot.

### What is Metamod?
* Metamod is a plugin/DLL manager that sits between the Half-Life Engine and an HL Game mod, allowing the dynamic loading/unloading of mod-like DLL plugins to add functionality to the HL server or game mod.

### What is AMX Mod?
* AMX Mod X is a Metamod plugin for Half-Life 1. It provides comprehensive scripting for the game engine and its mods. Scripts can intercept network messages, log events, commands, client commands, set cvars, modify entities, and more.

### WHat is DProto?
* It allows your server to accept non-Steam clients (clients with a cracked CS), if you don't have dproto installed on your server you can't enter on it without a legit Steam client/account. Dproto makes that possible!
### What is Probot?
* PODBot MetaMod is an open source (GPL) metamod plugin that adds computer players (bots) to a popular game called Counter-Strike.

# Quick Start
The fastest way to run the Counter-Strike 1.6 Server is via `docker run`.
* Pull the image:
```
docker pull cajuclc/cstrike-docker
```
* Run the image:
```
docker run --name cstrike -p 27015:27015/udp -p 27015:27015 cajuclc/cstrike-docker
```
* You can also run the server via `docker-compose`. You can find an example below.

# Custom Config Files
You can use your own `server.cfg`, `dproto.cfg`, `plugins.ini` and `mapcycle.txt` by mounting them to the container. Any custom config file **WILL** override the settings from your environment variables.
```
-v /path/to/your/server.cfg:/home/steam/cstrike/cstrike/server.cfg
```

The complete `docker run` command is:
```
docker run --name cstrike -p 27015:27015/udp -p 27015:27015 -v /path/to/your/server.cfg:/home/steam/cstrike/cstrike/server.cfg cajuclc/cstrike-docker
```

# Docker Compose
You can start the server by running:
```
docker-compose up -d
```
# Run on TrueNAS Scale
I wrote an article how to run this image on TrueNAS Scale. You can find the article [here](https://www.cloudtutorial.net/run-counter-strike-1-6-server-on-truenas-scale/).
# SteamCMD
SteamCMD is responsible to install Counter-Strike and/or other games.
There is a current bug that prevents the installation of Counter-Strike 1.6 in a single command. You can read more [here](https://developer.valvesoftware.com/wiki/SteamCMD#Downloading_an_app).

### Steam Application IDs
You can find the list of IDs [here](https://developer.valvesoftware.com/wiki/Steam_Application_IDs).
* 10 - Counter-Strike
* 70 - Half-Life
* 90 - Counter-Strike 1.6 Dedicated Server

# Source
The code to install the mods and bots were utilized from other repositories. Please give them some love and support.
* [counter-strike-docker](https://github.com/jimtouz/counter-strike-docker), created by [Dimitris Touzloudis](https://github.com/jimtouz).
* [cs16-server](https://github.com/b4k3r/cs16-server), created by [Marcin Prokop](https://github.com/b4k3r).
* [counter-strike_server](https://github.com/b4k3r/counter-strike_server), created by [febLey](https://github.com/febLey).

# WHY?
My friends and I decided to have a LAN Party (remember those?) at my house and we will be playing some classic games.\
Instead of running these games directly on my PC, I decided to run on my TrueNAS server. TrueNAS allows you to run containers, so I decided to create this docker image.
