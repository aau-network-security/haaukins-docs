---
title: "Cryptography"
description: "Cryptography challenges for Haaukins Platform"
lead: "Cryptography challenges for Haaukins Platform"
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

- [Cryptography](#cryptography)
    - [Difficulty Levels](#difficulty-levels)
  - [JS Crypto Client](#js-crypto-client)
  - [MD5 Collision Course](#md5-collision-course)
  - [Lurking in the shadows](#lurking-in-the-shadows)
  - [SSH Vigenère Vignette](#ssh-vigenère-vignette)

# Cryptography

The main goal is usually to crack or clone cryptographic objects or algorithms to reach the flag.

### Difficulty Levels

The levels of difficulty scale is based on the number of steps required in order to solve the
Training Challenge

- __Very Easy​:__ It requires just one step in order to get the flag
- __Easy:__​ It requires one-two steps, it is based on the challenge category
- __Medium​:__ It requires two-three steps, it is based on the challenge category
- __Hard:__ ​It requires three-four steps based on the challenge category
- __Very Hard:__​ It requires several steps in order to get the flag


## JS Crypto Client

**Points:** ​ 10 **Difficulty:** Easy

**Learning Objectives:**

- Understanding of cryptography algorithms

**Description:** ​The challenge is based on ​a rotation of the Caesar’s cipher encryption.
Challenge includes only index.html file which contains the encrypted flag through some JS
code.

**Prerequisite:**
- Know how Caesar’s cipher encryption techniques works

## MD5 Collision Course

**Points:** ​ 40 **Difficulty:** Easy

**Learning Objectives:**

- Learning the basic premise of hash security checks and collision attacks.
- Learning how MD5 hashing is less optimal for security applications due to the relative ease of constructing collisions.
- Learning how to give hexadecimal inputs in the terminal for other challenges.
- Learning how a little bit of brute-forcing might be viable for solving a challenge.

**Description:** ​MD5 hashing was originally meant to be a function used for security applications.
However, due to the relative ease of constructing colliding hashes, spoofing passwords and file checksums alike, the MD5 is now considered to be "cryptographically broken".
In this challenge, users will have to exploit a simple property holding for some MD5 collisions in order to construct an admin key, granting access to the flag.
Collision attacks like the one in the challenge are probably not seen in the wild very often. However, decisions were made in order to make the challenge easier, since the necessary computations for the attack usually are quite extensive.

**Prerequisite:**
- Knowledge about hexadecimal values and their relationship to bits, bytes and ASCII.

## Lurking in the shadows

**Points:** ​ 10 **Difficulty:** Medium

**Learning Objectives:**

- More knowledge about password hashes and brute forcing of these.

**Description:** This challenge is just a simple brute force challenge, where the user has been granted access to the shadow file.
The user will then need to retrieve the root password hash and crack it to login to the ssh server with root privileges.
The flag will be in the user home directory.

**Prerequisite:**
- Have heard about brute forcing.

## SSH Vigenère Vignette

**Points:** ​ 50 **Difficulty:** Medium

**Learning Objectives:**

- Learn how the cyclical application of the keyword is an important weakness of polyalphabetic ciphers.
- Learn how hashes can be used to reverse engineer unknown values.
- Possibly gain a better understanding of how the Vigenère cipher works.
- Possibly gain hands-on experience with implementing encryption/decryption algorithms.

**Description:** The Vigenère cipher can be construed as a more convoluted version of the Caesar cipher: The letters of a keyword are applied as offsets to the plaintext in a cyclical fashion in order to obscure the original message instead of always using the same offset on each plaintext letter. For instance, applying the keyword LEMON to the plaintext ATTACKATDAWN cyclically, i.e. applying LEMONLEMONLE, produces the cipher LXFOPVEFRNHR when using the zero-based enumeration of the capitalized English alphabet.
While it was historically known as "the indecipherable cipher", in many cases information about the cipher keyword can easily be obtained through statistical methods such as the Kasiski and Friedman analyses - relying upon assumptions about recurrent substrings and letters in real-life language use, respectively. Fully automated tools for deciphering Vigenère-encrypted texts exist online and are often used in a CTF setting to solve these challenges very quickly.
With this challenge it was attempted to require a more hands-on approach in order to break the cipher. In order to access the flag, the user has to decrypt the password to an SSH server by utilizing knowledge about how the Vigenère cipher works, and what its weaknesses are. Overall, the given information is limited and fragmented in a way that makes it harder to use statistics reliably:

- The available cipher text is relatively short.
- There are no recurrent cipher substrings of length above 1.
- The encryption alphabet deviates from a typical language alphabet in its motley character set and letter case distinction.
- Some plaintext is encoded in heavily stylized "leetspeak", deviating from normal language use.

This hopefully makes it more difficult to rely on automated tools for crypto analysis, making the challenge a better learning opportunity.

**Prerequisite:**
- Proficiency in and access to a programming language with facilities for quickly generating SHA-256 hashes.
- Mathematical background for understanding how the Vigenère cipher works, namely the modulo operation.
- Fundamental knowledge of what a hash value is.
- Ability to evaluate the feasibility of brute-force solutions.
