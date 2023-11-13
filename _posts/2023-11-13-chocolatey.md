---
title: "Chocolatey Package Manager"
date: 2023-11-13 00:00:00 +0000
categories: [Windows]
tags: [Install Chocolatey]    
author: Hamza Achahboune
layout: post
---

# Chocolatey: A guide to windows package management
![Alt text](image.png)
## Introduction

Chocolatey is a package manager for Windows that automates the process of installing, updating, and managing software. It simplifies the software management process by providing a command-line interface to handle package installations and updates. In this tutorial, we'll cover the basics of Chocolatey.

Package managers allow you to:

* Download and install software without having to go to different web pages.
* Verify packages have not been tampered with so that you don’t end up with malware from MITM attacks.
* Install multiple packages for you and even make sure to install other software that an app may require.
* Upgrade and remove packages
Search for packages.
* And much more.

## Installation

To get started with Chocolatey, you first need to install it. 
Open apowershell with administrative privileges and run the following command:

**Set it to require all scripts to be signed**

```powershell
Get-ExecutionPolicy
Set-ExecutionPolicy AllSigned
```
**Install Chocolatey**

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

```

**check the chocolatey version**

```powershell
choco --version
```

## Chocolatey tutorial

**Installing Packages:**

```powershell
choco install packageName
```

**Installing Multiple Packages:**

```powershell
choco install packageName1 packageName2
```

**Updating Packages:**
```powershell
choco update packageName
```

**Updating all Packages:**
```powershell
choco upgrade all
```

**pdating Packages:**
```powershell
choco uninstall packageName
```

**Searching for Packages:**
```powershell
choco search searchQuery
```
**Viewing Installed Packages:**
```powershell

choco list 
```
**Viewing Chocolatey Version:**
```powershell
choco --version
```

## Install Chocolatey GUI
![img-description](/assets/img/Blog/1.jpg)
```powershell
choco install ChocolateyGUI
```