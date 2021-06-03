# Salty Chat FAQ

## Table of Content

- [Where can I download an old version?](#where-can-i-download-an-old-version)
- [How to enable debug logging?](#how-to-enable-debug-logging)
- [My teamspeak crashs](#my-teamspeak-crashs)
- [Installation of Salty Chat is corrupt](#installation-of-salty-chat-is-corrupt)
- [*.ts3_plugin is unknown file / opened in wrong program](#ts3_plugin-is-unknown-file)
- [FiveM: Connection Timeout](#fivem-connection-timeout)
- [FiveM: I don't hear people ingame](#fivem-i-dont-hear-people-ingame)

## Where can I download an old version?

You don't need to download an old version. All 2.X.X versions are full compatible. If you have any problems, follow the steps below:

- If your TeamSpeak crashs, read chapter [My teamspeak crashs](#my-teamspeak-crashs)
- If you are using FiveM and your connection timeouts, read chapter [FiveM: Connection Timeout](#fivem-connection-timeout)
- If you are using FiveM and you don't hear people ingame, rad chapter [FiveM: I don't hear people ingame](#fivem-i-dont-hear-people-ingame)

## How to enable debug logging?

1. Open your TeamSpeak client
2. Go to `Plugins > Salty Chat > Open Settings`
3. Enable `Expert Mode`
4. Select `Extensive` for `Log Level`
**Don't enable ExtensiveDebug until further instructions, because this will result in a huge log file.**

## My teamspeak crashs

If your TeamSpeak crashs, update Salty Chat to version 2.3.3 or higher. If your TeamSpeak crashs with version 2.3.3 or higher, follow the steps below:

1. Follow the steps in chapter [How to enable debug logging?](#how-to-enable-debug-logging), except activating `ExtensiveDebug` instead `Extensive` for `Log Level`
2. Start your game and try to reproduce to crash TeamSpeaks.
3. Send us the newest crashdump (you can find it under `%appdata%\TS3Client\crashdumps`) in the Salty Chat Discord.
    - If there is no crashdump, send us the newest log (you can find it under `%appdata%\TS3Client\logs`)
4. Provide us informations to reproduce the crash.

## Installation of Salty Chat is corrupt

If you have the following error, follow the steps below:

![Installation of Salty Chat is corrupt](https://github.com/saltminede/saltychat-faq/raw/main/media/setup-installation-corrupt.png)

### Solution A

If you updated Salty Chat from a version prior or equal to 2.1.2, you may not have uninstalled Salty Chat before installing the new version:

1. Close TeamSpeak
2. Delete the files `%AppData%\TS3Client\plugins\SaltyChat.dll` and `%AppData%\TS3Client\plugins\VoiceDistortion.dll`
3. Install the latest Salty Chat release

### Solution B

Install the latest Visual C++ Redistributable:
- x86: https://aka.ms/vs/16/release/vc_redist.x86.exe
- x64: https://aka.ms/vs/16/release/vc_redist.x64.exe

### Solution C

If this does not help, follow the steps below:

1. Unzip the plugin.
2. Copy the unzipped files.
3. Go to `%appdata%\TS3Client\plugins` and paste the files.

This is explained in more detail in the chapter [*.ts3_plugin is unknown file / opened in wrong program](#ts3_plugin-is-unknown-file).

## *.ts3_plugin is unknown file

If you can't open the `*.ts3_plugin` file with double click, follow the steps below:

1. Go to `C:\Program Files\TeamSpeak 3 Client` (or where you TeamSpeak is installed).
2. Run `createfileassoc.exe` as administrator.

If this does not help, follow the steps below:

1. Close TeamSpeak.
2. Download the plugin.
3. Unzip the `*.ts3_plugin` (e.g. with 7-Zip or WinRaR)
4. Go to the extracted directory. There should be a directory named `plugin`.
5. Copy the content of the directory `plugin`.
6. Go to %appdata%\TS3Client\plugins. Paste the copied files.
7. Start TeamSpeak. If the plugin is not enabled you can enable it in the options of your teamspeak.

## FiveM: Connection Timeout

In FiveM websocket connections to `127.0.0.1` and `localhost` are blocked. So we had to use a workaround. Make sure that you can resolve `lh.saltmine.de`. Follw the steps below:

1. Open Windows Command Prompt by searching `cmd`
2. Execute `nslookup lh.saltmine.de`

If it resolved to `127.0.0.1`, follow the steps in chapter [How to enable debug logging?](#how-to-enable-debug-logging) and send us the newest log (you can find it under `%appdata%\TS3Client\logs`) in Salty Chat Discord. If it not resolved to `127.0.0.1`, try to use a alternative DNS server (e.g. Google DNS or Cloudflare DNS).

- Google DNS server: https://developers.google.com/speed/public-dns/docs/using#addresses
- Cloudflare DNS server: https://developers.cloudflare.com/1.1.1.1/setting-up-1.1.1.1/windows
- How to setup DNS server on Windows 10: https://www.privateinternetaccess.com/blog/changing-your-dns-settings-on-windows-10/

Note: If you have an IPv6 address, keep in mind to also change the DNS server for IPv6.

## FiveM: I don't hear people ingame

Check if OneSync is enabled on your server and your artifacts are up-to-date. If this does not help, follow the steps in chapter [How to enable debug logging?](#how-to-enable-debug-logging) and send us the newest log (you can find it under `%appdata%\TS3Client\logs`) in Salty Chat Discord.
