---
title: Mastering Torrent Search with qBittorrent and Jackett
published: 2025-04-20
updated: 2025-04-20
description: 'A comprehensive guide on integrating qBittorrent with Jackett for efficient multi-site torrent searching'
image: 'https://i.ibb.co/GftXTxvf/68747470733a2f2f692e696d6775722e636f6d2f75436177674c612e706e67.png'
tags: [qBittorrent, Jackett, Torrent, Tutorial]
category: 'Tutorial'
draft: false
---

## Introduction

This guide will teach you how to use **qBittorrent** and **Jackett** to search for torrents across multiple sites efficiently. Jackett acts as a bridge between qBittorrent and hundreds of torrent indexers, making it easy to find what you need. This guide is for **educational purposes only**.

## What You Need

1. **qBittorrent**: A free and open-source torrent client.
2. **Jackett**: A tool that connects qBittorrent to many torrent sites.
3. A computer with Windows, macOS, or Linux.
4. **.NET Runtime**: Required to run Jackett. Download it from the [official .NET website](https://dotnet.microsoft.com/download).

## Step 1: Install qBittorrent

1. Download qBittorrent from the [official website](https://www.qbittorrent.org/).
2. Install it on your computer by following the instructions.
3. Open qBittorrent and ensure it works.

## Enable the Search Tab in qBittorrent

Before you can use the search feature in qBittorrent, you need to enable the **Search** tab. Follow these steps:

1. Open qBittorrent.
2. Go to the **View** menu in the top bar.
3. Click on **Search Engine** to enable it.
   - If the option is already checked, the **Search** tab should be visible.
4. Once enabled, you will see the **Search** tab appear next to the other tabs (e.g., Transfers, Trackers).

## Install Default Search Plugins in qBittorrent

qBittorrent comes with some default search plugins that can be installed easily. Follow these steps to install or update them:

1. Open qBittorrent.
2. Go to the **Search** tab (enable it from the **View** menu if it's not visible).
3. Click on the **Search plugins…** button in the bottom-right corner.
4. In the new window, click **Check for updates**.
5. qBittorrent will automatically download and install the default search plugins.

For more details, you can visit the [official guide to install search plugins](https://github.com/qbittorrent/search-plugins/wiki/Install-search-plugins).

## Step 2: Install Jackett

1. Download Jackett from the [official website](https://github.com/Jackett/Jackett/releases).
2. Install Jackett on your computer.
3. Open Jackett in your browser. It usually runs at `http://127.0.0.1:9117`.

## Step 3: Add Torrent Sites to Jackett

1. In Jackett, click **Add Indexer**.
2. Search for the torrent sites you want to use (e.g., 1337x, RARBG, etc.).
3. Click **+** to add the site.
4. Follow the instructions to configure the site (some sites may require an account or API key).
5. Test the connection to ensure it works.

## Step 4: Connect Jackett to qBittorrent

1. In Jackett, go to the **API Key** section (top-right corner) and copy your API key.
   ![](https://i.ibb.co/PZWtZ59N/image.png)
2. Open qBittorrent.
3. Go to **Tools > Options > Search**.
4. Install the search plugins if prompted.
5. Add Jackett as a custom search engine:
   - Use Jackett's URL (`http://127.0.0.1:9117`) and your API key.
   - Save the configuration.


## Step 5: Search for Torrents in qBittorrent

1. Open qBittorrent.
2. Go to the **Search** tab (enable it from the **View** menu if hidden).
3. Type what you want to search for (e.g., a movie, TV show, or software).
4. Select the torrent site(s) you added through Jackett.
5. Click **Search** and wait for the results.
6. Double-click a result to start downloading.

## Advanced Configuration (Optional)

If you want to manually configure Jackett in qBittorrent, follow these steps:

1. Download the Jackett plugin file from [this link](https://raw.githubusercontent.com/qbittorrent/search-plugins/master/nova3/engines/jackett.py).
2. In qBittorrent, click **Search plugins…** in the **Search** tab.
3. Select **Install a new one > Web link** and paste the plugin URL.
4. Configure the plugin by creating a `jackett.json` file in the plugin folder:
   - **Windows**: `%LOCALAPPDATA%\qBittorrent\nova3\engines`
   - **Linux**: `~/.local/share/qBittorrent/nova3/engines`
   - **macOS**: `~/Library/Application Support/qBittorrent/nova3/engines`

   Example `jackett.json` file:
   ```json
   {
       "api_key": "YOUR_API_KEY_HERE",
       "url": "http://127.0.0.1:9117",
       "tracker_first": false,
       "thread_count": 20
   }
   ```

For more details, you can visit the [official guide on configuring the Jackett plugin](https://github.com/qbittorrent/search-plugins/wiki/How-to-configure-Jackett-plugin).


## Notes

- Always use a VPN when downloading torrents to protect your privacy.
- Respect copyright laws and only download legal content.

## Conclusion

By combining qBittorrent and Jackett, you can search for torrents across multiple sites directly from qBittorrent. This setup saves time and makes torrenting more efficient. Remember, this guide is for **educational purposes only**. Use it responsibly!
