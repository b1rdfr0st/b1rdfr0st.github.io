---
title: Setting Up PHP Development Environment with VSCode on Linux
published: 2024-06-04
updated: 2024-06-04
description: 'A step-by-step guide for setting up a PHP development environment using Visual Studio Code on Linux systems'
image: ''
tags: [PHP, Linux, VSCode, Development, Tutorial]
category: 'Tutorial'
draft: false
---

## Prerequisites

- Internet connection
- Linux

## Setup

- Download and install VSCode from [here](https://code.visualstudio.com/download)
- Install php with: `apt install php php-cli php-cgi`
- Go to VSCode Settings
- Make this settings:
    ![](https://i.ibb.co/tZQc3rt/image.png)
    - add this line like photo: `"php.validate.executablePath": "/usr/bin/php"`
- Install Extensions:
    - `Ctrl+P`
    - `ext install bmewburn.vscode-intelephense-client` ([PHP Intelephense](https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client))
    - `ext install brapifra.phpserver` ([PHP Server](https://marketplace.visualstudio.com/items?itemName=brapifra.phpserver))
- Restart VSCode
- Create an index.php file, right click an you can see `PHP: Serve Project` and `PHP Server: Stop Serve`
    ![](https://i.ibb.co/9h0V228/image.png)
- Open browser and go to `localhost`
