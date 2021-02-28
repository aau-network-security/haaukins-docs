---
title: "Reverse Engineering"
description: "Reverse Engineering challenges for Haaukins Platform"
lead: "Reverse Engineering challenges for Haaukins Platform."
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


- [Reverse Engineering](#reverse-engineering)
    - [Difficulty Levels](#difficulty-levels)
  - [Weird Code](#weird-code)
  - [Conditional Reverse Engineering](#conditional-reverse-engineering)
  - [Reverse APK](#reverse-apk)
  - [PWN_strings](#pwn_strings)
  - [C0ffee 0verfl0w](#c0ffee-0verfl0w)
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

## PWN_strings

**Points:** ​ 20, 42 **Difficulty:** Easy, Medium

**Learning Objectives:**

- Learn how to disassemble and do forensics on binaries, to be able crack the executable binary.  


**Description:**
This is a simple reverse engineering challenge composed of two challenges. Further investigation by applying the right tools for reverse engineering binaries will unveil more information on how to find the first and second flags.
1. Strings_everywhere  
    Difficulty: Easy  
    The binary for the callenge can be found and downloaded from `pwn-strings.com` website. The tools used to find the frist flag in the frist part of the challenge is `strings`, `grep` or a different tool to extract strings in binaries.
    
2. OWN_if_statement  
    Difficulty: Medium   
    The binary for the callenge can be found and downloaded from `pwn-strings.com` website. The tools used to find the second flag is debugging software such as `gdb` or other disassembly software such as radare2(r2). 

**Prerequisite:**
- Know how to use gdb (GNU Debugger) or radare2 (Reverse Engineering Framework)  
- Basic understanding of Assembler instructions in 32-bit   

## C0ffee 0verfl0w

**Points:** ​ 42 **Difficulty:** Medium

**Learning Objectives:**

- Learn how to take advantage of a buffer overflow/overrun. Another objective is to do forensics on the binary and decrypt the prices of successfully exploiting the overflow  


**Description:**
The challenge is a buffer overflow challenge. To retrieve the flag a buffer must be exploited correctly. A string will be presented when successfully exploited which then must be decrypted and deobfuscated from two formats namely, from hex and from base85 to obtain the flag.

1. C0ffee_0verfl0w  
    Difficulty: Medium  
    Browse C0ffee-0verfl0w.com and download the binary. When the binary has been exploited succesfully you will receive an encrypted flag. Decrypt the flag with openssl using the key; ThisMightBecomeHandy42. Algorithm used is AES256 and the cipher text is base64 encoded.

**Prerequisite:**
- Know how to use r2/radare2(Reverse Engineering Framework) or gdb (GNU Debugger)
- Basic understanding of Assembler instructions in 32-bit   
- Basic understanding of encryption/decryption schemes and string formats   

