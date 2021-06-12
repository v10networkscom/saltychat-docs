# Config variables

## ServerUniqueIdentifier
Identifies your TeamSpeak server, so you can use multiple tabs.  
The easiest way to get your Server UID, is to install [Salty Chat](https://www.saltmine.de) and click on the server in the channel tree.

![alt text][setup-server-uid]

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
IDs of the channels that can be entered while the game instance is running, without the client being automatically pushed back to the ingame channel.\
As soon as the client enters a swiss channel, the original TeamSpeak name is restored.

If the client is in a swiss channel while the game instance is initialized, the plugin will move it to the ingame channel and rename it only after leaving the swiss channel.

Note: If the ingame channel is declared as swiss channel, the player will not be moved to his original channel after disconnecting.
If the waiting room is declared as a swiss channel, no automatic joining of the ingame channel takes place until the waiting room is left.
