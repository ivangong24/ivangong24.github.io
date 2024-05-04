---
title: Build a home media center with Docker on Raspberry Pi
author: ivan
date: 2024-05-03 20:00:00 +0800
categories: [blog]
tags: [homelab]
---
  
### Introduction

In this article, I will show you how to build a home media center with Docker. We will use the following Docker containers:

  - [Sonarr](https://docs.linuxserver.io/images/docker-sonarr/)
  - [Radarr](https://docs.linuxserver.io/images/docker-radarr/)
  - [Overseer](https://docs.linuxserver.io/images/docker-overseerr/)
  - [Prowlarr](https://docs.linuxserver.io/images/docker-prowlarr/)
  - [Jackett](https://docs.linuxserver.io/images/docker-jackett/)
  - [Plex](https://docs.linuxserver.io/images/docker-plex/) (alternatives,  [Jellyfin](https://docs.linuxserver.io/images/docker-jellyfin/) , [Emby](https://docs.linuxserver.io/images/docker-emby/))
  - [Transmission](https://docs.linuxserver.io/images/docker-transmission/) (alternatives, [Deluge](https://docs.linuxserver.io/images/docker-deluge/), [qBittorrent](https://docs.linuxserver.io/images/docker-qbittorrent/))
  - [Tautulli](https://docs.linuxserver.io/images/docker-tautulli/)
  
### Step 1: Install Docker

First, you need to make sure Docker is installed on your Raspberry Pi. You can check it by running the following command:
```console
$ docker --version
```
If Docker is not installed, you can install it by the following command:
```console
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli docker-compose-plugin
```
If you have installed CasaOS following the [last post](https://ivangong24.github.io/posts/raspberrypi-homeserver/), we can skip this step.

### Step 2: Deploy Docker containers

#### Method 1: Using the App Store (Recommended)
Now, let's deploy the Docker containers. On a Raspberry Pi running CasaOS, you can use the "App Store" to deploy all the containers that we are going to use. Just search for the container name and click "Install".

#### Method 2: Using Command line
If you prefer to use commands to deploy the containers, I highly recommend using docker compose files given its simplicity and reproducibility. In the App Store, you can click the `Custom Install` on the top right corner, and click `Import` to paste the docker compose file that you want to use.

Here is an example of a `docker-compose.yml` file that you can use to deploy [Sonarr](https://docs.linuxserver.io/images/docker-sonarr/#media-folders):

```yaml

---
services:
  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - /path/to/data:/config
      - /path/to/tvseries:/tv #optional
      - /path/to/downloadclient-downloads:/downloads #optional
    ports:
      - 8989:8989
    restart: unless-stopped
```

You can modify the `volumes` section to match your setup. For example, you can click `Files` and navigate to the `AppData`. Then create a folder of the container name (e.g., `sonarr`) and create two other subfolders with it (`config` and `tvseries`). You can then copy the path of the `config` and `tvseries` folders and paste them into the `volumes` section of the `docker-compose.yml` file. After that, you can click `Submit` to start the container.

Alternatively, you can also use "docker-CLI" to deploy the containers. Here is an example of how to deploy the Sonarr container using the command line:

```console
$ docker run -d \
  --name=sonarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -p 8989:8989 \
  -v /path/to/data:/config \
  -v /path/to/tvseries:/tv \
  -v /path/to/downloadclient-downloads:/downloads \
  --restart unless-stopped \
  lscr.io/linuxserver/sonarr:latest
```

For the rest of the containers, you can follow the same steps as above.

### Step 3: Setup the containers

After deploying the containers, you can access the web interface of each container by entering the IP address of your Raspberry Pi followed by the port number of the container. For example, to access Sonarr, you can enter `http://<your_raspberry_pi_ip_address>:8989` in your web browser.

You will need to go through the initial setup process for each container. This usually involves setting up the download client, media folders, and other settings.

Take Sonarr as an example, you first need to add an indexer (e.g., Jackett/Prowlarr) and a download client (e.g., Transmission). You can do this by going to `Settings` -> `Indexers` -> `Add Indexer` and `Settings` -> `Download Clients` -> `Add Client`.

Once you have added the indexer and download client, you can add a new series by clicking `Series` -> `Add Series` -> `Add New Series`. You can search for the series you want to add and click `Add`. After that, you can configure the quality, language, and other settings for the series. It's recommended to set the quality to `1080p` or `720p` given the limited storage and CPU performance of Raspberry Pi. But if you are using other devices such as a NAS with more storage and stronger processors, you can set it to `4K`.

### Step 4: Enjoy your home media center

Congratulations! You have successfully set up a home media center with Docker on your Raspberry Pi. You can now add more containers to expand the functionality of your media center. Enjoy your favorite movies and TV shows!

### Conclusion

In this article, I have shown you how to build a home media center with Docker on a Raspberry Pi. By using Docker containers, you can easily deploy and manage various services such as Plex, Sonarr, Radarr, and more. This setup allows you to create a powerful media center that can stream your favorite content to any device in your home. If you have any questions or run into any issues, feel free to leave a comment below. Happy streaming!










  