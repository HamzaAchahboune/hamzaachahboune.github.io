---
title: "Install Openstack Devstack"
date: 2023-11-04 00:00:00 +0000
categories: [OpenStack]
tags: [Install Open Stack]    
author: Hamza Achahboune
layout: post
---
# How to Install OpenStack on Ubuntu 22.04 TLS gwith DevStack


![img-description](/assets/img/Blog/1.jpg){: .shadow }



## What is OpenStack?
OpenStack is a free, open standard cloud computing platform. It is mostly deployed as infrastructure-as-a-service in public and private clouds where virtual servers and other resources are available to users.

## What is DevStack?
DevStack is a series of scripts used to quickly bring up a complete OpenStack environment. We can download the latest version of OpenStack from the git master branch. It is used to set up a faster and quicker way to set up the development environment and serves as the basis for most of the OpenStack project functional testing.

## Minimum Requirements
Before we begin, ensure you have the following minimum prerequisites:

- A fresh Ubuntu 22.04 installation
- User with sudo privileges
- 8 GB RAM
- 2 vCPUs
- Hard disk capacity of 10 GB
- Internet connection

With the minimum requirements satisfied, we can now proceed.

## Step 1: Update and Upgrade the System

To start off, log into your Ubuntu 22.04 system using SSH protocol and update and upgrade system repositories using the following command:

```bash
apt update -y && apt upgrade -y
```
Next reboot the system using the command.

```bash
sudo reboot
```

## Step 2: Create Stack User and Assign Sudo Privileges

Best practice demands that DevStack should be run as a regular user with sudo privileges. With that in mind, we are going to add a new user called "stack" and assign sudo privileges.

To create the `stack` user, execute the following commands:

```bash
sudo adduser -s /bin/bash -d /opt/stack -m stack
sudo chmod +x /opt/stack
```

Assign sudo privileges to the user:

```bash
echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack
```

## Step 3: Install Git and Download DevStack

Once you have successfully created the user 'stack' and assigned sudo privileges, switch to the user using the command:

```bash
su - stack
```
In most Ubuntu 22.04 systems, Git comes already installed. If by any chance Git is missing, install it by running the following command:

```bash
sudo apt install git -y
```

## Step 4: Create DevStack Configuration File

In this step, navigate to the DevStack directory:

```bash
cd devstack
```
copy the `local.conf` file to the `devstack` folder

```bash
cp sample/local.conf .
```

Then create a local.conf configuration file:

```bash
vim local.conf
```
Paste the following content into the local.conf file:

```bash
[[local|localrc]]
# Password for KeyStone, Database, RabbitMQ, and Service
ADMIN_PASSWORD=StrongAdminSecret
DATABASE_PASSWORD=$ADMIN_PASSWORD
RABBIT_PASSWORD=$ADMIN_PASSWORD
SERVICE_PASSWORD=$ADMIN_PASSWORD
# Host IP - get your Server/VM IP address from the 'ip addr' command
HOST_IP=192.168.66.178
```
Save and exit the text editor.

## Step 5: Install OpenStack with DevStack

To commence the installation of OpenStack on Ubuntu 22.04, run the script below contained in the DevStack directory:
```bash
cd devstack/
```
and 

```bash
./stack.sh
```
The following features will be installed:

* Horizon — OpenStack Dashboard
* Nova — Compute Service
* Glance — Image Service
* Neutron — Network Service
* Keystone — Identity Service
* Cinder — Block Storage Service
* Placement — Placement API

## Step 6: Accessing OpenStack on a web browser
To access OpenStack via a web browser browse your Ubuntu’s IP address as shown. `https://server-ip/dashboard` This directs you to a login page as shown.
![Local Image](/assets/img/Blog/2.png)

