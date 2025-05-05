---
title: ShortenerBot - Telegram Link Shortener with Multiple Services
published: 2022-01-12
updated: 2022-01-12
description: 'A Telegram bot that supports 20+ URL shortening services for link shortening'
image: ''
tags: [Telegram, Bot, Python, URL, Shortener]
category: 'Project'
draft: false
---

🇬🇧 Telegram Link Shortener Bot (11 + 9 Shorteners)

🇹🇷 Telegram Link Kısaltıcı Bot (11 + 9 Kısaltıcı)

🔥 Repo: [HuzunluArtemis/ShortenerBot](https://gitlab.com/HuzunluArtemis/ShortenerBot)

[![](https://img.shields.io/gitlab/license/HuzunluArtemis/ShortenerBot?style=flat)](#)
[![](https://visitor-badge.laobi.icu/badge?page_id=huzunluartemis.ShortenerBot)](#)
[![](https://img.shields.io/twitter/follow/huzunluartemis?&label=twitter&color=blue&style=flat&logo=twitter)](https://twitter.com/HuzunluArtemis)
[![](https://img.shields.io/badge/telegram-up-blue?style=for-the-badge&logo=telegram&logoColor=blue&style=flat)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Frunkit.io%2Fdamiankrawczyk%2Ftelegram-badge%2Fbranches%2Fmaster%3Furl%3Dhttps%3A%2F%2Ft.me/HuzunluArtemis)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/badge/artemis.pages-.dev-blue?style=flat&logo=devdotto&style=flat)](https://artemis.pages.dev/)

## ShortenerBot:

All supported domains: v.gd, da.gd, is.gd, ttm.sh, clck.ru, chilp.it, osdb, tinyurl, owly

Requires APIKEY: shorte.st, bc.vc, pubiza, linkvertise, bit.ly, post, cutt.ly, adf.ly, shortcm, tinycc, ouo.io

## Setting up config file

Required Variables:

- `BOT_TOKEN`: Telegram Bot Token. Example: `3asd2a2sd32:As56das65d2as:ASd2a6s3d26as`
- `APP_ID`: Telegram App ID. Example: `32523453`
- `API_HASH`: Telegram Api Hash. Example: `asdasdas6d265asd26asd6as1das`
- `AUTH_IDS`: Auth only some groups or users. If you want public, leave it empty or give `0`. Example: `-100656 56191 -10056561`
- `BOT_USERNAME`: Your bot's username. without @. Example: `ShortenerBot`

Other Variables:

- `OWNER_ID`: Bot's owner id. Send `/id` to `t.me/MissRose_bot` in private to get your id Required for logs. If you don't want, leave it empty
- Shortener Variables:
  - Not required signup: `v.gd`, `da.gd`, `is.gd`, `ttm.sh`, `clck.ru`, `chilp.it`, `osdb`, `owly`
  - Required signup: `shorte.st`, `bc.vc`, `pubiza`, `linkvertise`, `bit.ly`, `post`, `cutt.ly`, `adf.ly`, `shortcm`, `tinycc`, `tinyurl`, `ouo.io`
  - `shortest`: Enter Api Key if you want.
  - `bcvc`: Enter Api Key if you want. bc.vc sample api: `"2dgdg5f1fgag7cg6f0622&uid=45634"`
  - `pubiza`: Enter Api Key if you want. pubiza sample api: `"hsdfgCgdgrsdfgsfgfgsdgLsfgXef mainstream"`. Split api key and ad type with a space. Genel içerik için: `mainstream` Yetişkin içerik için: `adult` İçerik Kilidi için: `content_locker`
  - `linkvertise`: Enter Api Key if you want.
  - `bitly`: Enter Api Key if you want.
  - `post`: Enter Api Key if you want.
  - `cuttly`: Enter Api Key if you want.
  - `adfly`: Enter Api Key if you want. adfly sample api: `"hsdfgCgdgrsdfgsfgfgsdgLsfgXef 51515155"` Split api key and user id with a space.
  - `shortcm`: Enter Api Key if you want. shortcm sample api: `"hsdfgCgdgrsdfgsfgfgsdgLsfgXef abcdotcom"` Split api key and domain with a space.
  - `tinycc`: Enter Api Key if you want. tinycc sample api: `"hsdfgCgdgrsdfgsfgfgsdgLsfgXef tinyccusername"` Split api key and username with a space.
  - `ouoio`: Enter Api Key if you want.
- `AUTO_DEL_SEC`: Global auto deletion seconds. Default 10.
- `AUTO_SHORT_MOTOR`: If you want auto shorting, fill like `is.gd`. Useful for groups / channels. Auto Shorting. Default None. If you dont want, dont fill.
- `DELETE_AUTO_SHORTENED`: Auto delete, auto-shortened link; after `AUTO_DEL_SEC` secs. Default False.
- `DELETE_COMMAND_SHORTENED`: Auto delete, shortened with command link; fter `AUTO_DEL_SEC` secs. Default False.

## Deploy

<b>Deploy to Heroku:</b>

- [Open me in new tab](https://heroku.com/deploy?template=https://gitlab.com/HuzunluArtemis/ShortenerBot)
- Fill required variables
- Fill app name (or dismiss)

<b>Deploy to Local:</b>

- install [python](https://www.python.org/downloads/) to your machine
- `git clone https://gitlab.com/HuzunluArtemis/ShortenerBot`
- `cd ShortenerBot`
- `pip install -r requirements.txt`
- `python bot.py`

<b>Deploy to Vps:</b>

- `git clone https://gitlab.com/HuzunluArtemis/ShortenerBot`
- `cd ShortenerBot`
- For Debian based distros `sudo apt install python3 && sudo snap install docker`
- For Arch and it's derivatives: `sudo pacman -S docker python`

## Lisans

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.