# Salty Chat FAQ

## Where can I download an old version?

In most cases you don't need an older version, because each version within a major release is compatible with each other (see [versioning scheme](intro.md#versioning-and-update-branches)).\
If you are experiencing issues with the latest version, you should create a detailed bug report here on [GitHub](https://github.com/v10networkscom/saltychat-docs/issues/new) or our Discord.

We provide older versions in case the latest version is unusable for your case, but we don't provide any guarantee for availability of older versions and will not support them.\
The download of specific versions is available at `https://gaming.v10networks.com/saltychat/download/x.x.x`, where **x.x.x** must be replaced with the desired version.\
For example, the link for Salty Chat 2.3.3 is `https://gaming.v10networks.com/saltychat/download/2.3.3`.

## How to enable extensive logging?

To debug issues and see what Salty Chat is sending/receiving through its WebSocket, you can enable more verbose logging.
- Open your TeamSpeak client
- Go to `Plugins` > `Salty Chat` > `Open Settings`
- Enable `Expert Mode`
- Select `Extensive` for `Log Level`

You can get a live feed of the log by pressing `CTRL` + `L` in TeamSpeak (`Tools` > `Client Log`) or find the files at `%appdata%\TS3Client\logs`.

To disable extensive logging, you can either disable `Expert Mode` or set `Log Level` to `Info`.\
**Don't use `ExtensiveDebug` until further instructions, because this will result in a huge log file.**

## My TeamSpeak crashes

Make sure you are using the latest version of Salty Chat.\
In case you are experiencing crashes with the latest version, provide us the crashdump (`%appdata%\TS3Client\crashdumps`) and some information about the situation in which the crash occurred. If there is no crashdump, you can provide the log (`%appdata%\TS3Client\logs`).

## Installation of Salty Chat is corrupt

If you have the following error, follow the solutions below.

![Installation of Salty Chat is corrupt](~/images/setup-installation-corrupt.png)

### Solution A

If you updated Salty Chat from a version prior or equal to 2.1.2, you may not have uninstalled Salty Chat before installing the new version:
- Close TeamSpeak
- Delete the the following files:
  - `%appdata%\TS3Client\plugins\SaltyChat.dll`
  - `%appdata%\TS3Client\plugins\SaltyChat\VoiceDistortion.dll`

### Solution B

With TeamSpeak x64 and Salty Chat 2.3.3+ you need `Microsoft Visual C++ Redistributable for Visual Studio 2015, 2017 and 2019` to run the plugin:
- Close TeamSpeak
- Download and install the [redist package](https://aka.ms/vs/16/release/vc_redist.x64.exe)

### Solution C

Check if the library files for voice distortion are present:
- `%appdata%\TS3Client\plugins\SaltyChat\VoiceDistortion_win32.dll`
- `%appdata%\TS3Client\plugins\SaltyChat\VoiceDistortion_win64.dll`

If not, follow the [manual installtion](#solution-c-manual-installation) instructions in `*.ts3_plugin is an unknown file`.

## *.ts3_plugin is an unknown file

If you can't open the `*.ts3_plugin` file or it tries to open it with e.g. notepad, you can use one of the following solutions.

### Solution A (Open with)

- Right click the `*.ts3_plugin` file
- `Open with...` or `Open with` > `Choose another app`
- `More apps` > `Look for antoher app on this PC` (at the botton)
- Go to your TS installation (probably `C:\Program Files\TeamSpeak 3 Client` or `C:\Program Files (x86)\TeamSpeak 3 Client`)
- Select `package_inst.exe`

### Solution B (Create file associations)

- Go to your TS installation (probably `C:\Program Files\TeamSpeak 3 Client` or `C:\Program Files (x86)\TeamSpeak 3 Client`)
- Run `createfileassoc.exe` as administrator.

### Solution C (Manual installation)

- Unzip the `*.ts3_plugin` file (e.g. with 7-Zip or WinRaR)
  - You can rename the file to `*.zip` and open it with the file explorer, so you don't need 3rd party software
- Copy the contents of the `plugin` directory and paste them into `%appdata%\TS3Client\plugins`

## CFX: NUI stuck at "Connecting..."

CFX team implemented a NUI blacklist and blocked local (`127.0.0.1` and `localhost`) connections.
To use the plugin without a proxy, you need to make sure that your DNS server can resolve `lh.v10.network` to `127.0.0.1`.

Follow these steps to find out if you can resolve `lh.v10.network`:

1. Open Windows Command Prompt by searching `cmd`
2. Execute `nslookup lh.v10.network`

If it resolves to `127.0.0.1`, follow the steps in chapter [How to enable debug logging?](#how-to-enable-extensive-logging) and try to find the issue before contacting us.

If it doesn't resolve to `127.0.0.1`, try to use a alternative DNS server (e.g. Google DNS or Cloudflare DNS) or add an exception to your router's DNS rebind protection (if possible).

### Solution A (Change DNS server)

See the guide on [how to change your DNS servers](https://www.privateinternetaccess.com/blog/changing-your-dns-settings-on-windows-10/) and use e.g. public DNS servers:
- Google DNS server: https://developers.google.com/speed/public-dns/docs/using#addresses
- Cloudflare DNS server: https://developers.cloudflare.com/1.1.1.1/setting-up-1.1.1.1/windows

Note: If you have an IPv6 address, keep in mind to also change the DNS server for IPv6.

### Solution B (Disable DNS rebind protection)

The procedure for disabling the dns rebind protection differs depending on the used router model.\
Check the manual of your router for the exact steps and make sure that the address `lh.v10.network` is defined as an exception for the dns rebind protection.
