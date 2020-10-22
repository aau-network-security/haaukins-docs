---
layout: default
title: Forensics
parent: Challenges
nav_order: 1
---


- [Forensics](#forensics)
    - [Difficulty Levels](#difficulty-levels)
  - [Network sniffing](#network-sniffing)
  - [Network scanning](#network-scanning)
  - [Web server login](#web-server-login)
  - [FTP server login](#ftp-server-login)
  - [Vulnerability exploitation](#vulnerability-exploitation)
  - [Man in the Middle](#man-in-the-middle)

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

**Points:** ​ 5 **Difficulty:** ​Very Easy

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


## Web server login

**Points:** ​ 5 **Difficulty:** ​Easy

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

## Vulnerability exploitation

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
- Knowhow to scan a network and what to look after (challenge 1.2)

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
