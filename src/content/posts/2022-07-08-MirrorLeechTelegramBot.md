---
title: MLTB - Mirror Leech Telegram Bot
published: 2022-07-08
updated: 2022-07-08
description: 'A Telegram bot for mirroring files from the internet to Google Drive or Telegram, with support for various file sources'
image: ''
tags: [Telegram, Bot, Python, Torrent, GoogleDrive]
category: 'Project'
draft: false
---

This is a Telegram Bot written in Python for mirroring files on the Internet to your Google Drive or Telegram. Based on [python-aria-mirror-bot](https://github.com/lzzy12/python-aria-mirror-bot) and [mirror-leech-telegram-bot](https://gitlab.com/HuzunluArtemis/QMirrorLeechBot). Written with [python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot) telagram api.

# Features

## From This Repo

- Leech upto 4 GB. You must set [LEECH_LOG](#leech) and [USER_SESSION_STRING](#rss) vars.
- Fully non-credit repo (For protect repo from ban etc.)
- Some more trackers
- Supports all yandex links like yandex.com.tr, yandex.com.ru
- Better YTDL Playlist naming: `"%(playlist_title)s %(playlist_index)s.%(n_entries)s %(title)s.%(ext)s"` Example: `Python Veri İşleme 20.43 Veri Sızıntıları.mp4` 20: video order, 43: playlist length.
- Update all python packages before start bot (optional) Add config `UPDATE_EVERYTHING_WHEN_RESTART` as `True ` Default False.
- Custom finished & unfinished string. (You can get from [1](https://coolsymbol.com/) [2](https://changaco.oy.lc/unicode-progress-bars/) [3](https://text-symbols.com/) or leave empty for default)
- Show thumbnail
- Better file captions. Now writing full path instead of only filename. Before: `Antalya.pdf` After: `Manisa/Antalya.pdf`
- Heroku Usage
- Dyno Restarter / Killer
  - Usage: `/restart dyno`. This will update your bot to latest version, re-set your configs with your new values.
  - Usage: `/restart kill`. This will kill your app for save dyno hours.
- AntiSpam Protections:
  - SpamWatch AntiSpam: Fill `SPAMWATCH_ANTISPAM_API` variable.
  - Combot AntiSpam (CAS): Set `COMBOT_CAS_ANTISPAM` to `True`
  - Userge AntiSpam: Fill `USERGE_ANTISPAM_API` variable.

## From Other Repositories

- Leech-Log, Mirror-Log, Bot-PM
- Force Sub to channel
- AppDrive & GdToT Support
- qBittorrent
- Select files from Torrent before downloading using qbittorrent
- Leech (splitting, thumbnail for each user, setting as document or as media for each user)
- Size limiting for Torrent/Direct, Zip/Unzip, Mega and Clone
- Stop duplicates for all tasks except yt-dlp tasks
- Zip/Unzip G-Drive links
- Counting files/folders from Google Drive link
- View Link button, extra button to open file index link in broswer instead of direct download
- Status Pages for unlimited tasks
- Clone status
- Search in multiple Drive folder/TeamDrive
- Recursive Search (only with `root` or TeamDrive ID, folder ids will be listed with non-recursive method)
- Multi-TD list by token.pickle if exists
- Extract rar, zip and 7z splits with or without password
- Zip file/folder with or without password
- Use Token.pickle if file not found with Service Account for all Gdrive functions
- Random Service Account at startup
- Mirror/Leech/Watch/Clone/Count/Del by reply
- YT-DLP quality buttons
- Search on torrents with Torrent Search API or with variable plugins using qBittorrent search engine
- Docker image support for linux `amd64, arm64, arm/v7, arm/v6, s390x, arm64/v8` (**Note**: Use `412314/mltb:arm64` for `arm64/v8` or oracle)
- Update bot at startup and with restart command using `UPSTREAM_REPO`
- Qbittorrent seed until reaching specific ratio or time
- Rss feed and filter. Based on this repository [rss-chan](https://github.com/hyPnOtICDo0g/rss-chan)
- Save leech settings including thumbnails in database
- Mirror/Leech/Clone multi links/files with one command
- Extenstion Filter for uploading/cloning files
- Incomplete task notifier to get incomplete task messages after restart, works with database.
- Many bugs have been fixed
- Mirror direct download links, Torrent, and Telegram files to Google Drive
- Mirror Mega.nz links to Google Drive
- Copy files from someone's Drive to your Drive (Using Autorclone)
- Download/Upload progress, Speeds and ETAs
- Mirror all yt-dlp supported links
- Docker support
- Uploading to Team Drive
- Index Link support
- Service Account support
- Delete files from Drive
- Shortener support
- Multiple Trackers support
- Shell and Executor
- Add sudo users
- Custom Filename* (Only for direct links, Telegram files and yt-dlp. Not for Mega links, Gdrive links or Torrents)
- Extract password protected files
- Extract these filetypes and uploads to Google Drive
  > ZIP, RAR, TAR, 7z, ISO, WIM, CAB, GZIP, BZIP2, APM, ARJ, CHM, CPIO, CramFS, DEB, DMG, FAT, HFS, LZH, LZMA, LZMA2, MBR, MSI, MSLZ, NSIS, NTFS, RPM, SquashFS, UDF, VHD, XAR, Z, TAR.XZ

- Direct links Supported:
  > letsupload.io, hxfile.co, anonfiles.com, bayfiles.com, antfiles, fembed.com, fembed.net, femax20.com, layarkacaxxi.icu, fcdn.stream, sbplay.org, naniplay.com, naniplay.nanime.in, naniplay.nanime.biz, sbembed.com, streamtape.com, streamsb.net, feurl.com, pixeldrain.com, racaty.net, 1fichier.com, 1drv.ms (Only works for file not folder or business account), uptobox.com (Uptobox account must be premium) and solidfiles.com

# How to deploy?

## Prerequisites

- Tutorial Video from A to Z: [YouTube](https://www.youtube.com/watch?v=gFQWJ4ftt48)

### 1. Installing requirements

- Clone this repo:
```
git clone https://gitlab.com/HuzunluArtemis/MirrorLeechTelegramBot && cd MirrorLeechTelegramBot
```
- For Debian based distros
```
sudo apt install python3 python3-pip
```
Install Docker by following the [official Docker docs](https://docs.docker.com/engine/install/debian/) or by commands below.
```
sudo apt install snapd
sudo snap install docker
```
- For Arch and it's derivatives:
```
sudo pacman -S docker python
```
- Install dependencies for running setup scripts:
```
pip3 install -r requirements-cli.txt
```

### 2. Setting up config file

- ```cp config_sample.env config.env```
- Remove the first line saying:
```_____REMOVE_THIS_LINE_____=True```
- Fill up rest of the fields. Meaning of each field is discussed below:

#### Required Fields

- `BOT_TOKEN`: The Telegram Bot Token that you got from [@BotFather](https://t.me/BotFather)
- `GDRIVE_FOLDER_ID`: This is the Folder/TeamDrive ID of the Google Drive Folder to which you want to upload all the mirrors.
- `OWNER_ID`: The Telegram User ID (not username) of the Owner of the bot. `Int`
- `DOWNLOAD_DIR`: The path to the local folder where the downloads should be downloaded to.
- `DOWNLOAD_STATUS_UPDATE_INTERVAL`: Time in seconds after which the progress/status message will be updated. Recommended `10` seconds at least. `Int`
- `AUTO_DELETE_MESSAGE_DURATION`: Interval of time (in seconds), after which the bot deletes it's message and command message which is expected to be viewed instantly. **NOTE**: Set to `-1` to disable auto message deletion. `Int`
- `IS_TEAM_DRIVE`: Set `True` if uploading to TeamDrive. Default is `False`. `Bool`
- `TELEGRAM_API`: This is to authenticate your Telegram account for downloading Telegram files. You can get this from https://my.telegram.org. `Int`
- `TELEGRAM_HASH`: This is to authenticate your Telegram account for downloading Telegram files. You can get this from https://my.telegram.org.

#### Optional Fields

- `DATABASE_URL`: Your SQL Database URL. Follow this [Generate Database](#generate-database) to generate database. Data will be saved in Database: auth and sudo users, leech settings including thumbnails for each user, rss data and incomplete tasks. **NOTE**: If deploying on heroku and using heroku postgresql delete this variable from **config.env** file. **DATABASE_URL** will be grabbed from heroku variables.
- `AUTHORIZED_CHATS`: Fill user_id and chat_id of groups/users you want to authorize. Separate them by space.
- `SUDO_USERS`: Fill user_id of users whom you want to give sudo permission. Separate them by space.
- `IGNORE_PENDING_REQUESTS`: Ignore pending requests after restart. Default is `False`. `Bool`
- `USE_SERVICE_ACCOUNTS`: Whether to use Service Accounts or not. For this to work see [Using Service Accounts](#using-service-accounts-for-uploading-to-avoid-user-rate-limit) section below. Default is `False`. `Bool`
- `INDEX_URL`: Refer to https://gitlab.com/ParveenBhadooOfficial/Google-Drive-Index.
- `STATUS_LIMIT`: Limit the no. of tasks shown in status message with buttons. **NOTE**: Recommended limit is `4` tasks.
- `STOP_DUPLICATE`: Bot will check file in Drive, if it is present in Drive, downloading or cloning will be stopped. (**NOTE**: File will be checked using filename not file hash, so this feature is not perfect yet). Default is `False`. `Bool`
- `CMD_INDEX`: commands index number. This number will added at the end all commands.
- `UPTOBOX_TOKEN`: Uptobox token to mirror uptobox links. Get it from [Uptobox Premium Account](https://uptobox.com/my_account).
- `TORRENT_TIMEOUT`: Timeout of dead torrents downloading with qBittorrent and Aria2c in seconds.
- `EXTENTION_FILTER`: File extentions that won't upload/clone. Separate them by space.
- `INCOMPLETE_TASK_NOTIFIER`: Get incomplete task messages after restart. Require database and (supergroup or channel). Default is `False`. `Bool`

#### Update

- `UPSTREAM_REPO`: Your github repository link, if your repo is private add `https://username:{githubtoken}@github.com/{username}/{reponame}` format. Get token from [Github settings](https://github.com/settings/tokens). So you can update your bot from filled repository on each restart. **NOTE**: Any change in docker or requirements you need to deploy/build again with updated repo to take effect. DON'T delete .gitignore file. For more information read [THIS](#upstream-repo-recommended).
- `UPSTREAM_BRANCH`: Upstream branch for update. Default is `h-code`.

#### Force SUB

- `FSUB`: Force BOT users to subscribe a specific channel in order to use the bot. Set it `True` if you want to use FSUB. Default is `False`.
- `CHANNEL_USERNAME`: Add the channel username for force sub. (Example: If the channel link is `https://t.me/HuzunluArtemis` then write `HuzunluArtemis`)
- `FSUB_CHANNEL_ID`: Add channel id for `FSUB`. (Ex: `-100123456`). ( **Note** Don't add "" )

#### Mirror

- `MIRROR_LOGS`: Group/Channel ID where Mirror-logs are posted. (Ex: `-100123456`). ( **Note** Don't add "", Simply enter  your userid )

#### Leech

- `BOT_PM`: To send Leeched files and mirrored links in PM, set it `True` (`False` by Default)
- `LEECH_LOG`: Group/Channel ID where Leech-logs are posted. (Ex: `-100123456`). ( **Note** Don't add "", Simply enter  your userid )
- `TG_SPLIT_SIZE`: Size of split in bytes. Default is `2GB`.
- `AS_DOCUMENT`: Default type of Telegram file upload. Default is `False` mean as media. `Bool`
- `EQUAL_SPLITS`: Split files larger than **TG_SPLIT_SIZE** into equal parts size (Not working with zip cmd). Default is `False`. `Bool`
- `CUSTOM_FILENAME`: Add custom word to leeched file name.

#### qBittorrent

- `BASE_URL_OF_BOT`: Valid BASE URL where the bot is deployed to use qbittorrent web selection. Format of URL should be `http://myip`, where `myip` is the IP/Domain(public) of your bot or if you have chosen port other than `80` so write it in this format `http://myip:port` (`http` and not `https`). This Var is optional on VPS and required for Heroku specially to avoid app sleeping/idling. For Heroku fill `https://yourappname.herokuapp.com`. Still got idling? You can use http://cron-job.org to ping your Heroku app.
- `SERVER_PORT`: Only For VPS even if `IS_VPS` is `False`, which is the **BASE_URL_OF_BOT** Port.
- `WEB_PINCODE`: If empty or `False` means no more pincode required while qbit web selection. `Bool`
- `QB_SEED`: QB torrent will be seeded after and while uploading until reaching specific ratio or time, edit `MaxRatio` or `GlobalMaxSeedingMinutes` or both from qbittorrent.conf (`-1` means no limit, but u can cancel manually by gid). **NOTE**: 1. Don't change `MaxRatioAction`, 2. Only works with `/qbmirror` and `/qbzipmirror`. Default is `False`. `Bool`
  - **Qbittorrent NOTE**: If your facing ram exceeded issue then set limit for `MaxConnecs`, decrease `AsyncIOThreadsCount` in qbittorrent config and set limit of `DiskWriteCacheSize` to `32`.

#### RSS

- If you dont want, skip these values. Dont fill.
- `RSS_DELAY`: Time in seconds for rss refresh interval. Recommended `900` second at least. Default is `900` in sec.
- `RSS_COMMAND`: Choose command for the desired action.
- `RSS_CHAT_ID`: Chat ID where rss links will be sent. If using channel then add channel id.
- `USER_SESSION_STRING`: To send rss links from your telegram account instead of adding bot to channel then linking the channel to group to get rss link since bot will not read command from itself or other bot. To generate session string use this command `python3 generate_string_session.py` after mounting repo folder for sure.
  - **RSS NOTE**: `DATABASE_URL` and `RSS_CHAT_ID` is required, otherwise all rss commands will not work. You must use bot in group. You can add the bot to a channel and add link this channel to group so messages sent by bot to channel will be forwarded to group without using `USER_STRING_SESSION`.

#### Private Files

- `ACCOUNTS_ZIP_URL`: Only if you want to load your Service Account externally from an Index Link or by any direct download link NOT webpage link. Archive the accounts folder to ZIP file. Fill this with the direct download link of zip file. If index need authentication so add direct download as shown below:
  - `https://username:password@example.workers.dev/...`
- `TOKEN_PICKLE_URL`: Only if you want to load your **token.pickle** externally from an Index Link. Fill this with the direct link of that file.
- `MULTI_SEARCH_URL`: Check `drive_folder` setup [here](#multi-search-ids). Write **drive_folder** file [here](https://gist.github.com/). Open the raw file of that gist, it's URL will be your required variable. Should be in this form after removing commit id: https://gist.githubusercontent.com/username/gist-id/raw/drive_folder
- `YT_COOKIES_URL`: Youtube authentication cookies. Check setup [here](https://github.com/ytdl-org/youtube-dl#how-do-i-pass-cookies-to-youtube-dl). Use gist raw link and remove commit id from the link, so you can edit it from gists only.
- `NETRC_URL`: To create .netrc file contains authentication for aria2c and yt-dlp. Use gist raw link and remove commit id from the link, so you can edit it from gists only. **NOTE**: After editing .nterc you need to restart the docker or if deployed on heroku so restart dyno in case your edits related to aria2c authentication.
  - **NOTE**: All above url variables used incase you want edit them in future easily without deploying again or if you want to deploy from public fork. If deploying using cli or private fork you can leave these variables empty add token.pickle, accounts folder, drive_folder, .netrc and cookies.txt directly to root but you can't update them without rebuild OR simply leave all above variables and use private UPSTREAM_REPO.

#### MEGA

- `MEGA_API_KEY`: Mega.nz API key to mirror mega.nz links. Get it from [Mega SDK Page](https://mega.nz/sdk)
- `MEGA_EMAIL_ID`: E-Mail ID used to sign up on mega.nz for using premium account.
- `MEGA_PASSWORD`: Password for mega.nz account.

#### Shortener

- `SHORTENER_API`: Fill your Shortener API key.
- `SHORTENER`: Shortener URL.
  - Supported URL Shorteners:
  >exe.io, gplinks.in, shrinkme.io, urlshortx.com, shortzon.com, bit.ly, shorte.st, linkvertise.com , ouo.io, adfoc.us, cutt.ly

#### GDTOT

- `CRYPT`: Cookie for gdtot google drive link generator. Follow these [steps](#gdtot-cookies).

#### AppDrive
- `APPDRIVE_EMAIL` = Fill your AppDrive Email address.
- `APPDRIVE_PASS` = AppDrive Password for login.

#### Size Limits

- `TORRENT_DIRECT_LIMIT`: To limit the Torrent/Direct mirror size. Don't add unit. Default unit is `GB`.
- `ZIP_UNZIP_LIMIT`: To limit the size of zip and unzip commands. Don't add unit. Default unit is `GB`.
- `CLONE_LIMIT`: To limit the size of Google Drive folder/file which you can clone. Don't add unit. Default unit is `GB`.
- `MEGA_LIMIT`: To limit the size of Mega download. Don't add unit. Default unit is `GB`.
- `STORAGE_THRESHOLD`: To leave specific storage free and any download will lead to leave free storage less than this value will be cancelled. Don't add unit. Default unit is `GB`.

#### Buttons

- `VIEW_LINK`: View Link button to open file Index Link in browser instead of direct download link, you can figure out if it's compatible with your Index code or not, open any video from you Index and check if its URL ends with `?a=view`, if yes make it `True`, compatible with [BhadooIndex](https://gitlab.com/ParveenBhadooOfficial/Google-Drive-Index) Code. Default is `False`. `Bool`

- Three buttons are already added including Drive Link, Index Link, and View Link, you can add extra buttons, if you don't know what are the below entries, simply leave them empty.
  - `BUTTON_FOUR_NAME`:
  - `BUTTON_FOUR_URL`:
  - `BUTTON_FIVE_NAME`:
  - `BUTTON_FIVE_URL`:
  - `BUTTON_SIX_NAME`:
  - `BUTTON_SIX_URL`:

#### Torrent Search

- `SEARCH_API_LINK`: Search api app link. Get your api from deploying this [repository](https://github.com/Ryuk-me/Torrent-Api-py).
  - Supported Sites:
  >1337x, Piratebay, Nyaasi, Torlock, Torrent Galaxy, Zooqle, Kickass, Bitsearch, MagnetDL, Libgen, YTS, Limetorrent, TorrentFunk, Glodls, TorrentProject and YourBittorrent
- `SEARCH_LIMIT`: Search limit for search api, limit for each site and not overall result limit. Default is zero (Default api limit for each site).
- `SEARCH_PLUGINS`: List of qBittorrent search plugins (github raw links). I have added some plugins, you can remove/add plugins as you want. Main Source: [qBittorrent Search Plugins (Official/Unofficial)](https://github.com/qbittorrent/search-plugins/wiki/Unofficial-search-plugins).

### 3. Getting Google OAuth API credential file and token.pickle

- Old authentication changed, now we can't use bot or replit to generate token.pickle. You need OS with a browser.
- Windows users should install python3 and pip. You can find how to install and use them from google or from this [telegraph](https://telegra.ph/Create-Telegram-Mirror-Leech-Bot-by-Deploying-App-with-Heroku-Branch-using-Github-Workflow-12-06) from [Wiszky](https://github.com/vishnoe115) tutorial.
- You can ONLY open the generated link from `generate_drive_token.py` in local browser.

1. Visit the [Google Cloud Console](https://console.developers.google.com/apis/credentials)
2. Go to the OAuth Consent tab, fill it, and save.
3. Go to the Credentials tab and click Create Credentials -> OAuth Client ID
4. Choose Desktop and Create.
5. Publish your OAuth consent screen App to prevent **token.pickle** from expire
6. Use the download button to download your credentials.
7. Move that file to the root of mirrorbot, and rename it to **credentials.json**
8. Visit [Google API page](https://console.developers.google.com/apis/library)
9. Search for Google Drive Api and enable it
10. Finally, run the script to generate **token.pickle** file for Google Drive:
```
pip3 install google-api-python-client google-auth-httplib2 google-auth-oauthlib
python3 generate_drive_token.py
```

## Deploying on VPS

1. You must set `SERVER_PORT` variable to `80` or any other port you want to use.
2. To clear the container (this will not affect on the image):
```
sudo docker container prune
```
3. To delete the images:
```
sudo docker image prune -a
```
4. Check the number of processing units of your machine with `nproc` cmd and times it by 4, then edit `AsyncIOThreadsCount` in qBittorrent.conf.
5. Use `anasty17/mltb:arm64` for oracle or arm64/v8.
   - Tutorial Video for Deploying on Oracle VPS:
     - Thanks to [Wiszky](https://github.com/vishnoe115)
     - No need to use sudo su, you can also use sudo before each cmd!
6. Tutorial is [here](https://youtu.be/IzUG7U7v4U4?t=968)

### Deploying on VPS Using Docker

- Start Docker daemon (skip if already running), if installed by snap then use 2nd command:
```
sudo dockerd
```
```
sudo snap start docker
```
- **Note**: If not started or not starting, run the command below then try to start.
```
sudo apt install docker.io
```
- Build Docker image:
```
sudo docker build . -t MirrorLeechTelegramBot
```
- Run the image:
```
sudo docker run -p 80:80 MirrorLeechTelegramBot
```
- To stop the image:
```
sudo docker ps
```
```
sudo docker stop id
```

### Deploying on VPS Using docker-compose

**NOTE**: If you want to use port other than 80, change it in [docker-compose.yml](https://gitlab.com/huzunluartemis/MirrorLeechTelegramBot/-/blob/h-code/docker-compose.yml) also.

```
sudo apt install docker-compose
```
- Build and run Docker image:
```
sudo docker-compose up
```
- After editing files with nano for example (nano start.sh):
```
sudo docker-compose up --build
```
- To stop the image:
```
sudo docker-compose stop
```
- To run the image:
```
sudo docker-compose start
```
- Tutorial [video](https://youtu.be/c8_TU1sPK08) from Tortoolkit repo for docker-compose and checking ports

## Heroku Deploy

1. Generate all your private files from h-code branch (token.pickle, config.env, drive_folder, cookies.txt etc...) since the generators not available in heroku branch but you should add the private files in heroku branch not in h-code or use variables links in `config.env`.
2. Don't add variables in heroku Environment, you can only add `CONFIG_FILE_URL`.
3. Don't deploy using hmanager or github integration.
4. This branch use megasdkrest and latest version of qBittorrent.
5. More notes will be added soon for h-code branch...

### Deploy With CLI

- Clone this repo:
```
git clone https://gitlab.com/HuzunluArtemis/MirrorLeechTelegramBot && cd MirrorLeechTelegramBot
```
- Switch to heroku branch
  - **NOTE**: Don't commit changes in h-code branch. If you have committed your changes in h-code branch and after that you switched to heroku branch, the new added files(private files) will `NOT` appear in heroku branch.
```
git checkout heroku
```
- After adding your private files
```
git add . -f
```
- Commit your changes
```
git commit -m token
```
- Login to heroku
```
heroku login
```
- Create heroku app
```
heroku create --region us YOURAPPNAME
```
- Add remote
```
heroku git:remote -a YOURAPPNAME
```
- Create container
```
heroku stack:set container
```
- Push to heroku
```
git push heroku heroku:h-code -f
```

### Extras

- To create heroku-postgresql database
```
heroku addons:create heroku-postgresql
```
- To delete the app
```
heroku apps:destroy YOURAPPNAME
```
- To restart dyno
```
heroku restart
```
- To turn off dyno
```
heroku ps:scale web=0
```
- To turn on dyno
```
heroku ps:scale web=1
```
- To set heroku variable
```
heroku config:set VARNAME=VARTEXT
```
- To get live logs
```
heroku logs -t
```

## Deploy With Github Workflow

1. Go to Repository Settings -> Secrets

![Secrets](https://telegra.ph/file/9d6ed26f8981c2d2f226c.jpg)

2. Add the below Required Variables one by one by clicking New Repository Secret every time.

   - HEROKU_EMAIL: Heroku Account Email Id in which the above app will be deployed
   - HEROKU_API_KEY: Your Heroku API key, get it from https://dashboard.heroku.com/account
   - HEROKU_APP_NAME: Your Heroku app name, Name Must be unique
   - CONFIG_FILE_URL: Copy [this](https://gitlab.com/huzunluartemis/MirrorLeechTelegramBot/-/raw/h-code/config_sample.env) in any text editor.Remove the _____REMOVE_THIS_LINE_____=True line and fill the variables. For details about config you can see Here. Go to https://gist.github.com and paste your config data. Rename the file to config.env then create secret gist. Click on Raw, copy the link. This will be your CONFIG_FILE_URL. Refer to below images for clarity.

![Steps from 1 to 3](https://telegra.ph/file/2a27cf34dc0bdba885de9.jpg)

![Step 4](https://telegra.ph/file/fb3b92a1d2c3c1b612ad0.jpg)

![Step 5](https://telegra.ph/file/f0b208e4ea980b575dbe2.jpg)

3. Remove commit id from raw link to be able to change variables without updating the CONFIG_FILE_URL in secrets. Should be in this form: https://gist.githubusercontent.com/username/gist-id/raw/config.env
   - Before: https://gist.githubusercontent.com/HuzunluArtemis/8cce4a4b4e7f4ea47e948b2d058e52ac/raw/19ba5ab5eb43016422193319f28bc3c7dfb60f25/config.env
   - After: https://gist.githubusercontent.com/HuzunluArtemis/8cce4a4b4e7f4ea47e948b2d058e52ac/raw/config.env

4. Add all your private files in this branch or use variables links in `config.env`.

5. After adding all the above Required Variables go to Github Actions tab in your repository.
   - Select Manually Deploy to Heroku workflow as shown below:

![Select Manual Deploy](https://telegra.ph/file/cff1c24de42c271b23239.jpg)

6. Choose `heroku` branch and click on Run workflow

![Run Workflow](https://telegra.ph/file/f44c7465d58f9f046328b.png)

## Bot commands to be set in [@BotFather](https://t.me/BotFather)

```
start - Auth Stats
mirror - Mirror
zipmirror - Mirror and upload as zip
unzipmirror - Mirror and extract files
qbmirror - Mirror torrent using qBittorrent
qbzipmirror - Mirror torrent and upload as zip using qb
qbunzipmirror - Mirror torrent and extract files using qb
leech - Leech
zipleech - Leech and upload as zip
unzipleech - Leech and extract files
qbleech - Leech torrent using qBittorrent
qbzipleech - Leech torrent and upload as zip using qb
qbunzipleech - Leech torrent and extract using qb
clone - Copy file/folder to Drive
count - Count file/folder of Drive
watch - Mirror yt-dlp supported link
zipwatch - Mirror yt-dlp supported link as zip
leechwatch - Leech through yt-dlp supported link
leechzipwatch - Leech yt-dlp support link as zip
leechset - Leech settings
setthumb - Set thumbnail
status - Get Mirror Status message
rsslist - List all subscribed rss feed info
rssget - Get specific No. of links from specific rss feed
rsssub - Subscribe new rss feed
rssunsub - Unsubscribe rss feed by title
rssset - Rss Settings
list - Search files in Drive
search - Search for torrents with API
cancel - Cancel a task
cancelall - Cancel all tasks
del - Delete file/folder from Drive
log - Get the Bot Log
shell - Run commands in Shell
restart - Restart the Bot [Kill / Dyno]
stats - Bot Usage Stats
ping - Ping the Bot
help - All cmds with description
```

## UPSTREAM REPO (Recommended)

- `UPSTREAM_REPO` variable can be used for edit/add any file in repository.
- You can add private/public repository link to grab/overwrite all files from it.
- You can skip adding the privates files like token.pickle or accounts folder before deploying, also no need to add variables direct links except **config.env**, simply fill `UPSTREAM_REPO` private one in case you want to grab all files including private files.
- If you added private files while deploying and you have added private `UPSTREAM_REPO` and your private files in this private repository, so your private files will be overwritten from this repository. Also if you are using URL variables like `TOKEN_PICKLE_URL` then all files from those variables will override the private files that added before deploying or from private `UPSTREAM_REPO`.
- If you filled `UPSTREAM_REPO` with the official repository link then be carefull incase any change in requirements.txt your bot will not start after restart. In this case you need to deploy again with updated code to install the new requirements or simply by changing the `UPSTREAM_REPO` to you fork link with that old updates or make it empty if deployed h-code branch.
- In case you you filled `UPSTREAM_REPO` with your fork link be carefull also if you fetched the commits from the official repository.
- The changes in your `UPSTREAM_REPO` will take affect only after restart.
- `UPSTREAM_BRANCH` don't ever fill heroku here.

## Using Service Accounts for uploading to avoid user rate limit
>For Service Account to work, you must set `USE_SERVICE_ACCOUNTS` = "True" in config file or environment variables.
>**NOTE**: Using Service Accounts is only recommended while uploading to a Team Drive.

### 1. Generate Service Accounts. [What is Service Account?](https://cloud.google.com/iam/docs/service-accounts)
Let us create only the Service Accounts that we need.

**Warning**: Abuse of this feature is not the aim of this project and we do **NOT** recommend that you make a lot of projects, just one project and 100 SAs allow you plenty of use, its also possible that over abuse might get your projects banned by Google.

>**NOTE**: If you have created SAs in past from this script, you can also just re download the keys by running:
```
python3 gen_sa_accounts.py --download-keys $PROJECTID
```
>**NOTE:** 1 Service Account can upload/copy around 750 GB a day, 1 project can make 100 Service Accounts so you can upload 75 TB a day or clone 2 TB from each file creator (uploader email).

#### Two methods to create service accounts
Choose one of these methods

##### 1. Create Service Accounts in existed Project (Recommended Method)
- List your projects ids
```
python3 gen_sa_accounts.py --list-projects
```
- Enable services automatically by this command
```
python3 gen_sa_accounts.py --enable-services $PROJECTID
```
- Create Sevice Accounts to current project
```
python3 gen_sa_accounts.py --create-sas $PROJECTID
```
- Download Sevice Accounts as accounts folder
```
python3 gen_sa_accounts.py --download-keys $PROJECTID
```

##### 2. Create Service Accounts in New Project
```
python3 gen_sa_accounts.py --quick-setup 1 --new-only
```
A folder named accounts will be created which will contain keys for the Service Accounts.

### 2. Add Service Accounts

#### Two methods to add service accounts
Choose one of these methods

##### 1. Add Them To Google Group then to Team Drive (Recommended)
- Mount accounts folder
```
cd accounts
```
- Grab emails form all accounts to emails.txt file that would be created in accounts folder
- `For Windows using PowerShell`
```
$emails = Get-ChildItem .\**.json |Get-Content -Raw |ConvertFrom-Json |Select -ExpandProperty client_email >>emails.txt
```
- `For Linux`
```
grep -oPh '"client_email": "\K[^"]+' *.json > emails.txt
```
- Unmount acounts folder
```
cd ..
```
Then add emails from emails.txt to Google Group, after that add this Google Group to your Shared Drive and promote it to manager and delete email.txt file from accounts folder

##### 2. Add Them To Team Drive Directly
- Run:
```
python3 add_to_team_drive.py -d SharedTeamDriveSrcID
```

### Generate Database

1. Using Railway
    - Go to [railway](https://railway.app) and create account
    - Start new project
    - Press on `Provision PostgreSQL`
    - After creating database press on `PostgresSQL`
    - Go to `Connect` column
    - Copy `Postgres Connection URL` and fill `DATABASE_URL` variable with it

2. [Using Heroku PostgreSQL](https://dev.to/prisma/how-to-setup-a-free-postgresql-database-on-heroku-1dc1)

3. Using ElephantSQL (Recommended)
    - Go to [elephantsql](https://elephantsql.com) and create account
    - Hit `Create New Instance`
    - Follow the further instructions in the screen
    - Hit `Select Region`
    - Hit `Review`
    - Hit `Create instance`
    - Select your database name
    - Copy your database url, and fill `DATABASE_URL` variable with it

## Multi Search IDs
To use list from multi TD/folder. Run driveid.py in your terminal and follow it. It will generate **drive_folder** file or u can simply create `drive_folder` file in working directory and fill it, check below format:
```
MyTdName folderID/tdID IndexLink(if available)
MyTdName2 folderID/tdID IndexLink(if available)
```

## Yt-dlp and Aria2c Authentication Using .netrc File
For using your premium accounts in yt-dlp or for protected Index Links, create .netrc file according to following format:

**Note**: Create .netrc and not netrc, this file will be hidden, so view hidden files to edit it after creation.

Format:
```
machine host login username password my_password
```
Example:
```
machine instagram login HuzunluArtemis password mypassword
```
**Instagram Note**: You must login even if you want to download public posts and after first try you must confirm that this was you logged in from different ip(you can confirm from phone app).

**Youtube Note**: For `youtube` authentication use [cookies.txt](https://github.com/ytdl-org/youtube-dl#how-do-i-pass-cookies-to-youtube-dl) file.

Using Aria2c you can also use built in feature from bot with or without username. Here example for index link without username.
```
machine example.workers.dev password index_password
```
Where host is the name of extractor (eg. instagram, Twitch). Multiple accounts of different hosts can be added each separated by a new line.

## Gdtot Cookies
To Clone or Leech gdtot link follow these steps:
1. Login/Register to [gdtot](https://new.gdtot.top).
2. Copy this script and paste it in browser address bar.
   - **Note**: After pasting it check at the beginning of the script in broswer address bar if `javascript:` exists or not, if not so write it as shown below.
   ```javascript
   javascript:(function () {
    const input = document.createElement('input');
    COOKIE = JSON.parse(JSON.stringify({cookie : document.cookie}));
    input.value = COOKIE['cookie'].split('crypt=')[1];
    document.body.appendChild(input);
    input.focus();
    input.select();
    var result = document.execCommand('copy');
    document.body.removeChild(input);
     if(result)
       alert('Crypt copied to clipboard');
     else
       prompt('Failed to copy Crypt. Manually copy below Crypt\n\n', input.value);
   })();
   ```
   - After pressing enter your browser will prompt a alert.
3. Now you'll get Crypt value in your clipboard
   ```
   NGxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxWdSVT0%3D
   ```
4. From this you have to paste value for **CRYPT** in config.env file.

# Lisans

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
