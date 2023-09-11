# Salty Chat
Salty Chat is a TeamSpeak voice plugin which adds more realism to your gamemode (like GTA 5 FiveM/RAGEMP).
In order to serve a wide range of mods, the plugin provides a WebSocket server, which allows bidirectional communication.
Due to the possibility of communication in both directions, the plugin can also send "State Trigger" (player speaks, microphone muted/unmuted, sound muted/unmuted and more).

We provide [resources](resources.md) for some mods and also maintain them.

Join our [Discord](https://gaming.v10networks.com/Discord) and get started with [Salty Chat](https://gaming.v10networks.com/SaltyChat)!

## Features
### Proximity
* 3D audio
* Adjustable ranges (for e.g. whispering and screaming)
* Distance-based flattening of the volume
* Multiple audio streams for one player (in combination with phone and radio)
* Voice effects
   * Muffling - Are you behind a wall?
   * Echo - Tunnel? HELLO...hello...hello
   * Megaphone - Police, stop right there!

### Radio
* Realistic voice distortion
* Distortion based on distance
* Different ranges
   * Ultra Short Range (1.8km)
   * Short Range (3km)
   * Long Range (8km)
* Communication from radio to radio, or distributed via radio towers
* Loudspeaker (players can listen to the radio traffic)
* [Customizable](configuration.md) audio mode for playback (left, right or stereo)

![alt text][concept-radio-modes]

### Phone
* Realistic voice distortion
* Distortion based on signal strength
* Loudspeaker (players can hear the conversation partners)
* [Customizable](configuration.md) audio mode for playback (left, right or stereo)

### Audio Player
* Sounds in the respective sound pack (`%appdata%\TS3Client\plugins\SaltyChat`) can be played and stopped
* Play multiple sounds at the same time (e.g. a ringtone and vibration)
* Clean looping of sounds
* Global overwriting of sounds (`%appdata%\TS3Client\plugins\SaltyChat\override`)
* Fallback if a file is missing (override > specified sound pack > default sound pack)

### Swiss Channels
In the [initiate command](commands.md#1--initiate) there is the possibility to declare TeamSpeak channels as swiss channels.\
Swiss channels are channels in which the plugin keeps the original name of the client and does not move them into the ingame channel.\
For example, support channels can be set as swiss channels, which gives you the ability to move users out of the in-game channel without them having to leave the game first.\
After declaring a channel as swiss channel, all it's sub-channels will be a swiss channel as well.

## Versioning and Update Branches
With version 0.4.0 we introduce a new versioning schema for Salty Chat.  
Versions within the same major version will be compatible with each other, even if there are changes like new features or fixes.

```
0.4.0
| | |
| | --- Patch (fixes and changes)
| --- Minor (new features)
--- Major (incompatible changes)
```

Any update will be tested in our multi-stage release process:

Branch | Description
------------ | -------------
Stable | Any change is tested in the previous branches and was found to be stable.
Testing | Public testing branch, where all changes can be tested. We recommend that this branch is only used by developers, who are familiar with the plugin and can debug any issues.
Preview | Private testing branch, where **untested** changes are made. Versions using this branch are distributed by Salty Chat developers and are meant to test specific changes, before releasing them to the testing branch.

## Credits
We are using code from the following open source projects:
* [Newtonsoft.Json](https://github.com/JamesNK/Newtonsoft.Json)
* [RadioFX](https://github.com/thorwe/teamspeak-plugin-radiofx)
* [DSPFilters](https://github.com/vinniefalco/DSPFilters)
* [Fleck](https://github.com/statianzo/Fleck)

Sounds we ship in the `default` sound pack are made by [BeatbaronTV](https://twitter.com/BeatbaronTV), except from the radio sounds, these are recorded from two `Motorola Talkabout T82 Extreme` we bought for this.

[concept-radio-modes]: ~/images/concept-radio-modes.jpg "Radio Modes"
