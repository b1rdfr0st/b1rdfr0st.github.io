---
title: "Reverse Hash API with Express and MongoDB"
date: 2024-04-25 03:20:00 +0200
categories: Project API
tags: ["hash","md5","sha1","sha256"]
image: 
---
# Reverse Hash API with express and MongoDB.

## Video

{% include embed/youtube.html id='HJMNubbzhmM' %}

## Introduction

Reverse Hash API searches its database for the md5 value you provide. If it finds a match, it returns the password. Every time you query a password, it calculates the MD5 value and saves it in the database. so you can do a reverse md5 query that is publicly accessible Currently only support MD5.

Dependencies: `express`, `mongodb`, `crypto-js`

## Usage

- Live demo: [reversehash.glitch.me](https://reversehash.glitch.me/)

- Usage for password to md5: [/md5?password=fr0stb1rd](https://reversehash.glitch.me/md5?password=fr0stb1rd)

- Usage for md5 to password(s): [/md5?md5=0616396ae9d2ece1258fe54853e76fc6](https://reversehash.glitch.me/md5?md5=0616396ae9d2ece1258fe54853e76fc6)

## Source Code

- Gitlab: [fr0stb1rd/Reverse-Hash-API](https://gitlab.com/fr0stb1rd/reverse-hash-api)
- Glitch: [reversehash](https://glitch.com/edit/#!/reversehash)
