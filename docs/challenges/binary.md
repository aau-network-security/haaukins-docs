---
layout: default
title: Binary
parent: Challenges
nav_order: 5
---

- [Binary](#binary)
    - [Difficulty Levels](#difficulty-levels)
  - [Set User ID](#set-user-id)
  - [Buffer Overflow](#buffer-overflow)

# Binary

Binary exploitation is the process of subverting a compiled application such that it violates some trust boundary in a way that is advantageous to the attacker. It comes down by abusing vulnerabilities that corrupt memory in software or by finding a vulnerability in the program and exploiting it in order to escalate privileges.

### Difficulty Levels

The levels of difficulty scale is based on the number of steps required in order to solve the
Training Challenge

- __Very Easy​:__ It requires just one step in order to get the flag
- __Easy:__​ It requires one-two steps, it is based on the challenge category
- __Medium​:__ It requires two-three steps, it is based on the challenge category
- __Hard:__ ​It requires three-four steps based on the challenge category
- __Very Hard:__​ It requires several steps in order to get the flag



## Set User ID

**Points:** ​ 10 **Difficulty:** ​Easy

**Learning Objectives:**
- Learn how to escalate the privilege and get root access
- ​Scanning a system to check if programs have specific privileges
  
**Description:** ​In this challenge the users will have access to an SSH session in which there
are a file containing the flag. That file is only readable by user with root privileges. In order to
solve the challenge the user will have to find the command for which is set the SUID bit and
then escalate privileges in order to open the file containing the flag.

**Prerequisite:**
- Basic usage of linux from command line
- Know linux user permissions

## Buffer Overflow

**Points:** ​ 20 **Difficulty:** ​Medium

**Learning Objectives:**
- Learn how the processes are held in the memory
- Learn how to exploit a buffer overflow through shellcode
- Learn how to manipulate memory and it’s registers to execute malicious code
  
**Description:** ​In this challenge the users will have access to an SSH session in which there
are a file containing the flag. That file is only readable by user with root privileges. The
challenge will require the user to find a program which has SUID bit set and is vulnerable to
buffer overflow. The main goal is to debug the program in order to find how many bytes are
necessary for the buffer to overwrite the instruction pointer and then write some assembly
code to get root privileges.

**Prerequisite:**
- Know what is a buffer overflow
- Know how to debug a binary file
- Basic knowledge of Assembly

