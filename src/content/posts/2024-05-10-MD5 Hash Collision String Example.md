---
title: Demonstrating MD5 Hash Collision with Example Strings
published: 2024-05-10
updated: 2024-05-10
description: 'A practical demonstration of MD5 hash collisions using real string examples and their implications for security'
image: ''
tags: [Security, MD5, Cryptography, Hash, Tutorial]
category: 'Tutorial'
draft: false
---

## Video

MD5 Metin Çarpışma Örneği

{% include embed/youtube.html id='qgIoHwNRNsg' %}

## POC - Proof of Concept

- text1:

    `TEXTCOLLBYfGiJUETHQ4hAcKSMd5zYpgqf1YRDhkmxHkhPWptrkoyz28wnI9V0aHeAuaKnak`

- text2:

    `TEXTCOLLBYfGiJUETHQ4hEcKSMd5zYpgqf1YRDhkmxHkhPWptrkoyz28wnI9V0aHeAuaKnak`

- hash:

    `faad49866e9498fc1719f5289e7a0269`

## Try in Browser

[reversehash.glitch.me](https://reversehash.glitch.me/md5?md5=faad49866e9498fc1719f5289e7a0269)

## Try in Terminal

```
echo -n "TEXTCOLLBYfGiJUETHQ4hAcKSMd5zYpgqf1YRDhkmxHkhPWptrkoyz28wnI9V0aHeAuaKnak" | md5sum
```

```
echo -n "TEXTCOLLBYfGiJUETHQ4hEcKSMd5zYpgqf1YRDhkmxHkhPWptrkoyz28wnI9V0aHeAuaKnak" | md5sum
```
