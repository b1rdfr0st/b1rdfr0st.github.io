---
title: "Group Member Balancer Telegram Bot (GMBTB)"
date: 2025-02-17 00:00:00 +0300
categories: Project TelegramBot
tags: telegram bot typescript cloudflare workers serverless balancer
image: 
---

A powerful Telegram bot built on Cloudflare Workers that automatically balances group members by setting rules to ban or kick users based on their membership in other groups. [Source Code](https://gitlab.com/fr0stb1rd/group-member-balancer-telegram-bot/) \| [Blog Post](https://fr0stb1rd.gitlab.io/posts/Group-Member-Balancer-Telegram-Bot/) \| [Live Bot](https://t.me/gmbtelegrambot)

## ✨ Features

- 🔄 Automatically balance members between groups
- 🔐 Secure permission management and admin controls
- 📊 Track rule settings and history
- 💾 Import/Export rules as JSON
- ⚡ High performance with Cloudflare Workers
- 🆓 Runs within Cloudflare's free tier limits

## 🛠️ Technology Stack

- **TypeScript**
- **Cloudflare Workers**
- **Cloudflare D1** (SQLite database)
- **Telegram Bot API**
- **Vitest** for testing

# 📸 Screenshots

| Image 1 | Image 2 | Image 3 | Image 4 |
|---------|---------|---------|---------|
| ![01](https://i.ibb.co/bMyGNgGL/01.png) | ![02](https://i.ibb.co/84Q1HcsG/02.png) | ![03](https://i.ibb.co/cKD7Dz1G/03.png) | ![04](https://i.ibb.co/Xf6jJVWr/04.png) |

| Image 5 | Image 6 | Image 7 | Image 8 |
|---------|---------|---------|---------|
| ![05](https://i.ibb.co/2HrxkH4/05.png) | ![06](https://i.ibb.co/KjRdhwfQ/06.png) | ![07](https://i.ibb.co/wrQn13MZ/07.png) | ![08](https://i.ibb.co/prP0XxFK/08.png) |

## 🚀 Getting Started

### Prerequisites

- Node.js 16 or higher
- npm/yarn
- Cloudflare Workers account
- Telegram Bot Token (get it from [@BotFather](https://t.me/botfather))

### Installation

1. Clone the repository:
   ```bash
   git clone https://gitlab.com/fr0stb1rd/group-member-balancer-telegram-bot.git
   cd group-member-balancer-telegram-bot
   npm install
   ```

2. Rename `sample.wrangler.json` to `wrangler.json` and configure it:
    ```json
    {
    "name": "group-member-balancer-telegram-bot",
    "main": "src/index.ts",
    "compatibility_date": "2025-02-04",
    "observability": {
        "enabled": true
    },
    "vars": {
        "TELEGRAM_BOT_TOKEN": "your_bot_token",
        "WEBHOOK_URL": "https://your-worker.workers.dev",
        "LOG_CHANNEL_ID": -100321321,
        "OWNER_ID": 123123,
        "USERS": [
        ]
    },

    "d1_databases": [
        {
        "binding": "DB",
        "database_name": "gmbtb",
        "database_id": "your_database_id"
        }
    ]

    }
    ```

3. Set up secrets:
   ```bash
   wrangler secret put TELEGRAM_BOT_TOKEN
   wrangler secret put LOG_CHANNEL_ID
   wrangler secret put OWNER_ID
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
| `/set`    | Set a group rule                |
| `/unset`  | Remove a rule                   |
| `/list`   | Show all active rules           |
| `/id`     | Show user and chat ID           |
| `/disable`| Disable a rule                  |
| `/enable` | Enable a rule                   |
| `/export` | Export all rules as JSON        |
| `/import` | Import rules from JSON data     |
| `/about`  | About & License & Privacy Policy|
| `/ban`    | Ban a user from using the bot   |
| `/unban`  | Unban a user                    |
| `/promote`| Promote a user to admin         |
| `/demote` | Demote a user from admin        |
| `/adduser`| Add a user to the database      |
| `/deluser`| Remove a user from the database |

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

### `env.USERS` Usage

The `env.USERS` variable is used to specify which users are allowed to interact with the bot. This is useful if you want to make the bot private and restrict its usage to a specific set of users. 

- **Adding Users**: To add users, you need to include their Telegram user IDs in the `USERS` array in the `wrangler.json` file. For example:
  ```json
  "USERS": [123456789, 987654321]
  ```

- **Empty Array**: If you leave the `USERS` array empty, the bot will be public and any user can interact with it.
  ```json
  "USERS": []
  ```

    ### Usage Scenarios:

    1. **Private Bot Mode**:
        - If you want to make the bot private, add your user ID to `env.USERS`.
        - Only the users listed in `env.USERS` will be able to interact with the bot.
        - If a user not listed in `env.USERS` tries to use the bot, they will receive a message saying "⛔️ You are not authorized to use this bot."

    2. **Public Bot Mode**:
        - If `env.USERS` is an empty array or not defined, the bot will be public.
        - Any user will be able to interact with the bot without restrictions.

    3. **Database Check**:
        - If `env.USERS` is defined and not empty, the bot will also check if the user exists in the database.
        - If the user is not found in the database, they will receive a message saying "⛔️ You are not authorized to use this bot."

    4. **Banned Users**:
        - Regardless of the `env.USERS` configuration, the bot will check if the user is banned.
        - If the user is banned, they will receive a message saying "You are banned from using this bot."

    ### Example:

    ```typescript
    const env: Env = {
    TELEGRAM_BOT_TOKEN: 'your-telegram-bot-token',
    WEBHOOK_URL: 'your-webhook-url',
    LOG_CHANNEL_ID: 123456789,
    DB: yourDatabaseInstance,
    OWNER_ID: 987654321,
    USERS: [123456789, 987654321] // Only these users can use the bot
    };
    ```

    In this example, only the users with IDs `123456789` and `987654321` will be able to use the bot.

### Example Commands

- Ban users from another group:
    ```bash
    /set -1001234567890 -1009876543210 ban
    ```

- Kick users from another group:
    ```bash
    /set -1001234567890 -1009876543210 kick
    ```

- Enable a rule:
    ```bash
    /enable -1001234567890 -1009876543210
    ```

- Disable a rule:
    ```bash
    /disable -1001234567890 -1009876543210
    ```

- List all your active rules:
    ```bash
    /list
    ```

- Export your rules as JSON:
    ```bash
    /export
    ```

- Import rules from JSON data:
    ```bash
    /import [{"user_id":12345,"from_group":"-10012345","to_group":"-10054321","action":"kick","enabled":1}]
    ```

- Ban a user from using the bot:
    ```bash
    /ban 123456789
    ```

- Unban a user:
    ```bash
    /unban 123456789
    ```

- Promote a user to admin:
    ```bash
    /promote 123456789
    ```

- Demote a user from admin:
    ```bash
    /demote 123456789
    ```

- Add a user to the database:
    ```bash
    /adduser 123456789
    ```

- Remove a user from the database:
    ```bash
    /deluser 123456789
    ```

## 🏗️ Project Structure

```plaintext
src/
└── index.ts          # Entry point and everything :D
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

#### Rules Table

```sql
CREATE TABLE settings (
    user_id INTEGER,
    from_group TEXT,
    to_group TEXT,
    action TEXT,
    enabled BOOLEAN DEFAULT TRUE,
    PRIMARY KEY (from_group, to_group)
);
```

#### Users Table

```sql
CREATE TABLE users (
    user_id INTEGER PRIMARY KEY,
    is_admin BOOLEAN DEFAULT FALSE,
    is_banned BOOLEAN DEFAULT FALSE
);
```


### Environment Variables

| Variable                  | Description                          |
|---------------------------|--------------------------------------|
| `TELEGRAM_TOKEN`          | Your bot's API token                 |
| `WEBHOOK_URL`             | Your worker's URL                    |
| `LOG_CHANNEL_ID`          | Chat ID for logging                  |
| `OWNER_ID`                | Owner's Telegram user ID             |
| `USERS`                   | List of allowed user IDs             |

## 🔒 Security

- Bot requires admin privileges in both groups
- Only authorized users can manage rules
- Webhook URL is protected with a secret path
- All database operations are parameterized to prevent SQL injection

## 🐛 Troubleshooting

Common issues and solutions:

1. **Bot not responding**
   - Check if bot token is correct
   - Verify webhook is set properly
   - Ensure bot has required permissions

2. **Rule management failure**  
   - Verify bot is admin in both groups.
   - Check if the rule format is correct.
   - Look for errors in worker logs.

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

Project Link: [https://gitlab.com/fr0stb1rd/group-member-balancer-telegram-bot](https://gitlab.com/fr0stb1rd/group-member-balancer-telegram-bot)

## ⚖️ License

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
