---
title: CleanForwardBot - Anonymize and Clean Telegram Messages
published: 2024-07-15
updated: 2024-07-15
description: 'A Telegram bot running on Cloudflare Workers that removes forwarded tags and anonymizes messages'
image: ''
tags: [Telegram, Bot, CloudflareWorkers, Privacy, Automation]
category: 'Project'
draft: false
---

# Clean Forward Bot (Forward Tag Remover Telegram Bot)

This project demonstrates an example application running a Telegram bot on Cloudflare Workers that removes "forwarded" tags from forwarded messages and anonymizes new messages.

Demo in Telegram: [@clean_forward_bot](https://t.me/clean_forward_bot)

## Features

- **Remove "Forwarded" Tags**: Automatically removes "forwarded" tags from messages.
- **Channel Admin Capability**: Requires channel admin permissions with delete permission to function properly.
- **Anonymize New Messages**: Automatically anonymizes new messages sent to the channel.
- **Anonymizes Private Messages**: Anonymizes messages sent privately as well.

## Setup

### Requirements

- Node.js should be installed.
- Uses the GrammY.js library.
- Requires a Telegram bot token and a log channel ID.

### Configuration

1. Set your Telegram bot token in the `BOT_TOKEN` variable.

### Installation Steps

1. Download or clone the project files.
2. Navigate to the project directory in your terminal or command prompt.
3. Run `npm install` to install dependencies.
4. Set up your Cloudflare Workers environment and configure tools like `wrangler`.
5. Deploy your bot to Cloudflare Workers using `wrangler publish`.

### Running the Bot

- Once deployed on Cloudflare Workers, verify that your bot is running on Telegram by using the `/start` command.
- The bot will automatically handle copying media messages and anonymizing new messages.

## Usage

- **/start**: Verifies the bot is running and lists its features.
- **/help**: Provides information about using the bot and its requirements.

## Screenshots

<img alt="private before" src="https://i.ibb.co/QmkGDT4/resim.png" width=160> <img alt="private after" src="https://i.ibb.co/mB3sg61/resim.png" width=160> <img alt="channel before" src="https://i.ibb.co/jhLPkdZ/resim.png" width=160> <img alt="channel after" src="https://i.ibb.co/xffKvL3/resim.png" width=160>

## Source Code

Soon...

## License

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
