---
title: New Message Forwarder Telegram Bot (NMFTB)
published: 2024-12-25
updated: 2024-12-25
description: 'A serverless Telegram bot built with Cloudflare Workers for automated message forwarding between channels with advanced filtering'
image: ''
tags: [Telegram, Bot, TypeScript, Cloudflare, Workers, Serverless]
category: 'Project'
draft: false
---

A powerful Telegram bot built on Cloudflare Workers that automatically forwards new messages between channels with advanced filtering capabilities. [Source Code](https://gitlab.com/fr0stb1rd/new-message-forwarder-telegram-bot/) \| [Blog Post](https://fr0stb1rd.gitlab.io/posts/New-Message-Forwarder-Telegram-Bot/) \| [Türkçe](https://gitlab.com/fr0stb1rd/new-message-forwarder-telegram-bot/-/blob/main/README.TR.md)

## ✨ Features

- 🔁 Forward messages between multiple Telegram channels or groups
- 🎯 Filter messages by type (text, photos, videos, documents, audio)
- 🔐 Secure permission management and admin controls
- 📊 Track forwarding statistics and history
- 💾 Import/Export forwarding rules as JSON
- ⚡ High performance with Cloudflare Workers
- 🆓 Runs within Cloudflare's free tier limits

## 🛠️ Technology Stack

- **TypeScript**
- **Cloudflare Workers**
- **Cloudflare D1** (SQLite database)
- **Telegram Bot API**
- **Vitest** for testing

# 📸 Screenshots

| Image 1 | Image 2 | Image 3 | Image 4 | Image 5 |
|---------|---------|---------|---------|---------|
| ![01](https://i.ibb.co/FmyFgTN/01.png) | ![02](https://i.ibb.co/1Z3v1JS/02.png) | ![03](https://i.ibb.co/hC3Y1xf/03.png) | ![04](https://i.ibb.co/7pBHQ6N/04.png) | ![05](https://i.ibb.co/PMNTD7H/05.png) |

| Image 6 | Image 7 | Image 8 | Image 9 | Image 10 |
|---------|---------|---------|---------|----------|
| ![06](https://i.ibb.co/PDHw1pZ/06.png) | ![07](https://i.ibb.co/THQsPHn/07.png) | ![08](https://i.ibb.co/gWV0vvH/08.png) | ![09](https://i.ibb.co/1rS6Fj5/09.png) | ![10](https://i.ibb.co/PgHBBW5/10.png) |

## 🚀 Getting Started

### Prerequisites

- Node.js 16 or higher
- npm/yarn
- Cloudflare Workers account
- Telegram Bot Token (get it from [@BotFather](https://t.me/botfather))

### Installation

1. Clone the repository:
   ```bash
   git clone https://gitlab.com/fr0stb1rd/new-message-forwarder-telegram-bot.git
   cd new-message-forwarder-telegram-bot
   npm install
   ```

2. Rename `sample.wrangler.toml` to `wrangler.toml` and configure it:
   ```toml
   name = "new-message-forwarder-telegram-bot"
   main = "src/index.ts"
   compatibility_date = "2024-12-18"
   compatibility_flags = ["nodejs_compat"]

   [observability]
   enabled = true

   [vars]
   TELEGRAM_BOT_USERNAME = "your_bot_username"
   SERVER_URL = "https://your-worker.workers.dev"
   MASTER_WEBHOOK_PATH = "your-secret-path"
   LOG_CHAT = "your-log-chat-id"

   [[d1_databases]]
   binding = "DB"
   database_name = "forwarder"
   database_id = "your-database-id"
   ```

3. Set up secrets:
   ```bash
   wrangler secret put TELEGRAM_BOT_TOKEN
   wrangler secret put ADMINS # Comma-separated list of admin Telegram IDs
   ```

4. Deploy the worker:
   ```bash
   npm run deploy
   ```

5. Initialize the bot:
   ```bash
   curl https://your-worker.workers.dev/init
   ```

## 📝 Usage

### Bot Commands

| Command   | Description                     |
|-----------|---------------------------------|
| `/help`   | Show help message               |
| `/set`    | Set forwarding rules             |
| `/unset`  | Remove forwarding rules          |
| `/list`   | Show active rules                |
| `/check`  | Check channel details            |
| `/export` | Export rules as JSON            |
| `/import` | Import rules from JSON          |
| `/stats`  | View statistics                 |
| `/id`     | Get your Telegram user ID       |

### Ready Command Texts for BotFather

To easily set up your bot, you can use the following command texts to copy and paste into BotFather:

1. **Create a new bot:**
   ```
   /newbot
   ```

2. **Set your bot's username:**
   ```
   YourBotUsername
   ```

3. **Set your bot's display name:**
   ```
   Your Bot Display Name
   ```

4. **Set commands for your bot:**
   ```
   help - Show help message
   set - Set forwarding rules
   unset - Remove forwarding rules
   list - Show active rules
   check - Check channel details
   export - Export rules as JSON
   import - Import rules from JSON
   stats - View statistics
   id - Get your Telegram user ID
   ```

### Message Type Filters

The bot supports filtering messages by type using these codes:

- `v` - Videos
- `p` - Photos
- `a` - Audio files
- `d` - Documents
- `t` - Text messages

### Examples

- **Forward all media types from one channel to another:**
  ```
  /set -100123456789 -100987654321 vpadt
  ```

- **Forward photos and videos from one channel to multiple channels:**
  ```
  /set -100123456789 -100987654321,-100111222333 vp
  ```

- **Forward only text messages from one channel to another:**
  ```
  /set -100123456789 -100987654321 t
  ```

- **Forward videos, photos, and audio files from one channel to multiple channels:**
  ```
  /set -100123456789 -100987654321,-100111222333,-100333444555 vpad
  ```

## 🏗️ Project Structure

```plaintext
src/
├── index.ts          # Entry point and request handler
├── constants.ts      # Constants and message templates
├── types.ts          # TypeScript type definitions
├── database.ts       # Database operations
├── telegram.ts       # Telegram API integration
├── utils.ts          # Utility functions
└── handlers/         # Command and webhook handlers
    ├── index.ts     # Main handler for commands
    ├── channelHandler.ts # Handles channel-related commands
    └── commandHandler.ts  # Handles command processing
```

## 🧪 Development

### Setting up local environment

1. Clone the repository
2. Install dependencies: `npm install`
3. Create a test bot with [@BotFather](https://t.me/botfather)
4. Copy `.dev.vars.example` to `.dev.vars` and fill in your test bot details
5. Start development server: `npm run dev`

### Running tests

```bash
npm test
```
```bash
npm run build
```

## 📚 API Documentation

### Database Schema

#### Forwarding Rules Table

```sql
CREATE TABLE forwarding (
   source_id INTEGER PRIMARY KEY,
   destination_ids TEXT,
   message_types TEXT
);
```

#### Statistics Table

```sql
CREATE TABLE stats (
   source_id INTEGER PRIMARY KEY,
   total_forwards INTEGER DEFAULT 0,
   last_forward TEXT
);
```

#### Bot Table

```sql
CREATE TABLE bot (
   cloudflare_requests INTEGER,
   cloudflare_last_reset_date INTEGER
);
```


### Environment Variables

| Variable                  | Description                          |
|---------------------------|--------------------------------------|
| `TELEGRAM_BOT_TOKEN`      | Your bot's API token                 |
| `TELEGRAM_BOT_USERNAME`   | Bot's username                       |
| `ADMINS`                  | Comma-separated list of admin user IDs |
| `SERVER_URL`              | Your worker's URL                   |
| `MASTER_WEBHOOK_PATH`     | Secret path for webhook             |
| `LOG_CHAT`                | Chat ID for logging                 |

## 🔒 Security

- Bot requires admin privileges in both source and destination channels
- Only authorized admins can manage forwarding rules
- Webhook URL is protected with a secret path
- All database operations are parameterized to prevent SQL injection

## 🐛 Troubleshooting

Common issues and solutions:

1. **Bot not responding**
   - Check if bot token is correct
   - Verify webhook is set properly
   - Ensure bot has required permissions

2. **Forwarding fails**
   - Verify bot is admin in both channels
   - Check if message type is allowed in rules
   - Look for errors in worker logs

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## ⚠️ Disclaimer

This bot is not affiliated with Telegram. Use at your own risk and responsibility. 

I am not responsible for any issues, damages, or consequences that may arise from using this bot. By using this bot, you agree to do so at your own discretion.

## 📧 Contact

Made with ❤️ by [@fr0stb1rd](https://t.me/fr0stb1rd)

Project Link: [https://gitlab.com/fr0stb1rd/new-message-forwarder-telegram-bot](https://gitlab.com/fr0stb1rd/new-message-forwarder-telegram-bot)

## ⚖️ License

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
