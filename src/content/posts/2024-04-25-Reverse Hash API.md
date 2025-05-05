---
title: Reverse Hash API with Express and MongoDB
published: 2024-04-25
updated: 2024-04-25
description: 'A REST API built with Express.js and MongoDB for reversing various hash algorithms including MD5, SHA1, and SHA256'
image: ''
tags: [API, Express, MongoDB, Security, Hash]
category: 'Project'
draft: false
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
