---
title: "DirectlinkRobot: Generate Direct Download Links from Telegram"
date: 2024-07-15 00:00:00 +0300
categories: Project TelegramBot
tags: telegram bot directlink linkgenerator
image: 
---

# Directlink Robot

Directlink Robot is a Telegram bot designed to generate direct download links for files, videos, and audios sent to it. The bot uses Cloudflare Workers for serverless deployment, ensuring fast and reliable performance.

Demo in Telegram: [@directlink_robot](https://t.me/directlink_robot)

## Features

- Responds to the `/start` command with a welcome message.
- Supported chat types: private, groups, supergroups.
- Handles file, video, and audio messages to generate direct download links.
- Auto rename unnamed videos with a timestamp.
- Limits file sizes to a maximum of 20 MiB due to Telegram Bot API constraints.
- Utilizes encryption for secure message handling.
- Supports CORS for cross-origin requests.

## Setup

1. **Clone the Repository**

   ```bash
   git clone https://gitlab.com/fr0stb1rd/directlink-robot.git
   cd directlink-robot
   ```

2. **Configure Bot Tokens**

   Add your bot tokens in the `BOT_TOKENS` array in the script. You can add multiple tokens separated by a comma.

   ```javascript
   const BOT_TOKENS = ["your_bot_token"];
   ```

3. **Set the Channel ID**

   Set the `CHANNEL_ID` to the ID of your Telegram channel where the bot will forward messages.

   ```javascript
   const CHANNEL_ID = -1000000000;
   ```

4. **Deploy to Cloudflare Workers**

   - Install the [Wrangler CLI](https://developers.cloudflare.com/workers/wrangler/get-started/).

     ```bash
     npm install -g @cloudflare/wrangler
     ```

   - Login to your Cloudflare account.

     ```bash
     wrangler login
     ```

   - Publish your worker.

     ```bash
     wrangler publish
     ```

5. **Set Webhook URL**

   Set the webhook URL for your bot using the following format:

   ```javascript
   const webhook_url = `https://api.telegram.org/bot<your_bot_token>/setWebhook?url=https://<your_worker_url>/webhook`;
   ```

   Replace `<your_bot_token>` with your bot token and `<your_worker_url>` with your Cloudflare Worker URL.

## How It Works

1. **Start Command**

   When a user sends the `/start` command, the bot responds with a welcome message and instructions.

2. **File Handling**

   When a user sends a file, video, or audio, the bot:
   - Forwards the message to the specified channel.
   - Generates a direct download link.
   - Sends the download link to the user.

3. **Download Links**

   The download links are generated using a cipher function to ensure security.

## Functions

- **cipher(textV)**
  - Encrypts the given text using a predefined salt.

- **decipher(textV)**
  - Decrypts the given text using the same salt.

- **handleOptions(request)**
  - Handles CORS preflight requests.

- **getBotToken()**
  - Retrieves a random bot token from the list of tokens.

- **generateRandomString(length)**
  - Generates a random string of the specified length.

- **fetchJson(url)**
  - Fetches JSON data from the specified URL.

- **downloadFile(message_id)**
  - Downloads the file from Telegram using the message ID.

- **handleUpdate(update)**
  - Handles incoming updates from Telegram.

## CORS Headers

The bot includes CORS headers to support cross-origin requests:

```javascript
const corsHeaders = {
    "Access-Control-Allow-Origin": "*",
    "Access-Control-Allow-Methods": "GET, HEAD, POST, OPTIONS",
    "Access-Control-Allow-Headers": "Content-Type",
};
```

## Screenshots

<img alt="private" src="https://i.ibb.co/DMXDRZH/resim.png" width=320> <img alt="group & supergroup" src="https://i.ibb.co/47LP6Vq/resim.png" width=320>

## Source Code

Soon...

## License

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
