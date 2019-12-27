# Config variables

## ServerUniqueIdentifier
Identifies your TeamSpeak server, so you can use multiple tabs.  
The easiest way to get your Server UID, is to install [Salty Chat](https://www.saltmine.de) and click on the server in the channel tree.

![alt text][setup-server-uid]

## RequiredUpdateBranch
If you specify a required update branch, the plugin of all players have to use the specified update branch.  
Update Branches:
* `Stable`
* `Testing`
* `PreBuild`

## MinimumPluginVersion
The plugin must have atleast the specified version, e. g. `0.3.11`.

## SoundPack
Specifies the sound pack the plugin should use.
Sound packs have to be at `%appdata%\TS3Client\plugins\SaltyChat`.

The plugin uses the following order, if it searches for sound files:
1. `override`
2. Specified sound pack
3. `default`

## IngameChannelId
ID of the TeamSpeak channel the client should be in while the session is running.  
The plugin will automaticly join the channel and rejoin it after moving out of it, or reconnecting to the TeamSpeak server.

![alt text][setup-channel-id]

## IngameChannelPassword
Password of the TeamSpeak channel.

[setup-server-uid]: https://github.com/saltminede/saltychat-docs/raw/master/media/setup-server-uid.jpg "TeamSpeak Server UID"
[setup-channel-id]: https://github.com/saltminede/saltychat-docs/raw/master/media/setup-channel-id.jpg "TeamSpeak Channel ID"

## SwissChannelIds
IDs of neutral channels that can be joined, while the game instance is running
While moving in one of these channels, the plugin will restore the original TeamSpeak name.
The client will be automaticly renamed to the instance name, once the swiss channel is leaved, which also results in a move to the instance channel.
