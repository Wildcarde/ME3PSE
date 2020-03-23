# Installation Guide
*This is lifted from the forum posts to preserve the original posts content; only formatting tweaks have been made.*


For reference, anywhere where I mention this: `%PSE%` - the folder where you put PSE.
Example: I have PSE installed at C:\Misc\PSE. So, for me, `%PSE%\logs` is `C:\Misc\PSE\logs`.

## Disclaimer:
Read everything in this topic.
Things may change, get added or deleted, with or without prior notice, at any time, for any reason.
Always back your shit up. Back your shit up even when you're not told to!
How-To's
Last update - Dec 22 2017

## 1 - Installing PSE
Well, you don't actually "install" anything. PSE won't mess up your registry, or add hidden files in system folders. PSE is 100% in a "portable" state.
Just extract PSE to a folder of your choice.
If you're on Windows 7, you need to install Microsoft .NET Framework 4.5 - Windows 8, 8.1 and 10 users don't need to install this.
IMPORTANT:
a) PSE requires administrator rights. If you have UAC enabled, you'll have to confirm the execution of ME3Server_WV.exe And Setup.exe. If you have UAC disabled, those files will run with whatever privileges your Windows account have, and PSE will fail to run if proper admin rights aren't available.
b) Even with admin rights, PSE is unable to bypass protections imposed by antiviruses and firewalls. You'll have to add an exception for %PSE% path in your antivirus and/or firewall.

## 2 - Patching up your game I: binkw32.dll
In its original state, Mass Effect 3 will refuse connecting to PSE because of a server certificate check which is carried out under SSL connection. This is valid even if you use a cracked EXE - crackers decrypted the EXE and removed the Origin integration, but the certificate check is still in place. In order to bypass the certificate check, a fake binkw32.dll is used. When the fake dll is loaded, a special code is run which will patch the certificate check so the game will connect to anything. This fake dll is in %PSE%\patch, where the true binkw32.dll has been renamed to binkw23.dll. Functions in the fake dll which mirror the real ones in name are set up in a way where any call to them will be redirected to their respective counterparts in binkw23.dll.
Aside from the cert check patch, the fake dll also includes a DLC patch (authenticates all DLC's, including modded and user-made ones) and a console patch (an Unreal Engine 3 feature; open it with tilde/tab while ingame).
- Back up your original binkw32.dll in `Mass Effect 3\Binaries\Win32`!
- Manual patching:
- - Copy all files in `%PSE%\patch` to `Mass Effect 3\Binaries\Win32`. Say `yes` to file replace confirmation.
- Tool-assisted patching:
- - with `Setup.exe`: click 'First Time Setup', then 'Patch Game'.
- - with `ME3Server_WV.exe`: menu 'Tools' -> 'Patch Game'.
In the 'Open' file window, just navigate `Mass Effect 3\Binaries\Win32`, where MassEffect3.exe is, and select that file.
IMPORTANT: unless stated otherwise, consider that only the `binkw32.dll` distributed with PSE contains the certificate patch!
As of r21, the included `binkw32.dll` pertains to this repository: https://github.com/Erik-JS/masseffect-binkw32

## 3 - Patching up your game II: MassEffect3.exe
While it's possible to use PSE with original MassEffect3.exe running under Origin, currently you'll only be able to access local, custom-made profiles if you use a cracked MassEffect3.exe. The original EXE attempts to connect to the server using an authentication string from Origin, and PSE is unable to recognize "real" profiles with that, so in this case it provides a temporary account to you ("OriginPlayer"). Using temporary account, player data like credits and characters unlocked won't be saved.
- Back up your original MassEffect3.exe in `Mass Effect 3\Binaries\Win32`

__!IMPORTANT:__  
a) cracks won't be provided here;  
b) EXE version must be `1.5.5427.124`.

## 4 - Player profiles
Profiles are nothing more than plain text files stored in `%PSE%\player`. Those files contain data which is used to authenticate clients connecting to PSE. Player's inventory, credits, promotions and challenges will all be stored there.
Before attempting to connect to PSE, a player must have his/her respective profile in `%PSE%\player` using either:
- with `Setup.exe`: First Time Setup -> Create Profile, or
- with `ME3Server_WV.exe`: Tools -> Create Player Profile.

### About Local_Profile.sav:
Before the txt file is created, you'll be asked if you want to create a `Local_Profile.sav`. That file is supposed to be put in `Documents\BioWare\Mass Effect 3\Save`. It's recommended that you back up your existing copy of Local_Profile.sav before replacing it with the one created by PSE.
The LP file contains an authentication string which will be read by ME3, and subsequently be sent by the game to PSE. There's an alternate form of authentication where you can use an in-game login screen if you don't have a Local_Profile.sav in `Documents\BioWare\Mass Effect 3\Save`. In this case, when the 'Welcome to EA' screen is shown, click 'Continue', then enter your profile name (email field) and password in the next screen.

## 5 - Hosts file redirection
This is a required step for all machines where an instance of ME3 will be run on.
The purpose of editing the hosts file is so any requests made by the game to the official EA servers will instead be redirected to PSE.
In case you don't know how hosts work: https://en.wikipedia.org/wiki/Hosts_%28file%29
All URL's listed in `%PSE%\conf\redirect.txt` must be assigned to the IP of the machine where PSE will be running.
For the machine where PSE will be running (SERVER):
- Setup.exe -> Setup For Hoster -> Select appropriate LAN interface on the combo box -> Set IP and Start Server.
For the machine where PSE won't be running (CLIENT):
- Setup.exe -> Setup For Client -> Enter the IP of the SERVER machine -> Set IP and Close.
IMPORTANT:
a) Back up your original 'hosts' file!
b) Antiviruses may prevent PSE from changing 'hosts'. It's up to you to add an exception for PSE.
c) By default, when closing or opening PSE, the program will detect URL's already present on the hosts files, and will ask if the user wants to wipe them out. Leaving redirection entries there may affect other EA games like Battlefield 4 or Dragon Age: Inquisition, preventing you from accessing their online portion;
d) You can activate/deactivate redirection from PSE through Tools -> Hosts: Activate Redirection (F5), Deactivate Redirection (F6), Show Content (F7);
e) On CLIENT machines, deactivation can be easily achieved with Setup.exe: just click the 'Deactivate Redirection' button.

#1 to #5 is "required stuff", so make sure you understood them. Secondary will get added here soon...
