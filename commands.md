# Commands
Commands are used to tell Salty Chat what to do given the required parameters.  
Most of the time the unique identifier of the TeamSpeak server is required, so Salty Chat can defer between multiple instances.

A basic command would look like this in JSON:
```json
{ "Command": 2, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": null }
```

## 0 – PluginState
This will be sent by Salty Chat after connecting to the WebSocket server. 

ServerUniqueIdentifier required: No  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Version | `string` | Version of Salty Chat
ActiveInstances | `int` | Number of instances that are currently running

Example:
```json
{ "Command": 0, "ServerUniqueIdentifier": null, "Parameter": { "Version": "2.0.0", "ActiveInstances": 0 } }
```

## 1 – Initiate
Start an instance of Salty Chat.

ServerUniqueIdentifier required: No  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
ServerUniqueIdentifier | `string` | UID of the TeamSpeak Server
Name | `string` | Name the client will be renamed to
ChannelId | `uint64` | ID of the channel the client will be moved to
ChannelPassword | `string` | Password of the channel
SoundPack | `string` | The name of the sound pack that will be used for the instance
SwissChannelIds | `uint64[]` | IDs of neutral channels that can be joined, while the game instance is running

Example:
```json
{ "Command": 1, "ServerUniqueIdentifier": null, "Parameter": { "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Name": "abc12345", "ChannelId": 64, "ChannelPassword": null, "SoundPack": "default" } }
```

## 2 – Reset
Send by the plugin if a game instance was reset

ServerUniqueIdentifier required: Yes  
Parameter object: null

Example:
```json
{ "Command": 2, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": null }
```

## 3 – Ping
Salty Chat will periodically ping the WebSocket to ensure the instance is still active.
If the WebSocket doesn’t answer for a fixed amount of time, Salty Chat will reset the instance.

ServerUniqueIdentifier required: Yes  
Parameter object: null

Example:
```json
{ "Command": 3, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": null }
```

## 4 – Pong
To respond to a ping you have to use Pong. 

ServerUniqueIdentifier required: Yes  
Parameter object: null

Example:
```json
{ "Command": 4, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": null }
```

## 5 – InstanceState
This will be sent by Salty Chat if the player (dis-)connects to the specified TeamSpeak server or channel. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
IsConnectedToServer | `bool` | Indicates if TeamSpeak is connected to the server with the UID specified in "Initiate"
IsReady | `bool` | Is `true` if the TeamSpeak client is connected to the specified server and in the correct channel

Example:
```json
{ "Command": 5, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "IsConnectedToServer": true, "IsReady": true } }
```

## 6 – SoundState
This will be sent by Salty Chat on every microphone and sound state change. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
IsMicrophoneMuted | `bool` | `true` if the microphone is muted on TeamSpeak
IsSoundMuted | `bool` | `true` if the sound is muted on TeamSpeak

Example:
```json
{ "Command": 6, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "IsMicrophoneMuted": true, "IsSoundMuted": false } }
```

## 7 – SelfStateUpdate
Used to update the local player's state.

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Position | `Vector3` | The players 3D position
Rotation | `float` | The rotation of the player (-180 to 180)
VoiceEffect | `VoiceEffect` | [Flags of effects](/enums.md#voiceeffect) that should be applied to the voice

Example:
```json
{ "Command": 7, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Position": { "X": 2.5, "Y": 231.2, "Z": -22.1 }, "Rotation": 0.0 } }
```

## 8 – PlayerStateUpdate
Used to update the state of other players.

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player
Position | `Vector3` | The players 3D position
Rotation | `float` | The rotation of the player
VoiceRange | `float` | Range the player can be heard (proximity voice)
IsAlive | `bool` | If `false` the player can't be heard
VolumeOverride | `float?` | Overrides the volume calculated by proximity voice (based on the distance)
NoLoS | `bool` | `true` to enable a muffling sound effect
DistanceCulled | `bool` | `true` to remove player from proximity calculation

Example:
```json
{ "Command": 8, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes", "Position": { "X": 12.5, "Y": -211.5, "Z": 24.9 }, "Rotation": 0.0, "VoiceRange": 22.0, "IsAlive": true, "VolumeOverride": null, "NoLoS": false, "DistanceCulled": false } }
```

## 9 – BulkUpdate
Updates all player states in one command

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
PlayerStates | `PlayerState[]` | Array of player states
SelfState | `PlayerState` | Own player state

Example:
```json
{ "Command": 9, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "PlayerStates": [{ "Name": "2913e966dd7b4d5a", "Position": { "X": -76.2008, "Y": 843.405151, "Z": 235.706909 }, "VoiceRange": 8.0, "IsAlive" : true,"VolumeOverride": null }], "SelfState": { "Position": { "X":1709.001, "Y":3596.44263, "Z":30.1104813 }, "Rotation": 154.050766 } } }
```

## 10 – RemovePlayer
Used to tell Salty Chat that a player has left, so it can cleanup. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player

Example:
```json
{ "Command": 10, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes" } }
```

## 11 – TalkState
This will be sent by Salty Chat as soon as a player (including yourself) starts or stops talking.  

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | Name of the player
IsTalking | `bool` | `true` when player starts talking, `false` when he stops

Example:
```json
{ "Command": 11, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "2913e966dd7b4d5a", "IsTalking": true } }
```

## 18 – PlaySound
Play a sound from the specified sound pack.

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Filename | `string` | Name of the sound file (without ".wav")
IsLoop | `bool` | If `true` the sound will be looped until stopped by StopSound
Handle | `string` | Used for StopSound, if null Salty Chat will take the Filename-Parameter as handle

Example:
```json
{ "Command": 18, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Filename": "phoneRingtone", "IsLoop": true,  "string": "Ringtone" } }
```

## 19 – StopSound
Stops a sound that is played by StartSound

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Handle | `string` | Filename/Handle of the sound

Example:
```json
{ "Command": 19, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Handle": "Ringtone" } }
```

## 20 – PhoneCommunicationUpdate
Used to start, update or end a call. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player
SignalStrength | `int` | Determines the level of voice distortion (0 = Good qulity)
Volume | `float?` | Overrides the volume
Direct | `bool` | `true` if the communication is direct, `false` to relay the communication through other players (`RelayedBy`)
RelayedBy | `string[]` | string array of TeamSpeak names from players that are relaying the communication (loudspeaker)

Example:
```json
{ "Command": 20, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes", "SignalStrength": 8, "Volume": null, "Direct": false, "RelayedBy": ["sdneus923", "o97sdhlan"] } }
```

## 21 – StopPhoneCommunication
Used to end a call. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player

Example:
```json
{ "Command": 21, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes" } }
```

## 30 – RadioCommunicationUpdate
Used to start, update or end a radio communication. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player
SenderRadioType | `RadioType` | Radio type of the sending player
OwnRadioType | `RadioType` | The local players radio type
PlayMicClick | `bool` | If `true` Salty Chat will automatically play the sound "onMicClick" or "offMicClick" of the specified sound pack, if the player is in range
Volume | `float?` | Overrides the volume
Direct | `bool` | `true` if the communication is direct, `false` to relay the communication through other players (`RelayedBy`)
Secondary | `bool` | `true` if the communication is on the secondary channel
RelayedBy | `string[]` | string array of TeamSpeak names from players that are relaying the communication (loudspeaker)

Example:
```json
{ "Command": 30, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes", "SenderRadioType": 12,  "OwnRadioType": 12,  "PlayMicClick": true, "Volume": null, "Direct": true, "RelayedBy": [] } }
```

## 31 – StopRadioCommunication
Used to end a radio communication. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player
PlayMicClick | `bool` | If `true` Salty Chat will automatically play the sound "offMicClick" of the specified sound pack, if the player is in range

Example:
```json
{ "Command": 31, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes",  "PlayMicClick": true } }
```

## 32 – RadioTowerUpdate
Update positions of all available radio tower used for the distributed radio.

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Towers | `Vector3[]` | Array of Vector3 positions representing the radio tower positions

Example:
```json
{ "Command": 32, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Towers": [{ "X": 942.5, "Y": -942.0, "Z": 41.5 }, { "X": 357.2, "Y": -811.5, "Z": 29.9 }, { "X": 55.5, "Y": 871.5, "Z": -52.3 }, { "X": 752.3, "Y": 358.2, "Z": -32.6 } ]} }
```

## 40 – MegaphoneCommunicationUpdate
Used to start, update or end a megaphone effect. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player
Range | `float` | Range where the player can be heard through the megaphone
Volume | `float?` | Overrides the volume

Example:
```json
{ "Command": 40, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes", "Range": 100.0, "Volume": null } }
```

## 41 – StopMegaphoneCommunication
Used to end a megaphone effect. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player

Example:
```json
{ "Command": 41, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes" } }
```
