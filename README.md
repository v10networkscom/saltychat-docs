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

## Radio
* Realistic voice distortion
* Distortion based on distance
* Different ranges
   * Ultra Short Range (1.8km)
   * Short Range (3km)
   * Long Range (8km)
* Communication from radio to radio, or distributed via radio towers
* Loudspeaker (players can listen to the radio traffic)
* Customizable 3D position for playback

## Phone
* Realistic voice distortion
* Distortion based on signal strength
* Loudspeaker (players can hear the conversation partners)
* Customizable 3D position for playback

## Audio Player
* Sounds in the respective sound pack (`%appdata%\TS3Client\plugins\SaltyChat`) can be played and stopped
* Play multiple sounds at the same time (e.g. a ringtone and vibration)
* Clean looping of sounds
* Global overwriting of sounds (`%appdata%\TS3Client\plugins\SaltyChat\override`)

# Configuration file
When the plugin is starting, the configuration file under `%appdata%\TS3Client\plugins\SaltyChat\settings.json` will be loaded an applied.
Here are various options that can be customized:

Parameter | Description
------------ | -------------
WebSocketAddress | Address and port on which the WebSocket server binds
UpdateBranch | Update branch which is queried for a new version through our version API
OriginExceptions | Exceptions for the source of a WebSocket connection - e.g. you surf on saltmine.de, locally executed JavaScript can connect to the WebSocket, whereby the source would then be `https://saltmine.de`
Is3dEnabled | Enables/disables 3D audio
IsDebugLoggingEnabled | Enables/disables simple debug logging - should only be switched on when needed
IsExtensiveLoggingEnabled | Enables/disables extensive debug logging - should only be turned on when needed
PhoneOffset | 3D position for phone playback
RadioOffset | 3D position for radio playback

# Available resources
Mod | Language | Maintainer | Link | Comment |
|     :---:      |     :---:      |     :---:      |     :---:      |     :---:      |
FiveM | C# | [saltmine.de](https://github.com/saltminede) | [repo](https://github.com/saltminede/saltychat-fivem) | - |
RedM | C# | [saltmine.de](https://github.com/saltminede) | [repo](https://github.com/saltminede/saltychat-redm) | - |
RAGEMP | C# | [saltmine.de](https://github.com/saltminede) | [repo](https://github.com/saltminede/saltychat-ragemp) | - |
RAGEMP | TypeScript | [saltmine.de](https://github.com/saltminede) | [repo](https://github.com/saltminede/saltychat-ragemp-js) | clientside only |
