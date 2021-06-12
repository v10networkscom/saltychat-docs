# Salty Chat
Salty Chat is a TeamSpeak voice plugin which adds more realism to your gamemode (like GTA 5 FiveM/RAGEMP).
In order to serve a wide range of mods, the plugin provides a WebSocket server, which allows bidirectional communication.
Due to the possibility of communication in both directions, the plugin can also send "State Trigger" (player speaks, microphone muted/unmuted, sound muted/unmuted and more).

We provide resources for some mods and also maintain them.
Since it is impossible for us to provide a resource for every mod and every framework, we need your help.
If you write resources for certain mods or frameworks that we haven't covered, you are welcome to add them to our resources list through a pull request.

You can help us to improve our docs by contributing via pull requests - we appreciate any contribution.

Join our [Discord](https://discord.gg/MBCnqSf) and start with [Salty Chat](https://www.saltmine.de/)!

# Features
## Proximity
* 3D audio
* Adjustable ranges (for e.g. whispering and screaming)
* Distance-based flattening of the volume
* Multiple audio streams for one player (in combination with phone and radio)
* Voice effects
   * Muffling - Are you behind a wall?
   * Echo - Tunnel? HELLO...hello...hello
   * Megaphone - Police, stop right there!

## Radio
* Realistic voice distortion
* Distortion based on distance
* Different ranges
   * Ultra Short Range (1.8km)
   * Short Range (3km)
   * Long Range (8km)
* Communication from radio to radio, or distributed via radio towers
* Loudspeaker (players can listen to the radio traffic)
* [Customizable](/readme.md#configuration-file) audio mode for playback (left, right or stereo)

![alt text][concept-radio-modes]

## Phone
* Realistic voice distortion
* Distortion based on signal strength
* Loudspeaker (players can hear the conversation partners)
* [Customizable](/readme.md#configuration-file) audio mode for playback (left, right or stereo)

## Audio Player
* Sounds in the respective sound pack (`%appdata%\TS3Client\plugins\SaltyChat`) can be played and stopped
* Play multiple sounds at the same time (e.g. a ringtone and vibration)
* Clean looping of sounds
* Global overwriting of sounds (`%appdata%\TS3Client\plugins\SaltyChat\override`)
* Fallback if a file is missing (override > specified sound pack > default sound pack)

## Swiss Channels
In the [configuration file](https://github.com/saltminede/saltychat-docs/blob/master/setup.md#swisschannelids) there is the possibility to declare TeamSpeak channels as swiss channels.\
Swiss channels are channels in which the plugin keeps the original name of the client and does not move them to the ingame channel.

If a client leaves the [ingame channel](https://github.com/saltminede/saltychat-docs/blob/master/setup.md#ingamechannelid) and enters a swiss channel, the plugin will change the clients TeamSpeak name back to its origin and won't move the client to the ingame channel as long as it is in a swiss channel.

Note: The ingame channel should not be declared as a swiss channel, otherwise the clients won't be moved out of it after disconnecting from the server.

# Configuration file
When the plugin is starting, the configuration file under `%appdata%\TS3Client\plugins\SaltyChat\settings.json` will be loaded an applied.
Here are various options that can be customized:

Parameter | Description
------------ | -------------
WebSocketAddress | Address and port on which the WebSocket server binds
UpdateBranch | Update branch which is queried for a new version through our version API
OriginExceptions | Exceptions for the source of a WebSocket connection - e.g. you surf on saltmine.de, locally executed JavaScript can connect to the WebSocket, whereby the source would then be `https://saltmine.de`
InstanceTimeout | Time in seconds after which the instance will reset without a pong
Is3dEnabled | Enables/disables 3D audio
ExpertMode | Enables/disables export mode in settings menu
LogLevel | Defines how extensive the logging will be (`Error`, `Warning`, `Info`, `Debug` or `Extensive`)
PhoneOffset | Audio mode for phone playback (`Stereo`, `LeftOnly` or `RightOnly`)
RadioOffset | Audio mode for radio playback (`Stereo`, `LeftOnly` or `RightOnly`)
SecondaryRadioOffset | Audio mode for secondary radio playback (`Stereo`, `LeftOnly` or `RightOnly`)
MicClickMode | Overrides `PlayMicClick` property on radio communications (`ScriptDependent`, `Never` or `Always`)

# Versioning and Update Branches
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

# TeamSpeak Server Settings
To avoid issues with your TeamSpeak server, we recommend the following settings:
* Manage Virtual Server --> `Misc` tab --> `Min clients in channel before silence`: More then your server slots
* Adjust anti-flood
   * Method 1: Manage Virtual Server --> `Anti-Flood` tab --> adjust values as needed
   * Method 2: Set `b_client_ignore_antiflood` permission flag to the group your users are in

# Available resources
Mod | Language | Maintainer | Link | Comment |
|     :---:      |     :---:      |     :---:      |     :---:      |     :---:      |
FiveM | C# | [saltmine.de](https://github.com/saltminede) | [repo](https://github.com/saltminede/saltychat-fivem) | - |
RedM | C# | [saltmine.de](https://github.com/saltminede) | [repo](https://github.com/saltminede/saltychat-redm) | - |
RAGEMP | C# | [saltmine.de](https://github.com/saltminede) | [repo](https://github.com/saltminede/saltychat-ragemp) | - |
RAGEMP | TypeScript | discontinued | [repo](https://github.com/saltminede/saltychat-ragemp-js) | clientside only, outdated |
alt:V | C#/TS | [deluvas1911](https://github.com/deluvas1911) | [repo](https://github.com/deluvas1911/saltychat-altv) | - |

# Credits
We are using code from the following open source projects:
* [Newtonsoft.Json](https://github.com/JamesNK/Newtonsoft.Json)
* [RadioFX](https://github.com/thorwe/teamspeak-plugin-radiofx)
* [DSPFilters](https://github.com/vinniefalco/DSPFilters)
* [Fleck](https://github.com/statianzo/Fleck)

Sounds we ship in the `default` sound pack are made by [BeatbaronTV](https://twitter.com/BeatbaronTV), except from the radio sounds, these are recorded from two `Motorola Talkabout T82 Extreme` we bought for this.

Since this plugin is completely free to use, please consider supporting us with a donation through our [website](https://www.saltmine.de/), especially if you are running a project and have some leftovers or making profit while using Salty Chat.

[concept-radio-modes]: https://github.com/saltminede/saltychat-docs/raw/master/media/concept-radio-modes.jpg "Radio Modes"
