
# How to  use SaltyChat with gcPhone (FiveM)
If you are using the GcPhone Script you can easily make it work with the SaltyChat System by adjusting some of its code.
#
 Make sure:
- that you have the WebRTC feature disabled in gcPhone (`html/static/config/config.json`)
- that you have removed all old code you may have added when using TokoVOIP or other modifications to gcPhone's voice/connecting system in the client.lua


After you are sure the above points are done, you can add the SaltyChat exports to the gcPhone `server.lua` file.

You will need the following lines of code:

To create a Call:
```lua
exports['saltychat']:EstablishCall(AppelsEnCours[id].receiver_src, AppelsEnCours[id].transmitter_src)
exports['saltychat']:EstablishCall(AppelsEnCours[id].transmitter_src, AppelsEnCours[id].receiver_src)
```
To cancel a Call:
```lua
exports['saltychat']:EndCall(AppelsEnCours[id].receiver_src, AppelsEnCours[id].transmitter_src)
exports['saltychat']:EndCall(AppelsEnCours[id].transmitter_src, AppelsEnCours[id].receiver_src)
```
			
		
- Look for the 'gcPhone:acceptCall' event and add the code to create a call below `saveAppels(AppelsEnCours[id])` like this:
![How to Create a call](https://screens.egopvp.com/files/2020/03/20/notepad_mnyJPbqAUB.png)

- Look for the 'gcPhone:rejectCall' event and add the code to cancel a call  like this:
![](https://screens.egopvp.com/files/2020/03/20/notepad_9SYhcnSYAB.png)

## Errors

If you encounter errors when trying to use that code:

- check for Spelling mistakes (often in the `"AppelsEnCours"` part!)
- make sure gcPhone is started AFTER SaltyChat.
- make sure u are in the `server.lua` and not the `client.lua`(or any other!)
- make sure gcPhone was working before using this fix. 
