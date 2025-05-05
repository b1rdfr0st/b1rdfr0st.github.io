---
title: "ChatSizeBot: Telegram Chat Size Calculator Bot"
date: 2022-07-12 03:20:00 +0200
categories: Project
tags: ["telegram", "python", "telegram-bot"]
image: 
---

## ChatSizeBot

🇹🇷 Telegram Kanal / Grup boyutu hesaplayıcı bot

🇬🇧 Telegram Channel / Group size calculator bot

Demo in telegram: [@ChatSizeBot](https://t.me/ChatSizeBot) 🔥 Repo: [HuzunluArtemis/ChatSizeBot](https://gitlab.com/HuzunluArtemis/ChatSizeBot)

[![](https://img.shields.io/gitlab/license/HuzunluArtemis/ChatSizeBot?style=flat)](#)
[![](https://visitor-badge.laobi.icu/badge?page_id=huzunluartemis.ChatSizeBot)](#)
[![](https://img.shields.io/twitter/follow/huzunluartemis?&label=twitter&color=blue&style=flat&logo=twitter)](https://twitter.com/HuzunluArtemis)
[![](https://img.shields.io/badge/telegram-up-blue?style=for-the-badge&logo=telegram&logoColor=blue&style=flat)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Frunkit.io%2Fdamiankrawczyk%2Ftelegram-badge%2Fbranches%2Fmaster%3Furl%3Dhttps%3A%2F%2Ft.me/HuzunluArtemis)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/badge/artemis.pages-.dev-blue?style=flat&logo=devdotto&style=flat)](https://artemis.pages.dev/)

## Features

- Task Quee
- Public, private chats
- Calculates: `document, video, audio, photo, animation, voice, video_note`
- Progress
- Auth users or public
- Force Subscribe
- Server stats & Dyno usage for heroku. Use: /stats
- Logger, Pinger, Shell executer

## Bot Commands (Set in [@BotFather](https://t.me/BotFather))

```
start - bot help
ping - check bot online status
stats - bot statistics
shell - execute shell command ❗ admin only
log - send bot logs ❗ admin only
```

## Environment Variables

- `BOT_TOKEN`: Telegram Bot Token. Example: `3asd2a2sd32:As56das65d2as:ASd2a6s3d26as`
- `APP_ID`: Telegram App ID. Example: `32523453`
- `API_HASH`: Telegram Api Hash. Example: `asdasdas6d265asd26asd6as1das`
- `AUTH_IDS`: Auth only some groups or users. If you want public, leave it empty or give `0`. Example: `-100656 56191 -10056561`
- `OWNER_ID`: Bot's owner id. Send `/id` to `t.me/MissRose_bot` in private to get your id.
- `HEROKU_API_KEY`: For dyno usage in /stats - Optional.
- `HEROKU_APP_NAME`: For dyno usage in /stats - Optional.
- `CHANNEL_OR_CONTACT`: your users contact link. give your username. example: HuzunluArtemis
- `FORCE_SUBSCRIBE_CHANNEL`: forcesub channel. optional. give channel id like `-1006616516165` or channel username like `HuzunluArtemis`
- You can use heroku-18, 20, 22 or docker deploy.
- `PROGRESSBAR_LENGTH`: Progressbar length. See `config.py`.
- `FINISHED_PROGRESS_STR`: Finished Progress Char. Default: `●`
- `UN_FINISHED_PROGRESS_STR`: Unfinished Progress Char. Default: `○`
- `JOIN_CHANNEL_STR`: Join channel warning string. See `config.py`.
- `YOU_ARE_BANNED_STR`: Banned user string. See `config.py`.
- `JOIN_BUTTON_STR`: Join button string. See `config.py`.

## Deploy

<b>Deploy to Heroku:</b>

- [Open me in new tab](https://heroku.com/deploy?template=https://gitlab.com/HuzunluArtemis/ChatSizeBot)
- Fill required variables
- Fill app name (or dismiss)

<b>Deploy to Local:</b>

- install [python](https://www.python.org/downloads/) to your machine
- `git clone https://gitlab.com/HuzunluArtemis/ChatSizeBot`
- `cd ChatSizeBot`
- `pip install -r requirements.txt`
- `python bot.py`

<b>Deploy to Vps:</b>

- `git clone https://gitlab.com/HuzunluArtemis/ChatSizeBot`
- `cd ChatSizeBot`
- For Debian based distros `sudo apt install python3 && sudo snap install docker`
- For Arch and it's derivatives: `sudo pacman -S docker python`

## Lisans

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.