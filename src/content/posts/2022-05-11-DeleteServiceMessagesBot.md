---
title: "DeleteServiceMessagesBot: Telegram Service Message Deletion Bot"
date: 2022-05-11 12:10:00 +0200
categories: Project TelegramBot
tags: telegram bot python
image: 
---

🇹🇷 Servis mesajlarını silen reklamsız, basit bir botum. (üye eklendi, üye katıldı, şu bunu ekledi vb. mesajlar) Yapman gereken beni grubuna yönetici olarak ekleyip silme yetkisi vermek. Sonrasını bana bırak.

🇬🇧 I am an ad-free, simple bot that deletes service messages.\n(member added, member joined, this added this, etc. messages) All you have to do is add me to your group as an administrator with delete permission. Leave the rest to me.

🔥 Repo: [HuzunluArtemis/DeleteServiceMessagesBot](https://gitlab.com/HuzunluArtemis/DeleteServiceMessagesBot)

[![](https://img.shields.io/gitlab/license/HuzunluArtemis/DeleteServiceMessagesBot?style=flat)](#)
[![](https://visitor-badge.laobi.icu/badge?page_id=huzunluartemis.DeleteServiceMessagesBot)](#)
[![](https://img.shields.io/twitter/follow/huzunluartemis?&label=twitter&color=blue&style=flat&logo=twitter)](https://twitter.com/HuzunluArtemis)
[![](https://img.shields.io/badge/telegram-up-blue?style=for-the-badge&logo=telegram&logoColor=blue&style=flat)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Frunkit.io%2Fdamiankrawczyk%2Ftelegram-badge%2Fbranches%2Fmaster%3Furl%3Dhttps%3A%2F%2Ft.me/HuzunluArtemis)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/badge/artemis.pages-.dev-blue?style=flat&logo=devdotto&style=flat)](https://artemis.pages.dev/)

## Setting up config file

- `BOT_TOKEN`: Telegram Bot Token. Example: `3asd2a2sd32:As56das65d2as:ASd2a6s3d26as`
- `APP_ID`: Telegram App ID. Example: `32523453`
- `API_HASH`: Telegram Api Hash. Example: `asdasdas6d265asd26asd6as1das`
- `UPDATES_CHANNEL`: Your updates channel or contact bot username. Example: `HuzunluArtemis`

## Deploy

<b>Deploy to Heroku:</b>

- [Open me in new tab](https://heroku.com/deploy?template=https://gitlab.com/HuzunluArtemis/DeleteServiceMessagesBot)
- Fill required variables
- Fill app name (or dismiss)

<b>Deploy to Local:</b>

- install [python](https://www.python.org/downloads/) to your machine
- `git clone https://gitlab.com/HuzunluArtemis/DeleteServiceMessagesBot`
- `cd DeleteServiceMessagesBot`
- `pip install -r requirements.txt`
- `python bot.py`

<b>Deploy to Vps:</b>

- `git clone https://gitlab.com/HuzunluArtemis/DeleteServiceMessagesBot`
- `cd DeleteServiceMessagesBot`
- For Debian based distros `sudo apt install python3 && sudo snap install docker`
- For Arch and it's derivatives: `sudo pacman -S docker python`

## Lisans

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.