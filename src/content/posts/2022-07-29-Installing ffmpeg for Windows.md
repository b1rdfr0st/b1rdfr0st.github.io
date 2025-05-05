---
title: Installing FFmpeg on Windows - A Step-by-Step Guide
published: 2022-07-29
updated: 2022-07-29
description: 'A comprehensive guide for installing and setting up FFmpeg multimedia framework on Windows operating system'
image: ''
tags: [FFmpeg, Windows, Tutorial, Multimedia, Software]
category: 'Tutorial'
draft: false
---

## Prerequisites

- Internet connection
- WinRAR or 7z

## Download

You have two option for download (dont download both of them.):
- recommended: [gyan.dev/ffmpeg](https://www.gyan.dev/ffmpeg/builds/)
  - download under `release builds`.
  - your filename be like: `ffmpeg-release-full.7z`
  - ![](https://i.ibb.co/s2sN6Nj/181802510-d4896609-061f-4d25-a592-a3d75824ded2.png)
- other: [BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds/releases/tag/latest)
  - download under `assets`.
  - your filename be like: `ffmpeg-master-latest-win64-gpl.zip`
  - ![](https://i.ibb.co/fCGGKzk/181802306-c1f7f5b2-0feb-4470-bc77-e0df635e5876.png)

## Install

- Open your downloaded file with 7z or winrar
- You will see a folder inside it
- Extract that folder to C:\

## Add To Path

- Go Windows search menu
- Type `Edit the system environment variables` (Turkish: `Sistem ortam değişkenlerini düzenleyin`)
- Navigate to Advanced button and click Environment Variables:
- ![](https://i.ibb.co/2cJC65h/181803861-53e7785f-8dfc-4d64-8132-2cecee9936bc.png)
- Find `Path` and double click:
- ![](https://i.ibb.co/Zh728Bt/181804198-c76f4330-ac0e-4e52-90e5-8c97fd404f8b.png)
- Click `Browse`:
- ![](https://i.ibb.co/nBDQwsX/181804447-783b0ec5-4314-49c8-ba0d-48c10e2190d1.png)
- Select your `bin` folder like this:
- ![](https://i.ibb.co/pvzVqbr/181806118-483c9a19-cebc-4cc1-a512-a305f189b947.png)
- save, save, save, save

> Dont download both of them. You will have only one bin folder.
{: .prompt-danger }

## Usage

- Now open a terminal, type `ffmpeg` and enter.
- You will see a output like this:
- ![](https://i.ibb.co/kQxJC7p/181807579-f0672e0e-39a9-4755-be3b-45d5f5072ca8.png)
- If you dont see this output, it means you did something wrong.
- We installed ffmpeg to windows. If you dont trust links, you can check from [here](https://ffmpeg.org/download.html#build-windows)
