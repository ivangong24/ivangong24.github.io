---
title: How to build a lite home server on Raspberry Pi
author: ivan
date: 2024-01-30 20:00:00 +0800
categories: [blog]
tags: [homelab]
---

## Prerequisites
  - A Raspberry Pi (I have a Raspberry Pi 4 Model B with 8GB of RAM as a birthday gift from my friend [Yuyuan](https://lin.foo/))
  - A microSD card (8G at least)/SSD drive (if compatible with nvme expansion board/case, recommended if you want to turn your Raspberry Pi into a NAS)
  - An ethernet cable connect your Raspberry Pi to your router/switch (recommended)


## OS Installation

1. Download the latest Raspberry Pi imager from the [official website](https://www.raspberrypi.com/software/).

2. Insert the microSD card/SSD drive(use an enclosure/case if applicable) into your computer and open the Raspberry Pi imager.

3. Select the OS you want to install on your Raspberry Pi. For a home server, I recommend using Raspberry Pi OS Lite (64-bit). Before flashing the OS, make sure to select the correct Raspberry Pi model and storage device. 

4. Before we click the write button, we need to enable SSH for remote control. To do this, you can press `Ctrl/Command + Shift + X` to open the advanced options menu. In the "GENERAL" tab, please set your hostname (optional but recommended, e.g., myraspberrypi), username and password. In the "SERVICES" tab, please enable the toggle for SSH. After that, click the "Save" button to apply the changes.

5. Click the "Write" button to flash the OS to the microSD card/SSD drive.

6. Once the flashing process is complete, insert the microSD card/SSD drive into your Raspberry Pi and power it on.

## Initial setup

1. Check the IP address of your Raspberry Pi. You can use your router's web interface (usually it's 192.168.x.1) or an IP scanner tool to find the IP address of your Raspberry Pi.

2. Open a terminal on your computer and SSH into your Raspberry Pi using the following command: 
```console
$ ssh yourusername@<your_raspberry_pi_ip_address>
```
if you have set a hostname, you can use:
```console
$ ssh yourusername@<your_raspberry_pi_hostname>.local
```
The default port for SSH is 22. If you have changed the port, you can specify it using the `-p` flag. 
For example, if you changed the port to 2222, you can use:
```console
$ ssh -p 2222 yourusername@<your_raspberry_pi_ip_address>
```

3. Enter the password you set during the OS installation process and you should be logged into your Raspberry Pi!

## Create a user-friendly interface

If you are not comfortable with the command line interface, you can install a web-based control panel which makes it easier to manage your Raspberry Pi. There are a lot of options available (e.g., [OpenMediaVault](https://www.openmediavault.org/), [CasaOS](https://casaos.io/), etc.). I will be using CasaOS for this guide.

1. Run the following code for updating the system and installing the required packages:
```console
$ sudo apt update && sudo apt upgrade -y
```

2. Install CasaOS using the following command:
```console
$ curl -fsSL https://get.casaos.io | sudo bash
```

3. After the installation is complete, you can access the CasaOS web interface by entering the IP address (or hostname.local) of your Raspberry Pi in a web browser. You will be prompted to create an account and set up your home server!

## Deploy web services
Once you logged into CasaOS, you can deploy web services like Nextcloud, Home Assistant, etc. to your Raspberry Pi. CasaOS provides a user-friendly interface (App store) for managing these services and makes it easy to install and configure them. They are actually running in Docker containers, so you can also manage them via the command line if you prefer.


## File sharing
If you installed an SSD drive with a relatively large storage, you can also enable file sharing on your Raspberry Pi since CasaOS has Samba installed by default. To do this, you can click "Files" in the CasaOS web interface, right click to create a new folder, then click the three dots on the right upper corner of the folder and select "Share". After that, you can access the shared folder from your computer by clicking `win + R` and entering `\\<your_raspberry_pi_ip_address>(or <your_raspberry_pi_hostname>.local)` if you are using Windows. If you are using MacOS, you can click `Cmd + K` and enter  `smb://<your_raspberry_pi_ip_address>` or `smb://<your_raspberry_pi_hostname>.local`.

## Conclusion
Congratulations! You have successfully set up a lite home server on your Raspberry Pi. You can now access your server remotely, deploy web services, and share files with other devices on your network. Feel free to explore more features and services to enhance your home server experience!