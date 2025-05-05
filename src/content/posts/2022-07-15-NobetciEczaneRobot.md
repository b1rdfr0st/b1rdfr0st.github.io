---
title: "NobetciEczaneRobot: Nobetçi Eczaneler Telegram Botu"
date: 2022-07-15 03:20:00 +0200
categories: Project TelegramBot
tags: telegram bot python
image: 
---

🇹🇷 Türkiye'deki Nöbetçi Eczaneleri Listeleyen Bot

🇬🇧 A Bot That Listing Pharmacies on Duty in Turkey

Demo in Telegram: [@NobetciEczaneRobot](https://t.me/NobetciEczaneRobot) 🔥 Repo: [HuzunluArtemis/NobetciEczaneRobot](https://gitlab.com/HuzunluArtemis/NobetciEczaneRobot)

[![](https://img.shields.io/gitlab/license/HuzunluArtemis/NobetciEczaneRobot?style=flat)](#)
[![](https://visitor-badge.laobi.icu/badge?page_id=huzunluartemis.NobetciEczaneRobot)](#)
[![](https://img.shields.io/twitter/follow/huzunluartemis?&label=twitter&color=blue&style=flat&logo=twitter)](https://twitter.com/HuzunluArtemis)
[![](https://img.shields.io/badge/telegram-up-blue?style=for-the-badge&logo=telegram&logoColor=blue&style=flat)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Frunkit.io%2Fdamiankrawczyk%2Ftelegram-badge%2Fbranches%2Fmaster%3Furl%3Dhttps%3A%2F%2Ft.me/HuzunluArtemis)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/badge/artemis.pages-.dev-blue?style=flat&logo=devdotto&style=flat)](https://artemis.pages.dev/)

Makinanızda chrome ve chromedrive ayarlamazsanız selenium ile çekilen websiteleri çalışmaz ama merak etmeyin, diğer alternatifleri kullanabilirsiniz. Websitelerinin hızlı yüklenmesi için seleniuma ublock origin otomatik olarak eklenir (selenyum kullanan apiler için). Aşağıdaki butondan heroku'ya direkt deploy edebilirsiniz. Dockerfile kullanmayın.

Botu olabildiğince uzun süre online tutmaya çalışacağım. Eğer bulunduğunuz ilin merkezindeyseniz ilçeyi merkez olarak girin. Örneğin: `adıyaman merkez`. Sıra önemlidir. İlk önce ili sonra ilçeyi girin.

Kendi projenizde kullanmak için [eczaneScrapers.py](https://github.com/HuzunluArtemis/NobetciEczaneRobot/blob/main/helper_funcs/eczaneScrapers.py) dosyasına göz atabilirsiniz. GPLv3 lisansının izin verdiği koşullar ile kullanabilirsiniz. Kısaca kredi verin. API ve websitesi sahiplerine teşekkürler.

## Features

- Task Quee
- Auth users or public
- 8 Farklı API
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
- `USING_API`: Give one of them:
    - `CollectApi`: Requires `API_KEY` variable. You can get from [here](https://collectapi.com/tr/). Fast.
    - `NosyApi`: Requires `API_KEY` variable. You can get from [here](https://www.nosyapi.com/api/nobetci-eczane). Fast.
    - `EczaneleriOrg`: Free alternative. Fast.
    - `EczanelerGenTr`: Free alternative. Fast.
    - `HastanemyanimdaCom`: Free alternative. Fast.
    - `EczaneleriNet`: Free alternative. Fast.
    - `TrNobetcieczaneCom`: Free alternative. Fast.
    - `EczaIo`: Free alternative. Slow because using selenium. If you on local, install google-chrome and setup chromedriver first.
- `CHROMEDRIVER_PATH`: For sselenium apis. Not required for others. Simply dont fill.
- `GOOGLE_CHROME_BIN`: For sselenium apis. Not required for others. Simply dont fill.
- `HEROKU_API_KEY`: For dyno usage in /stats - Optional.
- `HEROKU_APP_NAME`: For dyno usage in /stats - Optional.
- `CHANNEL_OR_CONTACT`: your users contact link. give your username. example: HuzunluArtemis
- `FORCE_SUBSCRIBE_CHANNEL`: forcesub channel. optional. give channel id like `-1006616516165` or channel username like `HuzunluArtemis`
- Dont use heroku-20 or heroku-18. Use container. Use button.
- `JOIN_CHANNEL_STR`: Join channel warning string. See `config.py`.
- `YOU_ARE_BANNED_STR`: Banned user string. See `config.py`.
- `JOIN_BUTTON_STR`: Join button string. See `config.py`.

## Deploy

<b>Deploy to Heroku:</b>

- [Open me in new tab](https://heroku.com/deploy?template=https://gitlab.com/HuzunluArtemis/NobetciEczaneRobot)
- Fill required variables
- Fill app name (or dismiss)

<b>Deploy to Local:</b>

- install [python](https://www.python.org/downloads/) to your machine
- `git clone https://gitlab.com/HuzunluArtemis/NobetciEczaneRobot`
- `cd NobetciEczaneRobot`
- `pip install -r requirements.txt`
- `python bot.py`

<b>Deploy to Vps:</b>

- `git clone https://gitlab.com/HuzunluArtemis/NobetciEczaneRobot`
- `cd NobetciEczaneRobot`
- For Debian based distros `sudo apt install python3 && sudo snap install docker`
- For Arch and it's derivatives: `sudo pacman -S docker python`

## Lisans

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.