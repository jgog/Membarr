[![Discord](https://img.shields.io/discord/997761163020488815?color=7289DA&label=Discord&style=for-the-badge&logo=discord)](https://discord.gg/7hAUKKTyTd)
[![DockerHub](https://img.shields.io/badge/Docker-Hub-%23099cec?style=for-the-badge&logo=docker)](https://hub.docker.com/r/yoruio/membarr)
![Docker Pulls](https://img.shields.io/docker/pulls/yoruio/membarr?color=099cec&style=for-the-badge)
[![docker-sync](https://github.com/Yoruio/Membarr/actions/workflows/docker-sync.yml/badge.svg)](https://github.com/Yoruio/Membarr/actions/workflows/docker-sync.yml)

Membarr 
=================

Membarr is a fork of Invitarr that invites discord users to Plex and Jellyfin. You can also automate this bot to invite discord users to a media server once a certain role is given to a user or the user can also be added manually.  

### Features

- Ability to invite users to Plex and Jellyfin from discord 
- Fully automatic invites using roles 
- Ability to kick users from plex if they leave the discord server or if their role is taken away.
- Ability to view the database in discord and to edit it.

Commands: 

```
/plex invite <email>
This command is used to add an email to plex
/plex remove <email>
This command is used to remove an email from plex
/jellyfin invite <jellyfin username>
This command is used to add a user to Jellyfin.
/jellyfin remove <jellyfin username>
This command is used to remove a user from Jellyfin.
/membarr dbls
This command is used to list Membarr's database
/membarr dbadd <@user> <optional: plex email> <optional: jellyfin username>
This command is used to add exsisting  plex emails, jellyfin users and discord id to the DB.
/membarr dbrm <position>
This command is used to remove a record from the Db. Use /membarr dbls to determine record position. ex: /membarr dbrm 1
```

# Unraid Installation
> For Manual an Docker setup, see below

1. Ensure you have the Community Applications plugin installed.
2. Inside the Community Applications app store, search for Invitarr.
3. Click the Install Button.
4. On the following Add Container screen, Change repository to yoruio/invitarr:latest
5. Add discord bot token.
6. Click apply
7. Finish setting up using [Setup Commands](#after-bot-has-started)

# Manual Setup (For Docker, see below)

**1. Enter discord bot token in bot.env**

**2. Install requirements**

```
pip3 install -r requirements.txt 
```
**3. Start the bot**
```
python3 Run.py
```

# Docker Setup & Start

1. First pull the image 
```
docker pull yoruio/invitarr:latest
```
2. Make the container 
```
docker run -d --restart unless-stopped --name invitarr -v /path to config:/app/app/config -e "token=YOUR_DISCORD_TOKEN_HERE" yoruio/invitarr:latest
```

# After bot has started 

# Plex Setup Commands: 

```
/plexsettings setup <username> <password> <server name>
This command is used to setup plex login. 
/plexsettings addrole <@role>
These role(s) will be used as the role(s) to automatically invite user to plex
/plexsettings removerole <@role>
This command is used to remove a role that is being used to automatically invite uses to plex
/plexsettings setuplibs <libraries>
This command is used to setup plex libraries. Default is set to all. Libraries is a comma separated list.
/plexsettings enable
This command enables the Plex integration (currently only enables auto-add / auto-remove)
/plexsettings disable
This command disables the Plex integration (currently only disables auto-add / auto-remove)
```

# Jellyfin Setup Commands:
```
/jellyfinsettings setup <server url> <api key>
This command is used to setup the Jellyfin server 
/jellyfinsettings addrole <@role>
These role(s) will be used as the role(s) to automatically invite user to Jellyfin
/jellyfinsettings removerole <@role>
This command is used to remove a role that is being used to automatically invite uses to Jellyfin
/jellyfinsettings setuplibs <libraries>
This command is used to setup Jellyfin libraries. Default is set to all. Libraries is a comma separated list.
/jellyfinsettings enable
This command enables the Jellyfin integration (currently only enables auto-add / auto-remove)
/jellyfinsettings disable
This command disables the Jellyfin integration (currently only disables auto-add / auto-remove)
```

# Migration from Invitarr
Membarr uses a slightly different database table than Invitarr. Membarr will automatically update the Invitarr db table to the current Membarr table format, but the new table will no longer be compatible with Invitarr, so backup your app.db before running Membarr!

# Migration to Invitarr
As mentioned in [Migration from Invitarr](#Migration-From-Invitarr), Membarr has a slightly different db table than Invitarr. To Switch back to Invitarr, you will have to manually change the table format back. Open app.db in a sqlite cli tool or browser like DB Browser, then remove the "jellyfin_username" column, and make the "email" column non-nullable.

# Other stuff
**Enable Intents else bot will not Dm users after they get the role.**
https://discordpy.readthedocs.io/en/latest/intents.html#privileged-intents
**Discord Bot requires Bot and application.commands permission to fully function.**

