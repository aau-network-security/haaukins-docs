---
layout: default
title: Binary
parent: Challenges
nav_order: 2
---

- [Binary](#binary)
    - [Difficulty Levels](#difficulty-levels)
  - [Set User ID](#set-user-id)
  - [Format String Exploitation](#format-string-exploitation)
  - [Shrunk-Chunk Heap Overflow](#shrunk-chunk-heap-overflow)
  <!-- - [Buffer Overflow](#buffer-overflow) -->
  - [Format String Exploitation](#format-string-exploitation)
  - [Shrunk-Chunk Heap Overflow](#shrunk-chunk-heap-overflow)

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

**Points:** ​ 30 **Difficulty:** ​Easy

**Learning Objectives:**
- Learn how to escalate the privilege and get root access
- ​Scanning a system to check if programs have specific privileges

**Description:** ​In this challenge the users will have access to an SSH session in which there
are a file containing the flag. That file is only readable by user with root privileges. In order to
solve the challenge the user will have to find the command for which is set the SUID bit and
then escalate privileges in order to open the file containing the flag.

**Prerequisite:**
- Basic usage of Linux from command line
- Know Linux user permissions

<!-- ## Buffer Overflow

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
- Basic knowledge of Assembly -->

## Format String Exploitation

**Points:** ​ 35 **Difficulty:** ​Medium

**Learning Objectives:**
- Learn how to read data from the stack using format strings while avoiding memory access violations.

**Description:** This challenge is about utilizing a simple format string exploit. A program named FormatString plays a game with the user, who has to guess the password, while the program repeats the user's guesses, using printf() on the input string. As it turns out, printf(), along with similar functions, has the quirk that it will carelessly read data off the stack when it looks for arguments corresponding to format specifiers in its control string - even when no arguments are specified, e.g.:
```
printf("%s %x %d %c");
```
Providing input with the right format specifiers will make the program slip up and reveal the password, hiding somewhere on the stack, on its own accord. Entering the password will make the program print the flag.


**Prerequisite:**
- Knowledge of where and how functions in the printf() school of thought look for their arguments.
- Basic knowledge of how the stack and its frames are organized.
- Basic knowledge of memory access through pointers and when they are legal/illegal (e.g. Segmentation faults).

## Shrunk-Chunk Heap Overflow

**Points:** ​ 70 **Difficulty:** ​hard

**Learning Objectives:**
- Knowledge of how metadata on the heap itself is used for its memory management, and how it can be exploited.
- Knowledge of how certain sequences of (de)allocations on the heap can produce overlapping chunks in previous glibc versions.
- Knowledge of how the difference between stack and heap memory management provides different approaches for buffer overflow attacks.
- Proficiency in examining the state of the heap and its allocations during runtime.
- Better understanding of how `malloc`, `free` and similar functions work.

**Description:**
This challenge is based on an overflow vulnerability in glibc popularized in a paper named 'Glibc Adventures: The Forgotten Chunks'. It has only been patched in relatively recent releases compared to other heap exploits. In essence, an overflow of a single null byte corrupting heap metadata and a specific sequence of malloc/free calls leads to two chunks on the heap overlapping. This is possible due to an absence of security checks in dynamic memory management. Since there are two overlapping allocations, exploiters might have indirect control over the memory area that the heap manager has "forgotten about" through another area. This opens up a lot of possibilities for memory writes and redirection of program execution.
In this challenge users will be presented with a binary (source code available) with a seemingly harmless "off-by-one" error causing the above vulnerability. By causing heap overflow with a single null byte the users can overwrite a global function pointer, redirecting program execution to call print_flag(). The program itself is fairly contrived and artificial in the way that it works, but this was chosen in order to provide a better signal-to noise-ratio for the users: Tracking several malloc/free calls will be important for solving the challenge. It runs inside a Debian 8.11 image utilizing a vulnerable glibc 2.19 implementation, and all default protection measures are in place.


**Prerequisite:**
- Knowledge of the C programming language and commonly used functions in its standard library - namely `strlen`, `strcpy`, `malloc` and `free`.
- Knowledge of the existence of metadata on the heap itself in order to perform dynamic memory management.
- Knowledge of the ELF format and the exploitability of the .got.plt table to redirect program execution.
- Ability to use tools such as GDB, objdump and ltrace to examine binary files and runtime memory state.
- Ability to use Bash or Python in order to provide long/hexadecimal input to the program.
