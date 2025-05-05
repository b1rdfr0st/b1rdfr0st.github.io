---
title: AntiSpamBot - Telegram Bot with Multiple Protection Options
published: 2022-01-06
updated: 2022-01-06
description: 'A Telegram bot featuring 5 different protection options to combat spam in groups'
image: ''
tags: [Telegram, Bot, Python, Security, AntiSpam]
category: 'Project'
draft: false
---

🇬🇧 Anti spam bot with 5 different protection options

🇹🇷 5 farklı koruma seçenekli anti spam bot

🔥 Repo: [HuzunluArtemis/AntiSpamBot](https://gitlab.com/HuzunluArtemis/AntiSpamBot)

[![](https://img.shields.io/gitlab/license/HuzunluArtemis/AntiSpamBot?style=flat)](#)
[![](https://visitor-badge.laobi.icu/badge?page_id=huzunluartemis.AntiSpamBot)](#)
[![](https://img.shields.io/twitter/follow/huzunluartemis?&label=twitter&color=blue&style=flat&logo=twitter)](https://twitter.com/HuzunluArtemis)
[![](https://img.shields.io/badge/telegram-up-blue?style=for-the-badge&logo=telegram&logoColor=blue&style=flat)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Frunkit.io%2Fdamiankrawczyk%2Ftelegram-badge%2Fbranches%2Fmaster%3Furl%3Dhttps%3A%2F%2Ft.me/HuzunluArtemis)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/badge/artemis.pages-.dev-blue?style=flat&logo=devdotto&style=flat)](https://artemis.pages.dev/)

## Setting up config file
 
- `BOT_TOKEN`: Telegram Bot Token. Example: `3asd2a2sd32:As56das65d2as:ASd2a6s3d26as`
- `APP_ID`: Telegram App ID. Example: `32523453`
- `API_HASH`: Telegram Api Hash. Example: `asdasdas6d265asd26asd6as1das`
- `AUTH_IDS`: Auth only some groups or users. If you want public, leave it empty or give `0`. Example: `-100656 56191 -10056561`
- `BOT_USERNAME`: Your bot's username. without @. Example: `AntiSpamBot`

<b>Other Variables:</b>

- `OWNER_ID`: Bot's owner id. Send `/id` to `t.me/MissRose_bot` in private to get your id Required for logs. If you don't want, leave it empty
- `BAN_ALL_NEWCOMERS`: Set `True` if you dont want users in your group anymore. Default `False`
- `COMBOT_CAS_ANTISPAM`: Set `True` if you want. Default `False`
- `INTELLIVOID_ANTISPAM`: Set `True` if you want. AI Detection. Default `False`
- `SPAMWATCH_ANTISPAM_API`: Give Api ID. Get it from `@SpamWatchBot` in telegram
- `USERGE_ANTISPAM_API`: Give Api ID. Get it from `@UsergeAntispamBot` in telegram
- `SILENT_BAN`: Set `True` if you dont want bot inform you about bans. Default `False`
- `USER_CLEAN_MESSAGE`: Set `True` if you want bot inform you about clean users. Default `False`
- `AUTO_DEL_SEC`: Set `3` if you want delete bot's banned message after 3 secs. Give `0` for no delete. Default `0`
- `CHECK_ALLOWED` Who can check user ban? `auths` or `public` or `disabled` or `owner` Default `owner`
- `DONT_BAN` Do not ban. Only show if there is a reason for ban. Default `False`

## Deploy

<b>Deploy to Heroku:</b>

- [Open me in new tab](https://heroku.com/deploy?template=https://gitlab.com/huzunluartemis/AntiSpamBot)
- Fill required variables
- Fill app name (or dismiss)

<b>Deploy to Local:</b>

- install [python](https://www.python.org/downloads/) to your machine
- `git clone https://gitlab.com/huzunluartemis/AntiSpamBot`
- `cd AntiSpamBot`
- `pip install -r requirements.txt`
- `python bot.py`

<b>Deploy to Vps:</b>

- `git clone https://gitlab.com/huzunluartemis/AntiSpamBot`
- `cd AntiSpamBot`
- For Debian based distros `sudo apt install python3 && sudo snap install docker`
- For Arch and it's derivatives: `sudo pacman -S docker python`

## Lisans

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.