# Official FAQ
Originally started by Milakai. Last update: Jul 09 2018




## ERRORS
- I get an error in the log: "AuthenticationException: A call to SSPI failed, see inner exception." (Windows 10)  
As of v1709 (Fall Creators Update; 10.0.16299.\*), Windows 10 no longer, by default, allows the use of two cipher suites (a set of algorithms used in secure connections) which are essential for PSE and ME3 to successfully communicate. Specifically: TLS_RSA_WITH_RC4_128_SHA and TLS_RSA_WITH_RC4_128_MD5.  
Either one or both cipher suites need to be put back by the user into the "allowed" list in order to fix this issue.  
Fortunately, I managed to create an easy way of doing that:  
https://www.dropbox.com/s/0oy8kn31o132x ... g.zip?dl=0  
After "adding" the cipher suites, restart your PC.  

Related topic: PSE for Windows 10?
Added in Feb 10 2018: PowerShell code for those who want to do it manually (don't know why I didn't disclose this before, whatever).
```
See currently enabled cipher suites:
CODE: SELECT ALL

Get-TlsCipherSuite | Format-Table -Property Name
Enable required cipher suites:
CODE: SELECT ALL

Enable-TlsCipherSuite -Name 'TLS_RSA_WITH_RC4_128_SHA'
Enable-TlsCipherSuite -Name 'TLS_RSA_WITH_RC4_128_MD5'
Edit: Jul 09 2018
```
1) Noted by GitHub user "micheljung": these PowerShell commands may require admin rights.  
2) Just a heads up: after the 1803 update (10.0.17134.\*), Windows 10 has disabled those cipher suites again, and I had to manually re-insert them back through PowerShell. It's likely that this will keep happening whenever a new big update is released.

- When I click on Multiplayer/any menu-like screen the game crashes
Let each menu "settle" (wait a few seconds before clicking anything).
This is a problem with the game itself, and there's no definitive fix for it yet.

- When I try connect to the server it writes this:
08-07-14-22-13-03 [Redirector] Crashed:
Authentication failed because the remote party has closed the stream transmission.
Make sure you patch the game with the dll's provided. See How-To #2.

- When I open Mass Effect 3 I get the 'could not connect to EA servers' message.
First of all, PSE must be running before ME3 is started.
Make sure redirection is active on the machine where ME3 is running (check hosts file to see if the correct IP has been written there, when in doubt just use the deactivate function and start all procedures again). See How-To #5.

- I'm using XP and got an error from the Binkw32.dll, 'GetTickCount64 could not be located in the dynamic link library KERNEL32.dll'
On r18, a new binkw32.dll properly compiled for Windows XP 32-bit was included.
As of r21, Windows XP is no longer supported.

- I get an error about missing MSVCP110.dll / MSVCR110.dll
You need to install the VC 2012 runtime. http://www.microsoft.com/en-us/download ... x?id=30679
As of r21, a separate VC runtime redistributable is not needed for binkw32.dll.

- When I enter the game the emulator doesn't do its job (can't login): "connecting to server", then "server is not available".
See How-To #4. This is caused by the game sending an unknown authentication string to PSE due to Local_Profile.sav being from an old/deleted profile, or from your Origin account.

- In Blinkw32.log is written: Autopatcher by Warranty Voider/Got adresses/Trying again (this repeats 10 times)/Patch position 2: 0xd5a351/Patch position 2: Patched/Patched Cert Check! (game fails to start)
Create a new PCConsoleTOC.bin with the ME3 Explorer (with the Auto TOC Tool)
Also make sure you create a proper profile and try using multiple versions of different cracks.
If you tried the methods above to no avail then reinstall the game and repeat.

- The joiner never finds the match the hoster is on, it keeps on searching forever (if you want to connect through hamachi or tunngle).
This issue has been corrected in r18. If you’re still having this trouble, please make a post stating so.

- ''The application was unable to start correctly (0x000007b). Click OK to close the application.''
This error message may occur on 64 bit operating systems trying to cope with 32-bit dll's, apps and all of that sort or vice-versa.
Try uninstalling all the microsoft visuals, .net framework and make sure you have at least directX 9.0c (and the first 2) installed for both architectures of windows(32 and 64 bit). After that, run disk cleanup to make sure everything is gone and then restart your computer. Download and install every software from here: http://www.computerbase.de/downloads/sy ... -runtimes/
If it still doesn't work you can try manually placing dll's in system32 and sysWOW64 by googling the error, but consider this as a last resort option.
If you manually replaced or moved some dll's in system32 or sysWOW64 (and this error pops up) without a backup alternative then you need to reinstall your OS.

- I get this windows error access to path c:\windows\system32\drivers\etc\host is denied.
Check your firewall / antivirus or any other kind of security measure currently active in your PC.

- I get an error message in the log: ”An attempt was made to access a socket in a way forbidden by assigned access privileges to it”
As with the previous question, this may be due to “rules” imposed by firewall / antivirus. Please add an exception for PSE in your firewall/antivirus.

- I get an error message in the log: ”The requested address is not valid in its context”
This happens when IP in conf.txt doesn’t match any of the IP’s assigned to network adapters (physical or virtual) in your machine. This can be fixed by using Setup.exe: Setup for Hoster -> select a valid interface/IP from the list -> Set IP and Start Server.

- I get an error message in the log: ”The parameter is incorrect”
 - Check AV / firewall;
 - reset Winsock;
 - reinstall/repair .NET Framework.  
Reference: http://hopper.minecraft.net/help/kb/soc ... -error-04/
More about resetting Winsock: http://forum.thewindowsclub.com/windows ... 8-7-a.html

- I'm unable to play as a profile I've created. The main menu message says I'm logged as "OriginPlayer".  
See How-To #3.  
Short story: custom profiles are only available through 'login' and 'silentLogin' packets. Original EXE logs in through 'originLogin'.  
Long story: currently, you must use a cracked EXE in order to play as custom profiles. The original EXE will attempt to log into the server with an 'originLogin' packet, which uses an auth string from Origin, and there's no way to manipulate that unless Origin itself is hacked. The cracked EXE obviously has all links cut from the Origin client, so it's sort of unable to retrieve an auth string from the Origin client, and instead uses whatever string is stored inside Local_Profile.sav ('silentLogin'), or may show a screen asking for email/password of the user's Origin account ('login').

- When using MITM, I get this error: ”Exception: Unknown Tdf Type”  
Change "RWTimeout" in conf/conf.txt to a number higher than 100. Ping the TargetIP (92.52.77.245) and see what average response time you get (e.g. if you get 213ms then you should use 250 or 300 as your RWTimeout).

## OTHER QUESTIONS
- If the game crashes will it save?
Nope.

- There 5 free DLC (Rebellion, Earth, Reckoning, Retaliation, Resurgence). Do they work with PSE?
Yes, they do. You can check the '/Mass Effect 3/BIOgame/DLC' folder for them (DLC_CON_MP1, 2, 3, 4 and 5)

- Where can I get them?  
Anyone who owns the game can get them from Origin: right-click ME3, View Game Details, scroll down to Add-ons & Bonuses.
And anyone who doesn't own the game will have to get them elsewhere, not here.

- Any way to make this work without patches?
You would need to MITM in the old version without the patches, but the online servers don't allow that anymore, so there's no way to regain that. Check your MassEffect3.exe for file version: 1.5.5427.124 and/or product version: 05427.124. If it’s anything other than these, then it won’t work with PSE, or it may work with limited functionality, you’re on your own in this case. (this also applies to ME3 Demo)

- What features are already available?
 - User authentication;
 - Create match;
 - Join match;
 - Save/load player data;
 - Galactic readiness and promotions in SP campaign;
 - Leaderboards.

- What features are not available yet?
 - Quick match filters: after client request, PSE returns lobbies according to these rules: 1- creation time, 2- is active, 3- has free slot. Any other rules are currently ignored (number of required/unused DLC's, private/public lobby, random or specific map/difficulty/enemy);
 - Host migration: currently under research.

- When will feature X be implemented? / When is the next release of PSE?
When it's done.
