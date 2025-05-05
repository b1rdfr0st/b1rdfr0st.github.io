---
title: Text-to-Picture Telegram Bot (TTPTB)
published: 2025-03-20
updated: 2025-03-20
description: 'A serverless Telegram bot for generating images from text using multiple AI models like SDXL, Lightning, and Dreamshaper'
image: ''
tags: [Telegram, Bot, TypeScript, Cloudflare, Workers, AI, ImageGeneration]
category: 'Project'
draft: false
---

A powerful Telegram bot built on Cloudflare Workers that generates images from text descriptions using multiple AI models. The bot supports various state-of-the-art image generation models and provides a user-friendly interface for creating stunning visuals from text prompts. [Blog Post](https://fr0stb1rd.gitlab.io/posts/Text-To-Picture-Telegram-Bot/) \| [Live Bot](https://t.me/text_to_picture_robot)

## ✨ Features

- 🎨 Multiple AI models support (SDXL, Lightning, Dreamshaper, etc.)
- 🚀 Fast image generation with Cloudflare Workers
- 🌍 Multi-language support (English and Turkish)
- 💾 User preferences persistence
- ⚡ High-performance image processing
- 🆓 Runs within Cloudflare's free tier limits

## 🛠️ Technology Stack

- **TypeScript**
- **Cloudflare Workers**
- **Cloudflare AI** (Multiple AI Models)
- **Telegram Bot API**
- **Workers KV** for user preferences

## 📸 Screenshots

| Image 1 | Image 2 | Image 3 | Image 4 |
|---------|---------|---------|---------|
| ![1](https://i.ibb.co/39nCXwzG/1.png) | ![2](https://i.ibb.co/fVQ7N1bZ/2.png) | ![3](https://i.ibb.co/RGVjhx6w/3.png) | ![4](https://i.ibb.co/MDt121Bm/4.png) |

| Image 5 | Image 6 | Image 7 | Image 8 |
|---------|---------|---------|---------|
| ![5](https://i.ibb.co/PGqz6nbT/5.png) | ![6](https://i.ibb.co/0jShgmGd/6.png) | ![7](https://i.ibb.co/C3dfXpWt/7.png) | ![8](https://i.ibb.co/MyYPBpF9/8.png) |

## 📝 Usage

### Bot Commands

| Command        | Description                          |
|---------------|--------------------------------------|
| `/start`      | Start the bot and show help          |
| `/help`       | Show help message                    |
| `/draw`       | Generate an image from text          |
| `/setmodel`   | Change the AI model                  |
| `/currentmodel`| Show current active model           |
| `/about`      | Show information about the bot       |

### Available AI Models

- `sdxl` - Stable Diffusion XL (Default)
- `lightning` - SDXL Lightning (Faster)
- `dreamshaper` - Dreamshaper 8 LCM (Creative)
- `flux` - FLUX.1 Schnell (Modern)
- `inpainting` - SD v1.5 Inpainting
- `img2img` - SD v1.5 Image to Image

### Example Commands

- Generate an image:
    ```
    /draw a futuristic cityscape with flying cars and neon lights
    ```

- Change AI model:
    ```
    /setmodel lightning
    ```

- Check current model:
    ```
    /currentmodel
    ```

## 🔒 Security

- Webhook URL is protected
- User preferences are securely stored in Workers KV
- All API operations are properly authenticated
- Error logging system for monitoring

## 🐛 Troubleshooting

Common issues and solutions:

1. **Image Generation Fails**
   - Check if the prompt is in English
   - Verify AI model availability
   - Check for any error messages

2. **Bot Not Responding**
   - Verify bot token is correct
   - Check webhook configuration
   - Ensure worker is deployed properly

## ⚠️ Disclaimer

This bot is not affiliated with Telegram or any of the AI model providers. Use at your own risk and responsibility.

I am not responsible for any issues, damages, or consequences that may arise from using this bot. By using this bot, you agree to do so at your own discretion.

## 📧 Contact

Made with ❤️ by [@fr0stb1rd](https://t.me/fr0stb1rd)

## ⚖️ License

This project is proprietary and confidential. Unauthorized copying, distribution, or modification of any part of this codebase is strictly prohibited. Access to the source code is restricted to authorized personnel only.
