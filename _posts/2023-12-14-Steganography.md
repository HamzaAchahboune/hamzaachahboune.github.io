---
title: "Steganography"
date: 2023-12-14 00:00:00 +0000
categories: [Cybersecurity]
tags: [Steganography]    
author: Hamza Achahboune
layout: post
---

# Steganography - What is, Techniques, & Examples


## What is Steganography :
Steganography is a technique of hiding secret information within an ordinary, non-secret file or message, so that it will not be detected. The sensitive information will then be extracted from the ordinary file or message at its destination, thus avoiding detection. Steganography is an additional step that can be used in conjunction with encryption in order to conceal or protect data. Steganography is a means of concealing secret information within (or even on top of) an otherwise mundane, non-secret document or other media to avoid detection. It comes from the Greek words steganos, which means “covered” or hidden, and graph, which means to write. Hence, hidden writing.

## Who uses Steganography :
Steganography is typically used by hackers who want to embed malicious code. They do so by altering an ordinary bit of a file and inserting malicious code in it. Once a user unintentionally downloads the code by opening a file or image, the malware is activated and the hacker gains control of the user’s network or the malware corrupts the content. The steganographic file is so subtly different from the original that it cannot be immediately detected.


## what is LSB :Least significant bit :
is the last digit in a binary number. It's the one on the right side.

**Examples:**
1. In the binary number `1010`, the **LSB** is `0` because it's the rightmost digit.
2. For the binary number `1101`, the **LSB** is `1` as it's the rightmost bit.
3. If we have `0010`, the **LSB** is `0` since it's the last digit in the binary representation.

## How does Steganography work :

For instance, each pixel of an image file is made up of three bytes of data that correspond to the colors red, green, and blue; some image formats allocate an additional fourth byte to transparency or alpha. 
What LSB Steganography does is change the last bit of each of those bytes to hide one bit of data. So, in order to conceal 1 MB of data, an 8 MB image file is required.
Modifying the last bit of pixel value does not visually change the picture as the viewer will not be able to tell the difference. In the same way, data can be hidden in different parts of audio files and videos without changing the audible or visual output.

**Original Pixel Values:**
- Suppose we have an image pixel represented in RGB with values (147, 106, 204) ==> (10010011, 01101010, 11001100).

**Binary Payload to Hide:**
- Let's say we want to hide the binary message "010" in the LSBs of each color channel.

**Modified Pixel Values (Hiding the Data):**
- Change the last digit of each binary number to hide the message:
  - Red:   10010011 (original) -> 10010010 (modified)
  - Green: 01101010 (original) -> 01101011 (modified)
  - Blue:  11001100 (original) -> 11001101 (modified)

So, the modified pixel values become (10010010, 01101011, 11001101).

This means we have hidden the binary message "010" in the LSBs of the original pixel values.

This is a simplified example, and in real-world applications, larger messages are distributed across multiple pixels to hide information more effectively. Keep in mind that the changes made are subtle and generally not noticeable by the human eye.

## Types of Steganography :


1. **Image Steganography:**
   - Concealing information within images. Techniques include modifying pixel values, hiding data in color channels, or embedding information in the frequency domain.

2. **Audio Steganography:**
   - Hiding data within audio files. This can involve manipulating the amplitude, frequency, or phase of the audio signal to embed hidden information.

3. **Video Steganography:**
   - Concealing data within video files. Similar to image steganography, but applied to video frames. Techniques may include modifying pixel values or encoding data in the video stream.

4. **Text Steganography:**
   - Embedding information within text documents. This can be done by altering the spacing, font styles, or word choices to convey a hidden message.

5. **File Steganography:**
   - Hiding data within other types of files. This can include embedding information in the binary structure of various file formats.

6. **Network Steganography:**
   - Concealing data within network protocols or communication. Techniques may involve manipulating packet headers, timing, or other network properties.

7. **Printed Steganography:**
   - Hiding information in printed documents. This can involve using nearly invisible ink, microdots, or altering the shapes of printed characters.

8. **Digital Watermarking:**
   - Embedding information in digital media to prove ownership or authenticity. Watermarks are often visible but can also be hidden to serve as a form of steganography.

9. **Spatial Domain Techniques:**
   - Manipulating the spatial characteristics of an image, such as altering pixel values or modifying the arrangement of image elements.

10. **Transform Domain Techniques:**
    - Applying transformations to data in the frequency or spatial domain. This includes methods like Fourier Transform and Discrete Cosine Transform.

11. **Least Significant Bit (LSB) Steganography:**
    - Modifying the least significant bits of pixel values in images or other data types. LSB steganography is a common and simple technique.

12. **Phase Encoding Steganography:**
    - Concealing information by manipulating the phase of signals, often used in audio steganography.

## Steganography Tools :
- Xiao Steganography
- Image Steganography
- Steghide
- Crypture
- SteganographX Plus
- Camouflage
- OpenStego
- SteganPEG
- Hide’N’Send
- rSteg
- SSuite Picsel
- Our Secret

## Steghide Steganography tool
Steghide is a steganography program that allows you to hide data in various types of images and audio files.   

### Installing Steghide in KaliLInux :
```shell
sudo apt-get install steghide
```   

### Hide text file in image
```shell
sudo xsteghide embed -cf image.jpg -ef secret.txt
```

### Extract text file from image
```shell
sudo steghide extract -sf image.jpg
```

### Display info about the hiden file 
```shell
sudo steghide info image.jpg
```
