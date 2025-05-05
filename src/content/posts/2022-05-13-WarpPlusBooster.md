---
title: WarpPlusBooster - Automate Cloudflare Warp+ with Ease
published: 2022-05-13
updated: 2022-05-13
description: 'A Python tool for automating Cloudflare Warp+ operations, deployable on Heroku or local machine'
image: ''
tags: [Cloudflare, Python, Automation, Network]
category: 'Project'
draft: false
---

Automate Warp+ cloudflare with heroku (or local python interpreter)

🔥 Repo: [HuzunluArtemis/WarpPlusBooster](https://gitlab.com/HuzunluArtemis/WarpPlusBooster)

[![](https://img.shields.io/gitlab/license/HuzunluArtemis/WarpPlusBooster?style=flat)](#)
[![](https://visitor-badge.laobi.icu/badge?page_id=huzunluartemis.WarpPlusBooster)](#)
[![](https://img.shields.io/twitter/follow/huzunluartemis?&label=twitter&color=blue&style=flat&logo=twitter)](https://twitter.com/HuzunluArtemis)
[![](https://img.shields.io/badge/telegram-up-blue?style=for-the-badge&logo=telegram&logoColor=blue&style=flat)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Frunkit.io%2Fdamiankrawczyk%2Ftelegram-badge%2Fbranches%2Fmaster%3Furl%3Dhttps%3A%2F%2Ft.me/HuzunluArtemis)](https://t.me/HuzunluArtemis)
[![](https://img.shields.io/badge/artemis.pages-.dev-blue?style=flat&logo=devdotto&style=flat)](https://artemis.pages.dev/)

## Setting up config file

- `WARP_ID`: Your warp+ id. Like: `asdf51saf15sa1d-as2d6f26a-31asd-aasd`
- `USE_PROXY`: I dont recommend use proxy mode. `True` or `False`. Default: `False`
- `PROXY_API`: Custom proxy api. Default: `https://api.proxyscrape.com/v2/?request=getproxies&protocol=http&timeout=10000&country=all&ssl=all&anonymity=all`
- `THREAD_COUNT`: Custom thread count for proxy mode. Dont give huge numbers. Your account may get banned. Default: `1000`
- `WAIT_SECS_FOR_NORMAL_MODE`: Waiting seconds between process. Default: `17`

## Thanks

Thanks to original developer: <a href="https://github.com/teppyboy/warp-plus-cloudflare">teppyboy & ALIILAPRO</a> 

## Deploy

<b>Deploy to Heroku:</b>

- [Open me in new tab](https://heroku.com/deploy?template=https://gitlab.com/HuzunluArtemis/WarpPlusBooster)
- Fill required variables
- Fill app name (or dismiss)

<b>Deploy to Local:</b>

- install [python](https://www.python.org/downloads/) to your machine
- `git clone https://gitlab.com/HuzunluArtemis/WarpPlusBooster`
- `cd WarpPlusBooster`
- `pip install -r requirements.txt`
- `python bot.py`

<b>Deploy to Vps:</b>

- `git clone https://gitlab.com/HuzunluArtemis/WarpPlusBooster`
- `cd WarpPlusBooster`
- For Debian based distros `sudo apt install python3 && sudo snap install docker`
- For Arch and it's derivatives: `sudo pacman -S docker python`

## Lisans

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.