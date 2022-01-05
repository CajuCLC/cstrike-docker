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

# Podbot Menu
If you want to be able to use the Podbot admin menu, you need to configure your Counter-Strike client (the one you play the game) with password. First make sure you add the file `podbot/podbot.cfg` as a mount to your container. This is the folder in the container:
```
/home/steam/cstrike/cstrike/addons/podbot/podbot.cfg
```
Search for `pb_passwordkey`, that's the name we will need. In my case: `pb_passwordkey "_pbadminpw"`.\
Now I need the password, it's the next configuration. Here is mine: `pb_password "your_password"` (make sure you change your password).\
We have to configure the password on the client (game) now. Open `cstrike` folder inside Steam installation. In my case I use a separate disk for all my games and this is where Counter-Strike is installed:
```
E:\Games\Steam\steamapps\common\Half-Life\cstrike
```

I manually created a file called `autoexec.cfg`. If you already this file, you just need to edit. Add the line:
```
setinfo _pbadminpw "your_password"
```
Again, make sure you use some safe password. Now open the game and create a bind:
```
bind "=" "pb menu"
```
This way every time you press `=` it will open the Podbot menu and you can add, remove, kill bots and much more.
# AMX Mod Menu
If you need to have access to AMX Mod Menu. Then mount file `users.ini` to this location:
```
/home/steam/cstrike/cstrike/addons/amxmodx/configs/users.ini
```
Here is an example of the file: https://github.com/alliedmodders/amxmodx/blob/master/configs/users.ini
You need to add your `user/IP/steam_id` to the list. Then inside the `autoexec.cfg` file we just created/edited you can add:
```
setinfo _pw "mypassword"
```
We get the `_pw` configuration from `amx_password_field "_pw"`, which comes from this file: https://github.com/alliedmodders/amxmodx/blob/master/configs/amxx.cfg#L14
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
