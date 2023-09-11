# Recommended TeamSpeak Settings

## Client
todo

## Server
To avoid issues with your TeamSpeak server, we recommend the following settings:
* Manage Virtual Server --> `Misc` tab --> `Min clients in channel before silence`: More then your server slots
* Adjust anti-flood (only if needed)
   * Method 1: Manage Virtual Server --> `Anti-Flood` tab --> adjust values as needed
   * Method 2: Set `b_client_ignore_antiflood` permission flag to the group your users are in

Ensure that users can whisper among themselves while in the ingame channel. In larger and more restrictive environments, you may not want to give all users permission to whisper. There are ways to solve this with bots, but here are "easy" ones:
* Method 1 (only users in the ingame channel can whisper):
   * Remove the `i_client_whisper_power` permission flag in the group to which your users belong and set `i_client_needed_whisper_power` to, say, 10
   * Edit the permissions for your ingame channel (`Permissions` --> `Channel Permissions` and select the channel on the left) and set `i_client_whisper_power` to 10 (>= needed power from before)
* Method 2 (everony can whisper):
   * Set `i_client_whisper_power` permission flag for your user group >= `i_client_needed_whisper_power` of all your groups