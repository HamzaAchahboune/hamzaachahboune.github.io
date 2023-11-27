---
title: "NTFY : Local Notification server"
date: 2023-11-27 00:00:00 +0000
categories: [Linux]
tags: [Install NTFY]    
author: Hamza Achahboune
layout: post
---

# NTFY : the local notification server 
# ![img-description](/assets/img/Blog/ntfy1.png)
## Introduction


`ntfy` is a simple yet powerful tool designed to bring convenience to your digital life. It's an HTTP-based pub-sub notification service that allows you to send notifications from any computer to your phone or desktop Locally. Whether you're a developer running long processes, a system administrator who needs to be alerted about system events, or just someone who wants to automate their digital life, `ntfy` can make things easier for you.

The use cases for `ntfy` are vast and varied. Here are a few examples:

1. **Cronjobs**: You can use `ntfy` to get notified when your cronjobs or long-running scripts are done. This can be particularly useful for backups, data processing tasks, or any other tasks that take a long time to complete.

2. **System Monitoring**: `ntfy` can be used to monitor your system and alert you about important events. For example, you can set up `ntfy` to send you a notification when your disk space is running low, when your CPU usage is high, or when a specific process starts or stops.

3. **Home Automation**: If you're into home automation, you can use `ntfy` to get notified about various events in your home. For example, you can set up `ntfy` to alert you when your laundry is done, when there's movement in your yard, or when your front door is opened.

4. **Development**: Developers can use `ntfy` to get notified about various events related to their projects. For example, you can set up `ntfy` to alert you when your code compilation is done, when a long-running test suite finishes, or when a deployment is completed.

## Installation

Before we start with the installation process, there are a few prerequisites you need to have:

### Prerequisites
1. **Docker**: Docker is a platform that allows you to automate the deployment, scaling, and management of applications in containers. You can download Docker from the [official Docker website]. Make sure to choose the right version for your operating system.

2. **A Server or a Computer**: You need a Linux server or a computer where you can install and run Docker. In my case i use kali linux.
use this following command to install Docker .
```bash
$ sudo apt install docker.io
```


### Step-by-step guide on how to install `ntfy` using Docker

Once you have the prerequisites ready, you can proceed with the installation of `ntfy`:

1. **Install and run the Docker image**:
# ![img-description](/assets/img/Blog/4.png)
 The first step is to run this command to install and run the contain of ntfy .
```bash
sudo docker run -p 80:80 binwiederhier/ntfy server
```

2. **Check if container is installed**:
# ![img-description](/assets/img/Blog/5.png)
to check if the container is installed and running successfuly use this following command :
```bash 
sudo docker ps
```  

then go to browser and tap the ip address of the container the ntfy application will display
# ![img-description](/assets/img/Blog/6.png)


## Usage

Once you have `ntfy` installed and configured, you can start using it to send and receive notifications. Here's how:

### How to Send Notifications Using `ntfy`

Sending notifications with `ntfy` is as simple as making a POST request. You can do this with a tool like `curl`. Here's an example:

to send notifications to the Ntfy server 
```bash
curl -d "Your message here" ntfy.sh/mytopic
```
to send notifications to the local Ntfy server 
```bash
curl -d "Your message here" ip-server/mytopic
```


### How to Receive Notifications on Your Phone

To receive notifications on your phone, you need install the application `ntfy` then subscribe to a topic.

### Examples of Scripts That Use `ntfy` to Send Notifications

Here are a simple example of how you can use `ntfy` in your scripts to send notifications:
The script starts by updating the system. It does this by running the `apt-get update`  and `apt-get upgrade` commands, Then u recieve a notification to your server and also your phone  

1. **Send a notification when a long-running process finishes**:

```bash
#!/bin/bash


sudo apt-get update -y && sudo apt-get upgrade -y


if [ $? -eq 0 ]; then

    curl -d "Update was successful" 192.168.66.180/Update_al   
    curl -d "Update was successful" ntfy.sh/Update_al
else

   curl -d "Update was faild" 192.168.66.180/Update_al      
   curl -d "Update was faild" ntfy.sh/Update_al 
fi
     
```

After Running the script i have recieve the notification on my phone and web application 
# ![img-description](/assets/img/Blog/7.png)

Sure, here's a sample conclusion for your blog post:

## Conclusion

In this tutorial, we've explored `ntfy`, a versatile tool for sending push notifications. We've covered everything from installation and configuration to practical examples of use. Whether you're integrating `ntfy` into your scripts, using it from the command line, or incorporating it into your web applications, you now have the knowledge to use `ntfy` effectively.




