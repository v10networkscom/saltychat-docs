# Salty Chat FAQ

## Table of Content

- [Where can I download an old version?](#where-can-i-download-an-old-version)
- [How to enable extensive logging?](#how-to-enable-extensive-logging)
- [My teamspeak crashs](#my-teamspeak-crashs)
- [Installation of Salty Chat is corrupt](#installation-of-salty-chat-is-corrupt)
- [*.ts3_plugin is unknown file / opened in wrong program](#ts3_plugin-is-unknown-file)
- [FiveM/RedM/LibertyM: NUI stuck at "Connecting..."](#fivem-nui-stuck-at-connecting) 

## Where can I download an old version?

Before downloading an older version, take a look at the [versioning scheme](https://github.com/saltminede/saltychat-docs#versioning-and-update-branches) to see if it's compatible with the servers script version.

The download of older versions is available at the following address: `https://www.saltmine.de/saltychat/download/x.x.x`, where **x.x.x** must be replaced with the required version.
For example, the link for Salty Chat 2.3.3 is `https://www.saltmine.de/saltychat/download/2.3.3`.
There is no guaranteed availability or support for older versions.

## How to enable extensive logging?

1. Open your TeamSpeak client
2. Go to `Plugins > Salty Chat > Open Settings`
3. Enable `Expert Mode`
4. Select `Extensive` for `Log Level`
**Don't enable ExtensiveDebug until further instructions, because this will result in a huge log file.**

## My teamspeak crashs

If your TeamSpeak crashs, update Salty Chat to the latest version. If your TeamSpeak still crashs, follow the steps below:

1. Follow the steps in chapter [How to enable extensive logging?](#how-to-enable-extensive-logging), except activating `ExtensiveDebug` instead `Extensive` for `Log Level`
2. Start your game and try to reproduce to crash TeamSpeaks.
3. Send us the newest crashdump (you can find it under `%appdata%\TS3Client\crashdumps`) in the Salty Chat Discord.
    - If there is no crashdump, send us the newest log (you can find it under `%appdata%\TS3Client\logs`)
4. Provide us informations to reproduce the crash.

## Installation of Salty Chat is corrupt

If you have the following error, follow the steps below:

![Installation of Salty Chat is corrupt](https://github.com/saltminede/saltychat-docs/raw/master/media/setup-installation-corrupt.png)

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

## FiveM: NUI stuck at "Connecting..."

CFX team implemented a NUI blacklist and blocked local (`127.0.0.1` and `localhost`) connections.
To use the plugin without a proxy, you need to make sure that your DNS server can resolve `lh.saltmine.de` to `127.0.0.1`.

Follow these steps to find out if you can resolve `lh.saltmine.de`:

1. Open Windows Command Prompt by searching `cmd`
2. Execute `nslookup lh.saltmine.de`

If it resolved to `127.0.0.1` follow the steps in chapter [How to enable debug logging?](#how-to-enable-debug-logging) and try to find the issue before contacting us.

If it doesn't resolve to `127.0.0.1` try to use a alternative DNS server (e.g. Google DNS or Cloudflare DNS) or add an exception to your router's DNS rebind protection (if possible).

### Solution A (change DNS server)

See following [guide](https://www.privateinternetaccess.com/blog/changing-your-dns-settings-on-windows-10/) how to change your dns servers.
Servers you can use for example:

- Google DNS server: https://developers.google.com/speed/public-dns/docs/using#addresses
- Cloudflare DNS server: https://developers.cloudflare.com/1.1.1.1/setting-up-1.1.1.1/windows

Note: If you have an IPv6 address, keep in mind to also change the DNS server for IPv6.

### Solution B (disable DNS rebind protection)

The procedure for disabling the dns rebind protection differs depending on the used router model.\
Check the manual of your router for the exact steps and make sure that the address `lh.saltmine.de` is defined as an exception for the dns rebind protection.
