---
title: utube - YouTube Uploader Telegram Bot
published: 2022-07-23
updated: 2022-07-23
description: 'A Telegram bot that uses YouTube Data API v3 to upload videos directly to YouTube from Telegram'
image: ''
tags: [Telegram, Bot, Python, YouTube, Upload]
category: 'Project'
draft: false
---

Simple [telegram bot](https://core.telegram.org/bots "Telegram Bots") which uses [Youtube Data API v3](https://developers.google.com/youtube/v3/ "Youtube Data API v3") to upload videos to Youtube. Written in python3. Here is [repo](https://github.com/fr0stb1rd/utube).

## Features From This Repo:

- upgraded to pyrogram 2.0.34 (now you can upload up to 4GB)
- added bot commands
- auto pin auth message. user can easily find auth json message
- fixed some typo & refactored
- local config.env support
- disabled repo creator's id from every bot generated from this repo!

## Local Deploy

```bash
$ git clone https://gitlab.com/fr0stb1rd/utube.git
$ cd utube
$ python3 -m venv venv
$ source venv/bin/activate
```

## Heroku Deploy

[Tutorial?](https://www.youtube.com/watch?v=LSs8b5dMWIA)

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

## Environment Variables

- `BOT_TOKEN` (Required) - Get your bot token from [Bot Father](https://tx.me/BotFather "Bot Father").
- `SESSION_NAME` (optional) - Your bot's username.
- `API_ID` (Required) - Your telegram api id, get from [Manage Apps](https://my.telegram.org).
- `API_HASH` (Required) - Your telegram api hash, get from [Manage Apps](https://my.telegram.org).
- `CLIENT_ID` (Required) - Your google client id.
- `CLIENT_SECRET` (Required) - Your google client secret.
- `BOT_OWNER` (Required) - Telegram id of bot owner.
- `AUTH_USERS` (optional) - Telegram id's of authorised users, separated by `,`.
- `VIDEO_DESCRIPTION` (optional) - Any default description to be aded to the video.
- `VIDEO_CATEGORY` (optional) - YouTube's video category id. If not specified or specified id is invalid, category id will be selected randomly.
- `VIDEO_TITLE_PREFIX` (optional) - Any prefix to be added to the video's title.
- `VIDEO_TITLE_SUFFIX` (optional) - Any suffix to be added to the video's title.
- `UPLOAD_MODE` (optional) - The video's privacy status. Valid values for this property are: `private`, `public`, `unlisted`.
- `DEBUG` (optional) - Whether to set logging level to DEBUG. If set logging will be set to DEBUG level, else INFO level.

## Get `CLIENT_ID` and `CLIENT_SECRET`

- Head to [Google console](https://console.developers.google.com "Google console"), create a new project named `Youtube Uploader` and enable `API'S AND SERVISES`. Search for `YOUTUBE DATA API v3` and enable the API. Go to [Credentials](https://console.developers.google.com/apis/credentials "Credentials") page, select your project `Youtube Uploader` create a new credential with `desktop` as type. Copy the `CLIENT_ID` and `CLIENT_SECRET`.
- You have to verify your application with google, only then you can make the uploaded videos public. YouTube changed its developer policy, and videos uploaded using unverfied applications will be kept private.

## Bot Commands - Set in [@BotFather](https://t.me/BotFather)

```
start - Start the bot
help - Bot help
authorise - Auth with code. Example: /authorise abcdef12345
save_auth_data - Reply to authorise code
upload - Reply a video to upload
```

## Special Notes

- With the Youtube Data API you are awarded with 10,000 points of requests. For one video upload it costs 1605 points, regardless of file size, which calculates to about 6 uploads daily. Once you have exhausted your daily points, you have to wait till daily reset. Resets happens at 0:00 PST, i.e. 12:30 IST. So make your uploads count.

- Uploading copyright contents will leads to immediate blocking of the video.

- By default, all the videos are uploaded as private with random category id unless you provide `UPLOAD_MODE` and `VIDEO_CATEGORY`. You may change it after youtube processes the video.

## Screenshots

[<img alt="overview" src="https://github.com/fr0stb1rd/utube/raw/master/ss/overview.jpg" width=160>](https://github.com/fr0stb1rd/utube/raw/master/ss/overview.jpg)
[<img alt="bot-start" src="https://github.com/fr0stb1rd/utube/raw/master/ss/bot-start.jpg" width=160>](https://github.com/fr0stb1rd/utube/raw/master/ss/bot-start.jpg)
[<img alt="bot-help" src="https://github.com/fr0stb1rd/utube/raw/master/ss/bot-help.jpg" width=160>](https://github.com/fr0stb1rd/utube/raw/master/ss/bot-help.jpg)
[<img alt="bot-authorise" src="https://github.com/fr0stb1rd/utube/raw/master/ss/bot-authorise.jpg" width=160>](https://github.com/fr0stb1rd/utube/raw/master/ss/bot-authorise.jpg)
[<img alt="bot-upload" src="https://github.com/fr0stb1rd/utube/raw/master/ss/bot-upload.jpg" width=160>](https://github.com/fr0stb1rd/utube/raw/master/ss/bot-upload.jpg)

## Lisans

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
