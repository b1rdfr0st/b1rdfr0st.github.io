---
title: FBICompress - Compress Images Without Limits on Compressor.io
published: 2025-02-23
updated: 2025-02-23
description: 'A tool for unlimited image compression using compressor.io with Cloudflare bypass and proxy support'
image: ''
tags: [Compression, ImageProcessing, Cloudflare, Python, Proxy]
category: 'Project'
draft: false
---

**FBICompress** is a powerful image compression tool that utilizes [compressor.io](https://compressor.io) to reduce image sizes while maintaining quality. It supports **JPG, JPEG, PNG, GIF, and WEBP** formats. The script leverages **cloudscraper** to bypass Cloudflare protection and requires **valid proxies** to avoid rate limits. [Blog Post](https://fr0stb1rd.gitlab.io/posts/FBICompress/) \| [Source Code](https://gitlab.com/fr0stb1rd/fbicompress) \| [Türkçe](https://gitlab.com/fr0stb1rd/fbicompress/-/blob/master/README.TR.md)

## ✨ Features  
✅ Compress entire image folders  
✅ Supports **lossy** and **lossless** compression  
✅ Automatically fetches and verifies proxies  
✅ Option to overwrite original images  
✅ **Bypasses compressor.io limitations**  

## 🛡️ Bypassing Restrictions  
By default, **compressor.io** enforces:  
- **50 images per day limit**  
- **Maximum 10 images per batch**  

**FBICompress** bypasses these restrictions by:  
- **Rotating proxies** to prevent detection  
- **Utilizing multiple concurrent threads**  
- **Using Cloudscraper** to evade Cloudflare protection  

This exploit takes advantage of a **cybersecurity vulnerability** in the platform’s rate-limiting system.  

⚠ **This may violate compressor.io’s Terms of Service. Use responsibly!**  

## 🔧 Requirements
- **Python 3.6+**  
- **Cloudscraper library** (`pip install cloudscraper`)  
- **Active internet connection**  

## ⚙️ Installation
1. Install **Python 3.6+**  
2. Install required dependencies:  
   ```bash
   pip install cloudscraper
   ```
3. Download and run the script.  

## 🚀 Usage
Basic compression:  
```bash
python FBICompress.py /path/to/images
```
Lossless compression:  
```bash
python FBICompress.py /path/to/images -t lossless
```
Save compressed images in a different directory:  
```bash
python FBICompress.py /path/to/images -o /path/to/compressed
```
Overwrite original images:  
```bash
python FBICompress.py /path/to/images -o /path/to/images --overwrite
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## ⚠️ Disclaimer

This project is not affiliated with [compressor.io](https://compressor.io). Use at your own risk and responsibility. 

I am not responsible for any issues, damages, or consequences that may arise from using this project. By using this program, you agree to do so at your own discretion.

## 📧 Contact

Made with ❤️ by [@fr0stb1rd](https://t.me/fr0stb1rd)

Project Link: [https://gitlab.com/fr0stb1rd/FBICompress](https://gitlab.com/fr0stb1rd/fbicompress)

## ⚖️ License

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
