# Plugin Configuration
When the plugin is starting, the configuration file under `%appdata%\TS3Client\plugins\SaltyChat\settings.json` will be loaded an applied.
Here are various options that can be customized:

Parameter | Description
------------ | -------------
WebSocketAddress | Address and port on which the WebSocket server binds
UpdateBranch | Update branch which is queried for a new version through our version API
OriginExceptions | Exceptions for the source of a WebSocket connection - e.g. you surf on gaming.v10networks.com, locally executed JavaScript can connect to the WebSocket, whereby the source would then be `https://gaming.v10networks.com`
InstanceTimeout | Time in seconds after which the instance will reset without a pong
Is3dEnabled | Enables/disables 3D audio
ExpertMode | Enables/disables export mode in settings menu
LogLevel | Defines how extensive the logging will be (`Error`, `Warning`, `Info`, `Debug` or `Extensive`)
PhoneOffset | Audio mode for phone playback (`Stereo`, `LeftOnly` or `RightOnly`)
RadioOffset | Audio mode for radio playback (`Stereo`, `LeftOnly` or `RightOnly`)
SecondaryRadioOffset | Audio mode for secondary radio playback (`Stereo`, `LeftOnly` or `RightOnly`)
MicClickMode | Overrides `PlayMicClick` property on radio communications (`ScriptDependent`, `Never` or `Always`)

Most options are available through our settings UI: `TeamSpeak` > `Plugins` > `Salty Chat` > `Settings`