---
title: "Forensics"
description: "Forensics challenges for Haaukins Platform"
lead: "Forensics challenges for Haaukins Platform"
date: 2020-10-13T15:21:01+02:00
lastmod: 2021-02-28T21:16:01+02:00
draft: false
images: []
menu: 
  docs:
    parent: "challenges"
weight: 100
toc: true
---


- [Forensics](#forensics)
    - [Difficulty Levels](#difficulty-levels)
  - [Network sniffing](#network-sniffing)
  - [Web server login](#web-server-login)
  - [Network scanning](#network-scanning)
  - [SSHtay HYDRAted](#sshtay-hydrated)
  - [Telnet Stream and Login](#telnet-stream-and-login)
  - [Git logs](#git-logs)
  - [FTP server login](#ftp-server-login)
  - [Man in the Middle](#man-in-the-middle)
  - [Steganography](#steganography)
    - [Doormat Steganography](#doormat-steganography)
    - [Steganography Slam](#steganography-slam)
  - [Linux walk-through](#linux-walk-through)
  - [Translator](#translator)
  - [Android Permission Abuse](#android-permission-abuse)
  - [Android Phishing Login Page](#android-phishing-login-page)
    <!-- - [Vulnerability exploitation](#vulnerability-exploitation) -->
    - [Man in the Middle](#man-in-the-middle)
    - [Steganography](#steganography)
        - [Doormat Steganography](#doormat-steganography)
        - [Steganography Slam](#steganography-slam)
    - [Linux walk-through](#linux-walk-through)
  - [Translator](#Translator)
  - [Android Permission Abuse](#Android-Permission-Abuse)
  - [Android Phishing Login Page](#Android-Phishing-Login-Page)

# Forensics

This is a broad category that includes different types of training challenges
such as file format analysis, steganography, memory dump analysis, or network packet
capture analysis. Any challenge to examine and process a hidden piece of information out of
static data files could be considered a Forensics challenge, unless it involves cryptography.

### Difficulty Levels

The levels of difficulty scale is based on the number of steps required in order to solve the
Training Challenge

- __Very Easy​:__ It requires just one step in order to get the flag
- __Easy:__​ It requires one-two steps, it is based on the challenge category
- __Medium​:__ It requires two-three steps, it is based on the challenge category
- __Hard:__ ​It requires three-four steps based on the challenge category
- __Very Hard:__​ It requires several steps in order to get the flag

## Network sniffing

**Points:** ​ 8 **Difficulty:** ​Very Easy

**Learning Objectives:**

- Working with Kali Linux
- Network packets, protocols and software (Wireshark) dedicated to monitor and analyse
network traffic

**Description:** ​The network sniffing challenge, encourages the HAAUKINS user to utilize
basic knowledge about network communication to execute a simple cyber attack of network
eavesdropping. The user is expected to make use of Wireshark, to complete a basic passive
network scan of the local network. By sorting the traffic captured over a short period of time
and analysing the result, the user should be able to successfully locate an unencrypted login
request to a HTTP server. Inspecting this POST request packet, will lead to the flag.

**Prerequisite:**
- Basic knowledge in Linux OS and its terminal
- Wireshark

## Web server login

**Points:** ​ 10 **Difficulty:** ​Easy

**Learning Objectives:**

- Knowledge of HTTP POST requests and why encrypted traffic is so important

**Description:** ​In this challenge, the HAAUKINS user is expected to utilise a combination of
knowledge from the network sniffing and network scanning exercises. By further inspecting
the HTTP POST request packet, the user will be able to find login credentials. This is a
simulation of wiretapping into a network and monitoring the traffic, while someone else
connected to the same network completed a login procedure to an unencrypted website. The
flag is presented to the user, when they access the website connected to the destination
ip-address of the HTTP POST request packet, and successfully logs in using the login
credentials they have just sniffed.

**Prerequisite:**
-  Network scanning

## Network scanning

**Points:** ​ 5 **Difficulty:** ​Very easy

**Learning Objectives:**

- Introduction to NMAP and network scanning
- Knowledge in fingerprinting, ports and specific protocols such as HTTP

**Description:** ​The network scanning challenge is indented as an introduction to
vulnerabilities associated with unencrypted network traffic, HTTP. The HAAUKINS user, is
expected to perform a simple active network scanning procedure of a local subnet using
NMAP. Through analysing the outcome of the scan, it should be possible to locate a
completely open unencrypted webserver, that subsequently can be accessed directly by
ip-address and provide the flag.

**Prerequisite:**
- Basic knowledge in Linux OS and its terminal
- Know what software to use when scanning a network


## SSHtay HYDRAted

**Points:** ​20 **Difficulty:** ​Very easy

**Learning Objectives:**
- Learn how to perform a brute-force attack on an SSH server by using Hydra.
- Learn how to establish constraints for a password alphabet.
- Learn how to reason about the feasibility of the password search space and the impact of parallelization.

**Description:**
In this challenge, users can brute-force a simple password for an SSH server by using Hydra. Hydra is a versatile tool commonly used for brute-forcing login details in penetration testing etc. This tool is known for being really fast, in large part due to its parallelization.

**Prerequisite:**
- Able to work with the Linux CLI.
- Knows how to connect to an SSH server.
- Knowledge of Hydra helps, but ability to google it is sufficient.


## Telnet Stream and Login

**Points:** ​ 8-8  **Difficulty:** ​Easy

**Learning Objectives:**
- Learn how to follow a network stream in Wireshark.

**Description:**
In this exercise the student will have to utilize Wireshark to listen to a network, identify a telnet stream and follow this stream, this stream will then contain the first flag and login credentials to login to the telnet server and find the second flag.

**Prerequisite:**
- Knowledge of Wireshark.
- Knowledge of traffic types.

## Git logs

**Points:** ​ 12  **Difficulty:** ​Easy

**Learning Objectives:**
- Learn that it is important to consider what is committed to a repository.

**Description:**
The challenge consists of one host running ssh, the user the need to log in to this host and find out that the folder "project" is tracked using git.
From there the user then needs to look into the git logs and find out that a password(the flag) is deleted at one of the commits and then go back the the commit before that and find the flag.

**Prerequisite:**
- Knowledge of git file tracking

##  FTP server login

**Points:** ​ 7 **Difficulty:** ​Easy

**Learning Objectives:**

- Introduction to File Transfer Protocol, FTP, and its vulnerabilities such as missing
encryption
- Fingerprinting with NMAP
- Brute force attacks on a live system and why a powerful wordlist can do this easy
- Characteristics of encoding schemes

**Description:** ​FTP servers are used to keep files and deliver it through FT protocol, however
some FTP servers use weak or default passwords which make them vulnerable to brute
force attacks and gain access to files. This challenge requires to brute force FTP server
using default dictionaries on Kali machine in order to achieve flag file.

**Prerequisite:**
- Knowhow to scan a network
- Basic knowledge of Hydra (Kali Tool) or different techniques to make a brute force attack
on a live system

<!-- ## Vulnerability exploitation

**Points:** ​ 10 **Difficulty:** ​Easy

**Learning Objectives:**

- Introduction to the Metasploit framework
- Confidence navigating Kali Linux terminal
- Acquire knowledge about vulnerability search and exploits
-
**Description:** ​In this challenge, the HAAUKINS user is expected to utilise an operating
system specific active network scan, to locate a host connected to the network running an
outdated and extremely vulnerable operating system. By deeper inspection, the user will be
able to retrieve specific information about this host, that will allow them to Google their way
to an exploit using the Metasploit framework for exactly this target. By navigating through
Metasploit and setting up the configuration, the user will be able to gain root access to the
Windows computer. In the final step of the challenge, the user has to navigate through the
filesystem and find a file containing sensitive information.

**Prerequisite:**
- Knowhow to scan a network and what to look after (challenge 1.2) -->

## Man in the Middle

**Points:** ​ 15 **Difficulty:** ​Very hard

**Learning Objectives:**

- ARP spoofing a network

**Description:** ​Man-in-the-middle is an attack where the attacker secretly relays and possibly
alters the communications between two parties who believe that they are directly
communicating with each other. To get the flag the participant will need to act as
man-in-the-middle between a server and a client.

**Prerequisite:**
- Know what a man-in-the-middle attack is
- Know the vulnerabilities attached by only running https on part of the website

## Steganography
### Doormat Steganography
**Points:** ​ 60 **Difficulty:** ​Very hard

**Learning Objectives:**

- Learn how extraneous file headers can be used to detect hidden data in media files.
- Learn how all files are in a sense just byte sequences, and how this knowledge can be used to restore original files.
- Learn how to brute-force crack a 4-digit PIN.

**Description:** ​Data can easily be hidden in media files while preserving file validity and without introducing any noticeable aesthetic changes.
This feature is sometimes exploited in order to transfer malicious executables or other files to a target, bypassing regular antivirus checks etc.
Some modern browsers will warn users against downloading fishy images from fishy websites - when unexpected file headers are detected for instance.
In this challenge the user will ignore this exact precaution in order to get the password to access the flag.
On a website, the user needs an unknown password in order to access the flag inside a "vault", and as per the common trope an extra key is hidden underneath a doormat.
In different terms, the user has to find the bytes of a ZIP file header in a doormat.jpeg file, restore the archive by extracting the necessary bytes, and then crack it in order to get the password to the vault and the flag.

**Prerequisite:**
- Knowledge about the possibility of hiding extra data in media files.
- Knowledge about the use of file headers to interpret different file types.
- Knowledge about the feasibility of brute-forcing simple passwords, like 4-digit PINs.
- Ability to read and write bytes from a file through scripting, the CLI or the like.

### Steganography Slam
**Points:** ​ 14 **Difficulty:** ​Medium

**Learning Objectives:**

- Learning the basic premise of steganography: That extraneous data can easily be hidden in files without compromising their integrity.
- Learning how many other steganography challenges can be solved: By reinterpreting the given data.
- Learning how to inspect raw file data.

**Description:** The basic premise of steganography is that extraneous data can easily be hidden in files, especially media files, without compromising their integrity.
This challenge introduces users to that premise. In order to retrieve the flag, they will have to reinterpret the raw binary data of an image file as ASCII text.
The challenge description and content of the image file hint at the solution.

**Prerequisite:**
- Knowledge about the existence of ASCII as a character encoding.

## Linux walk-through
**Points:** ​ 1-2-3-4-5-6-7-8 **Difficulty:** ​easy

**Learning Objectives:**

- Learn the basic commands of Linux.
- Learn about the file permissions of Linux.
- Learn how to execute binaries within Linux.
- Learn how to navigate around in a Linux terminal environment.

**Description:** This container will contain a number of flags, it will mainly focus on key commands in Linux.
The purpose is to make a Linux environment for the user to learn how to use the terminal environment within Linux.
So it will be very simple challenges which requires the use of _cd_, _ls_, _find_, _nmap_, _grep_ among others.
This will give the user an overview over the Linux environment to continue on all the other challenges on Haaukins.
This is intended for people who never before seen a terminal or worked with Linux for that matter.

**Prerequisite:**
- Know how to open a terminal and type a command.



## Translator
**Points:** 18 - 21 - 23 **Difficulty:** Easy - Medium

**Learning Objectives:**
- Learn how to reverse an apk.
- Learn about apk certificate.
- Learn to follow a packed in wireshark.

**Description**
This app provide an android device a translator that can be used on every site. By highligting a word or sentence on the device the app can be launched on the selection bar. The app then sends the text to be translated online. 
The app is holding secrets that shows information about the request that can be received by revese engineering the app.   
The challenge is using an emulator, wireshark and multiple android tools to get information about the app and the connections it have. 

**Prerequisite:**
- Knowledge of an android project. 
- Knowledge of where information can be found inside an android project. 
- Know how to reverse and read an APK file by using APKTOOL 
- Knowledge of following a stream in wireshark. 

## Android Permission Abuse
**Points:** 27 - 29 **Difficulty:** Medium

**Learning Objectives:**
- Learn how to reverse an apk.
- Learn to read android src code. 
- Learn to follow a packed in wireshark.
- Learn about permissions on android. 

**Description**
This challenge is an apk file that ask for permission from the user and with the permission to read just sending the data in clear text over the internet to an api hosted. This shows a peak into how much data can be acces when got permission, and permission is accepted by most without thinking about this. This is also way in the latast version of android there have been focus on adding more layers to the permission and get the user to actually think about them.

**Prerequisite:**
- Knowledge of an android project. 
- Knowledge of where information can be found inside an android project. 
- Know how to reverse and read an APK file by using APKTOOL.
- Knowledge of following a stream in wireshark. 
- Knowledge of android permissions and what is possible id they are granted. 

## Android Phishing Login Page
**Points:** 37 **Difficulty:** Medium

**Learning Objectives:**
- Learn to follow a packed in wireshark.
- Learn about android app links. 

**Description**
This challenge is using android app link to phishing data from the user. When the app android app is installed on the android device, it is linked with a website it does not own, in this case it is a fake banking website, that have a login screen. When clicking on a link to the website the app launches instead, the app then shows a login screen. When trying to login nothing happens on the screen, but the credentials is send to a server on the network.

**Prerequisite:**
- Knowledge of an android project. 
- Knowledge of following a stream in wireshark. 
- Knowledge of app links on android. 
