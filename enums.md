# Enums

## Radio Type
```csharp
[Flags]
enum RadioType
{
    None = 1,
    ShortRange = 2,
    LongRange = 4,
    Distributed = 8,
    UltraShortRange = 16
}
```

## Command
```csharp
enum Command
{
    // Plugin
    PluginState = 0,

    // Instance
    Initiate = 1,
    Reset = 2,
    Ping = 3,
    Pong = 4,
    InstanceState = 5,
    SoundState = 6,
    SelfStateUpdate = 7,
    PlayerStateUpdate = 8,
    BulkUpdate = 9,
    RemovePlayer = 10,
    TalkState = 11,
    PlaySound = 18,
    StopSound = 19,

    // Phone
    PhoneCommunicationUpdate = 20,
    StopPhoneCommunication = 21,

    // Radio
    RadioCommunicationUpdate = 30,
    StopRadioCommunication = 31,
    RadioTowerUpdate = 32,

    // Megaphone
    MegaphoneCommunicationUpdate = 40,
    StopMegaphoneCommunication = 41,
}
```

## Error
```csharp
enum Error
{
    OK = 0,
    InvalidJson = 1,
    NotConnectedToServer = 2,
    AlreadyInGame = 3,
    ChannelNotAvailable = 4,
    NameNotAvailable = 5,
    InvalidValue = 6
}
```

## UpdateBranch
```csharp
enum UpdateBranch
{
    Stable = 0,
    Testing = 1,
    Preview = 2
}
```
