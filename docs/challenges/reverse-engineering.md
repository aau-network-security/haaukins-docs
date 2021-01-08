---
layout: default
title: Reverse Engineering
parent: Challenges
nav_order: 8
---

- [Reverse Engineering](#reverse-engineering)
    - [Difficulty Levels](#difficulty-levels)
  - [Weird Code](#weird-code)
  - [Conditional Reverse Engineering](#conditional-reverse-engineering)
  - [Reverse APK](#reverse-apk)
  <!-- - [Program Behaviour](#program-behaviour) -->

# Reverse Engineering

 It is typically the process of taking a compiled (machine code,
 bytecode) program and converting it back into a more human readable format.


### Difficulty Levels

The levels of difficulty scale is based on the number of steps required in order to solve the
Training Challenge

- __Very Easy​:__ It requires just one step in order to get the flag
- __Easy:__​ It requires one-two steps, it is based on the challenge category
- __Medium​:__ It requires two-three steps, it is based on the challenge category
- __Hard:__ ​It requires three-four steps based on the challenge category
- __Very Hard:__​ It requires several steps in order to get the flag


## Weird Code

**Points:** ​ 25 **Difficulty:** Easy

**Learning Objectives:**

- Learn the basic syntax of Go Programming language

**Description:** ​This is a Code-base challenge in which the user will have access to an FTP
server in order to download a source code file. The user have to gather the piece of flag
spread over the tricky source code in order to solve the challenge.

**Prerequisite:**
- Basic concepts of a programming language

## Conditional Reverse Engineering

**Points:** ​ 30 **Difficulty:** Easy

**Learning Objectives:**

- Learn what coupled if statements looks like in assembly.

**Description:** ​This challenge is an easy reverse engineering challenge. A binary called StringToHexConverter takes in a text string as an argument.
Normally It would just return the hex string that you could put straight into a printf(). Example could be writing Hello
```bash
$ ./StringToHexConverter Hello
\x48\x65\x6C\x6C\x6F
```
Writing a very specific string will make the program print the flag in the terminal.


**Prerequisite:**
- Little knowledge in assembly language
- Know how to run GDP

## Reverse APK

**Points:** ​ 20 **Difficulty:** Easy

**Learning Objectives:**

- Learn how to decompile an APK and read smali files.

**Description:**
The user has to download an APK from a website and reverse engineer the APK to read the source code of the file in order to solve the challenge.

**Prerequisite:**
- Knowledge of how an android project is structured.

<!-- ## Program Behaviour

**Points:** ​ 10 **Difficulty:** ​Medium

**Learning Objectives:**

- Learn how to crack a program
-
**Description:** ​This is a simple reverse engineering challenge in which the users will have
access to an FTP server in order to download a binary file containing the flag. The main goal
of the challenge is to let understand the user how to crack a program in order to change its
behaviour. It will be necessary to use a debugger tool to analyse and understand the
workflow on the program.

**Prerequisite:**
- Know how to use a debugger tool
- Basic knowledge of Assembly and CPU registers -->
