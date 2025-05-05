---
title: "AnonymousMessageForwarderBot: Telegram Anonymous Message Forwarder"
date: 2022-06-19 12:10:00 +0200
categories: Project TelegramBot
tags: telegram bot python
image: 
---

🇹🇷 Ben basit bir yönlendirici botuyum.
Gönderdiğiniz her mesajı anonimleştiririm.
Benim göndereceğim mesajı gönderirsiniz.
Böylece mesajı sizin gönderdiğiniz belli olmaz.

🇬🇧 This a simple forwarder bot.
I anonymize every message you send
You send the message I sent.
Thus, it is not clear that you sent the message.

🔥 Repo: [HuzunluArtemis/AnonymousMessageForwarderBot](https://gitlab.com/HuzunluArtemis/AnonymousMessageForwarderBot)

[![](https://img.shields.io/gitlab/license/HuzunluArtemis/AnonymousMessageForwarderBot?style=flat)](#)
[![](https://visitor-badge.laobi.icu/badge?page_id=huzunluartemis.AnonymousMessageForwarderBot)](#)
[![](https://img.shields.io/twitter/follow/huzunluartemis?&label=twitter&color=blue&style=flat&logo=twitter)](https://twitter.com/HuzunluArtemis)
[![](https://img.shields.io/badge/telegram-up-blue?style=for-the-badge&logo=telegram&logoColor=blue&style=flat)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Frunkit.io%2Fdamiankrawczyk%2Ftelegram-badge%2Fbranches%2Fmaster%3Furl%3Dhttps%3A%2F%2Ft.me/HuzunluArtemis)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/badge/artemis.pages-.dev-blue?style=flat&logo=devdotto&style=flat)](https://artemis.pages.dev/)

## Setting up config file

- `BOT_TOKEN`: Telegram Bot Token. Example: `3asd2a2sd32:As56das65d2as:ASd2a6s3d26as`
- `APP_ID`: Telegram App ID. Example: `32523453`
- `API_HASH`: Telegram Api Hash. Example: `asdasdas6d265asd26asd6as1das`
- `UPDATES_CHANNEL`: Your updates channel or contact bot username. Example: `HuzunluArtemis`
- `FORCE_SUBSCRIBE_CHANNEL`: Force-subscribe channel. Example: `HuzunluArtemis`
- `OWNER_ID`: Type `/id` to @MissRose_bot to get this value. Example: `2323423423`
- `AUTH_IDS`: Id's of bot users, seperate with blank. Leave it empty for public. Example: `2323423423 325345`
- `BOT_USERNAME`: Bot's username. Example: `@AnonimSenderBot`
- `SEND_AS_REPLY`: Send copy message as reply to your message. Example: `1` or `0`

## Deploy

<b>Deploy to Heroku:</b>

- [Open me in new tab](https://heroku.com/deploy?template=https://gitlab.com/HuzunluArtemis/AnonymousMessageForwarderBot)
- Fill required variables
- Fill app name (or dismiss)

<b>Deploy to Local:</b>

- install [python](https://www.python.org/downloads/) to your machine
- `git clone https://gitlab.com/HuzunluArtemis/AnonymousMessageForwarderBot`
- `cd AnonymousMessageForwarderBot`
- `pip install -r requirements.txt`
- `python bot.py`

<b>Deploy to Vps:</b>

- `git clone https://gitlab.com/HuzunluArtemis/AnonymousMessageForwarderBot`
- `cd AnonymousMessageForwarderBot`
- For Debian based distros `sudo apt install python3 && sudo snap install docker`
- For Arch and it's derivatives: `sudo pacman -S docker python`

## Lisans

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.