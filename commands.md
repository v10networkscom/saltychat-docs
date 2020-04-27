# Commands
Commands are used to tell Salty Chat what to do given the required parameters.  
Most of the time the unique identifier of the TeamSpeak server is required, so Salty Chat can defer between multiple instances.

A basic command would look like this in JSON:
```json
{ "Command": 2, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": null }
```

## -1 – Reset
Send by the plugin if a game instance was reset

ServerUniqueIdentifier required: Yes  
Parameter object: null

Example:
```json
{ "Command": -1, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": null }
```

## 0 – Initiate
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
{ "Command": 0, "ServerUniqueIdentifier": null, "Parameter": { "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Name": "abc12345", "ChannelId": 64, "ChannelPassword": null, "SoundPack": "default" } }
```

## 1 – Ping
Salty Chat will periodically ping the WebSocket to ensure the instance is still active.
If the WebSocket doesn’t answer for a fixed amount of time, Salty Chat will reset the instance.

ServerUniqueIdentifier required: Yes  
Parameter object: null

Example:
```json
{ "Command": 1, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": null }
```

## 2 – Pong
To respond to a ping you have to use Pong. 

ServerUniqueIdentifier required: Yes  
Parameter object: null

Example:
```json
{ "Command": 2, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": null }
```

## 3 – StateUpdate
This will be sent by Salty Chat on every state change and displays the current state of Salty Chat and TeamSpeak. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
UpdateBranch | `string` | Branch of Salty Chat
Version | `string` | Version of Salty Chat
IsConnectedToServer | `bool` | Indicates if TeamSpeak is connected to the server with the UID specified in "Initiate"
IsReady | `bool` | Is `true` if the TeamSpeak client is connected to the specified server and in the correct channel
IsTalking | `bool` | `true` if the player is talking on TeamSpeak
IsMicrophoneMuted | `bool` | `true` if the microphone is muted on TeamSpeak
IsSoundMuted | `bool` | `true` if the sound is muted on TeamSpeak

Example:
```json
{ "Command": 3, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "UpdateBranch": 0, "Version": "0.2.11", "IsConnectedToServer": true, "IsReady": true, "IsTalking": false, "IsMicrophoneMuted": true, "IsSoundMuted": false } }
```

## 4 – SelfStateUpdate
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
{ "Command": 4, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Position": { "X": 2.5, "Y": 231.2, "Z": -22.1 }, "Rotation": 0.0 } }
```

## 5 – PlayerStateUpdate
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
{ "Command": 5, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes", "Position": { "X": 12.5, "Y": -211.5, "Z": 24.9 }, "Rotation": 0.0, "VoiceRange": 22.0, "IsAlive": true, "VolumeOverride": null, "NoLoS": false, "DistanceCulled": false } }
```

## 6 – RemovePlayer
Used to tell Salty Chat that a player has left, so it can cleanup. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player

Example:
```json
{ "Command": 6, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes" } }
```

## 7 – PhoneCommunicationUpdate
Used to start, update or end a call. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player
SignalStrength | `int` | Determines the level of voice distortion (0 = Good qulity, 18 = worst quality)
Volume | `float?` | Overrides the volume `available (0 - 20)`
Direct | `bool` | `true` if the communication is direct, `false` to relay the communication through other players (`RelayedBy`)
RelayedBy | `string[]` | string array of TeamSpeak names from players that are relaying the communication (loudspeaker)

Example:
```json
{ "Command": 7, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes", "SignalStrength": 8, "Volume": null, "Direct": false, "RelayedBy": ["sdneus923", "o97sdhlan"] } }
```

## 8 – StopPhoneCommunication
Used to end a call. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player

Example:
```json
{ "Command": 8, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes" } }
```

## 9 – RadioTowerUpdate
Update positions of all available radio tower used for the distributed radio.

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Towers | `Vector3[]` | Array of Vector3 positions representing the radio tower positions

Example:
```json
{ "Command": 9, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Towers": [{ "X": 942.5, "Y": -942.0, "Z": 41.5 }, { "X": 357.2, "Y": -811.5, "Z": 29.9 }, { "X": 55.5, "Y": 871.5, "Z": -52.3 }, { "X": 752.3, "Y": 358.2, "Z": -32.6 } ]} }
```

## 10 – RadioCommunicationUpdate
Used to start, update or end a radio communication. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player
SenderRadioType | `RadioType` | Radio type of the sending player
OwnRadioType | `RadioType` | The local players radio type
PlayMicClick | `bool` | If `true` Salty Chat will automatically play the sound "onMicClick" or "offMicClick" of the specified sound pack, if the player is in range
Volume | `float?` | Overrides the volume `available (0 - 20)`
Direct | `bool` | `true` if the communication is direct, `false` to relay the communication through other players (`RelayedBy`)
Secondary | `bool` | `true` if the communication is on the secondary channel
RelayedBy | `string[]` | string array of TeamSpeak names from players that are relaying the communication (loudspeaker)

Example:
```json
{ "Command": 10, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes", "SenderRadioType": 12,  "OwnRadioType": 12,  "PlayMicClick": true, "Volume": null, "Direct": true, "RelayedBy": [] } }
```

## 11 – StopRadioCommunication
Used to end a radio communication. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player
PlayMicClick | `bool` | If `true` Salty Chat will automatically play the sound "offMicClick" of the specified sound pack, if the player is in range

Example:
```json
{ "Command": 11, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes",  "PlayMicClick": true } }
```

## 12 – PlaySound
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
{ "Command": 12, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Filename": "phoneRingtone", "IsLoop": true,  "string": "Ringtone" } }
```

## 13 – StopSound
Stops a sound that is played by StartSound

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Handle | `string` | Filename/Handle of the sound

Example:
```json
{ "Command": 13, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Handle": "Ringtone" } }
```

## 14 – BulkUpdate
Updates all player states in one command

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
PlayerStates | `PlayerState[]` | Array of player states
SelfState | `PlayerState` | Own player state

Example:
```json
{ "Command": 14, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "PlayerStates": [{ "Name": "2913e966dd7b4d5a", "Position": { "X": -76.2008, "Y": 843.405151, "Z": 235.706909 }, "VoiceRange": 8.0, "IsAlive" : true,"VolumeOverride": null }], "SelfState": { "Position": { "X":1709.001, "Y":3596.44263, "Z":30.1104813 }, "Rotation": 154.050766 } } }
```

## 15 – TalkStateChange
This will be sent by Salty Chat as soon as a player starts or stops talking.  

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | Name of the player
IsTalking | `bool` | `true` when player starts talking, `false` when he stops

Example:
```json
{ "Command": 15, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "2913e966dd7b4d5a", "IsTalking": true } }
```

## 16 – MegaphoneCommunicationUpdate
Used to start, update or end a megaphone effect. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player
Range | `float` | Range where the player can be heard through the megaphone
Volume | `float?` | Overrides the volume `available (0 - 20)`

Example:
```json
{ "Command": 16, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes", "Range": 100.0, "Volume": null } }
```

## 17 – StopMegaphoneCommunication
Used to end a megaphone effect. 

ServerUniqueIdentifier required: Yes  
Parameter object:

Property | Type | Description
------------ | ------------- | -------------
Name | `string` | TeamSpeak name of the player

Example:
```json
{ "Command": 17, "ServerUniqueIdentifier": "NMjxHW5psWaLNmFh0+kjnQik7Qc=", "Parameter": { "Name": "s1v8s2e7wes" } }
```
