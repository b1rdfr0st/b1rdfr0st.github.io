---
title: MailruDownBot - Telegram Mail.ru File Transfer Bot
published: 2022-07-09
updated: 2022-07-09
description: 'A Telegram bot that transfers files from Mail.ru cloud storage to Telegram'
image: ''
tags: [Telegram, Bot, Python, FileTransfer, Cloud]
category: 'Project'
draft: false
---

🇹🇷 Mail.ru'dan telegram'a dosya aktaran bot.

🇬🇧 A bot that upload files from mail.ru to telegram.

Demo in telegram: [@MailruDownBot](https://t.me/MailruDownBot) 🔥 Repo: [HuzunluArtemis/MailruDownBot](https://gitlab.com/HuzunluArtemis/MailruDownBot)

[![](https://img.shields.io/gitlab/license/HuzunluArtemis/MailruDownBot?style=flat)](#)
[![](https://visitor-badge.laobi.icu/badge?page_id=huzunluartemis.MailruDownBot)](#)
[![](https://img.shields.io/twitter/follow/huzunluartemis?&label=twitter&color=blue&style=flat&logo=twitter)](https://twitter.com/HuzunluArtemis)
[![](https://img.shields.io/badge/telegram-up-blue?style=for-the-badge&logo=telegram&logoColor=blue&style=flat)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Frunkit.io%2Fdamiankrawczyk%2Ftelegram-badge%2Fbranches%2Fmaster%3Furl%3Dhttps%3A%2F%2Ft.me/HuzunluArtemis)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/badge/artemis.pages-.dev-blue?style=flat&logo=devdotto&style=flat)](https://artemis.pages.dev/)

## Features

- Task Quee
- Auth users or public
- Limit download size
- Force Subscribe
- Upload with custom filename
- Custom thumbnail for each user. Use: /save /clear /show
- Server stats & Dyno usage for heroku. Use: /stats
- Logger, Pinger, Shell executer

## To-Do

- Add download status like upload status
- Add folder download

## Bot Commands (Set in [@BotFather](https://t.me/BotFather))

```
start - bot help
save - reply a photo to save thumbnail
clear - clear thumbnail
show - show thumbnail
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
- `MAX_FILESIZE`: Allowed max filesize in bytes. Default is telegram's maximum filesize.
- `USE_ARIA2`: Use aria2 for downloads. Faster. Example: `False` Default: `True`
- `LOG_CHANNEL`: Log all downloads for spammers etc. Give channel id or simply your id.
- `HEROKU_API_KEY`: For dyno usage in /stats - Optional.
- `HEROKU_APP_NAME`: For dyno usage in /stats - Optional.
- `CHANNEL_OR_CONTACT`: your users contact link. give your username. example: HuzunluArtemis
- `FORCE_SUBSCRIBE_CHANNEL`: forcesub channel. optional. give channel id like `-1006616516165` or channel username like `HuzunluArtemis`
- Dont use heroku-20 or heroku-18. Use container. Use button.
- `FORCE_DOC_UPLOAD`: Force send all files as document. Without compress videos, photos etc. Example: `True` Default: `False`
- `PROGRESS`: Progress string with 6 variables. See `config.py`.
- `PROGRESSBAR_LENGTH`: Progressbar length. See `config.py`.
- `FINISHED_PROGRESS_STR`: Finished Progress Char. Default: `●`
- `UN_FINISHED_PROGRESS_STR`: Unfinished Progress Char. Default: `○`
- `JOIN_CHANNEL_STR`: Join channel warning string. See `config.py`.
- `YOU_ARE_BANNED_STR`: Banned user string. See `config.py`.
- `JOIN_BUTTON_STR`: Join button string. See `config.py`.

## Deploy

<b>Deploy to Heroku:</b>

- [Open me in new tab](https://heroku.com/deploy?template=https://gitlab.com/HuzunluArtemis/MailruDownBot)
- Fill required variables
- Fill app name (or dismiss)

<b>Deploy to Local:</b>

- install [python](https://www.python.org/downloads/) to your machine
- `git clone https://gitlab.com/HuzunluArtemis/MailruDownBot`
- `cd MailruDownBot`
- `pip install -r requirements.txt`
- `python bot.py`

<b>Deploy to Vps:</b>

- `git clone https://gitlab.com/HuzunluArtemis/MailruDownBot`
- `cd MailruDownBot`
- For Debian based distros `sudo apt install python3 && sudo snap install docker`
- For Arch and it's derivatives: `sudo pacman -S docker python`

## Lisans

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.