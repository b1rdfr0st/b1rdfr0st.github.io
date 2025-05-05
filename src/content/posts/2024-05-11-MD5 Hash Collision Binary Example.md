---
title: Demonstrating MD5 Hash Collision with Binary Files
published: 2024-05-11
updated: 2024-05-11
description: 'A technical exploration of MD5 hash collisions using binary files, demonstrating practical security implications'
image: ''
tags: [Security, MD5, Cryptography, Binary, Tutorial]
category: 'Tutorial'
draft: false
---

## Video

MD5 Binary Çarpışma Örneği

{% include embed/youtube.html id='AHjVO2E-FTU' %}

## POC - Proof of Concept

- Get sample files from [releases](https://gitlab.com/fr0stb1rd/evilize/-/releases) (`evil` and `good` files.)

- Run like bellow:

    ![](https://i.ibb.co/VMWv2M2/image.png)

- The files have same md5: `2c88a72315854541c00d38a04962ba8d`

## Steps

- [Download](https://gitlab.com/fr0stb1rd/evilize) and extract repo as zip:

    ![](https://i.ibb.co/PFYRnKK/image.png)

- Edit the `main_good()` and `main_evil()` functions in  `hello-erase.c` as you want. Like bellow:

    ![](https://i.ibb.co/frRQHrG/image.png)

- `make` it in terminal:

    ![](https://i.ibb.co/BTZpcY1/image.png)

- Compile your program and link against goodevil.o with `gcc hello-erase.c goodevil.o -o hello-erase`

    ![](https://i.ibb.co/XLk1QHW/image.png)

- Execute `./evilize hello-erase -g good -e evil` and wait several hours:

    ![](https://i.ibb.co/kBmXQDw/image.png)

- Check the MD5 checksums of the files "good" and "evil"; they should be the same.
