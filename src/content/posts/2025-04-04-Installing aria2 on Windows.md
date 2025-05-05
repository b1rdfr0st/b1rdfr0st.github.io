---
title: Installing aria2 on Windows - A Step-by-Step Guide
published: 2025-04-04
updated: 2025-04-04
description: 'A comprehensive guide for installing and configuring aria2 download manager on Windows systems'
image: ''
tags: [Aria2, Windows, Download, Tutorial]
category: 'Tutorial'
draft: false
---

## Prerequisites

- Internet connection
- WinRAR or 7z

## Download

You have two options for download (don't download both of them):
- recommended: [aria2 GitHub Releases](https://github.com/aria2/aria2/releases)
  - download the latest `.zip` file under `Assets`.
  - your filename will be like: `aria2-*-win-64bit-build1.zip`
  - ![](https://i.ibb.co/qF73zdfR/image.png)
- other: [aria2 SourceForge](https://sourceforge.net/projects/aria2/)
  - download the `.zip` file for Windows.
  - your filename will be like: `aria2-*-win-64bit.zip`
  - ![](https://i.ibb.co/TBBMbMG8/image.png)

## Install

- Open your downloaded file with 7z or WinRAR.
- You will see a folder inside it.
- Extract that folder to `C:\`.

## Add To Path

- Go to the Windows search menu.
- Type `Edit the system environment variables` (Turkish: `Sistem ortam değişkenlerini düzenleyin`).
- Navigate to the Advanced tab and click Environment Variables:
- ![](https://i.ibb.co/2cJC65h/181803861-53e7785f-8dfc-4d64-8132-2cecee9936bc.png)
- Find `Path` and double-click:
- ![](https://i.ibb.co/Zh728Bt/181804198-c76f4330-ac0e-4e52-90e5-8c97fd404f8b.png)
- Click `Browse`:
- ![](https://i.ibb.co/nBDQwsX/181804447-783b0ec5-4314-49c8-ba0d-48c10e2190d1.png)
- Select the folder where `aria2c.exe` is located (e.g., `C:\aria2\`):
- ![](https://i.ibb.co/pvzVqbr/181806118-483c9a19-cebc-4cc1-a512-a305f189b947.png)
- Save, save, save, save.

> Don't download both of them. You will have only one folder containing `aria2c.exe`.
{: .prompt-danger }

## Usage

- Now open a terminal, type `aria2c --version` and press Enter.
- You will see an output.
- If you don't see the output, it means you did something wrong.
- We installed aria2 on Windows. If you don't trust links, you can check from [here](https://aria2.github.io/).
