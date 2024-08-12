---
title: "Windows Edition During Installation problem"
date: 2024-8-12 00:00:00 +0000
categories: [windows]
tags: [windows]    
author: Hamza Achahboune
layout: post
---

# Selecting Windows Edition During Installation with `ei.cfg`
![select-windows-11-pro-edition-during-clean-install](https://github.com/user-attachments/assets/df691fe3-1879-4d19-9be8-726e8583d925)

## Introduction

When installing Windows, you may want to choose a specific edition from multiple options available. If you are using a USB drive for installation and want to ensure that the edition selection screen appears, you can achieve this by creating a specific configuration file.

## Creating the `ei.cfg` File

To enable the edition selection screen during Windows installation, follow these steps:

### 1. Prepare Your Installation Media

Ensure you have a bootable USB drive with the Windows installation files.

### 2. Create the `ei.cfg` File

1. Open a text editor (such as Notepad).
2. Enter the following content into the editor:

    ```ini
    [EditionID]
    Professional
    [Channel]
    Retail
    ```

3. Save the file as `ei.cfg`.

### 3. Place the `ei.cfg` File in the Correct Location

1. Navigate to the `Sources` folder on your USB drive.
2. Copy the `ei.cfg` file you created and place it in the `Sources` folder.

![1](https://github.com/user-attachments/assets/aba1201f-0910-4894-8979-801a5746adf7)

![Capture d'écran 2024-08-12 141651](https://github.com/user-attachments/assets/0a6c19a0-ce35-4c2c-8daa-c93cc1401564)



### 4. Boot from the USB Drive

1. Restart your computer and boot from the USB drive.
2. Follow the installation prompts. You should now see the Windows edition selection screen.

## Conclusion

By creating and placing an `ei.cfg` file with the appropriate content, you can control the Windows edition selection during installation. This can be useful for various deployment scenarios or if you need to ensure a specific edition is chosen.

## Troubleshooting

- **File Not Recognized**: Ensure the file is named exactly `ei.cfg` and is placed in the `Sources` folder.
- **No Edition Selection**: Verify that the installation media is not customized in a way that prevents edition selection.

## References

- [Microsoft Documentation on Windows Installation](https://docs.microsoft.com/windows/deployment)
