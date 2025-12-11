# Daybreak Launcher on Linux – Working Installation Guide

### Faugus Launcher

Install Faugus via your package manager.<br>
The github can be found here: https://github.com/Faugus/faugus-launcher

Once Faugus is open, click the `+` button in the bottom left corner.

1. Enter a title
2. The Prefix will automatically fill
3. Add your Guild Wars installer file to the path by clicking the `search` button (`GwSetup.exe`)
4. You can choose to add shortcuts below, with the tick boxes
5. In the Tools tab, ensure `Game Mode` is ticked
6. Click `Ok` to close this window
7. The click the `Play` button or double click to run 


![](images/faug0.png)

8. When you see the Guild Wars installer window, you can either let the install complete now, or close it and have the Daybreak launcher handle the install. To speed things up and ensure Daybreak is working I recommend just closing the installer now.
9. Download the Daybreak launcher from their github here: https://github.com/gwdevhub/Daybreak/releases
10. Right click your Guild Wars entry in Faugus and click `Open prefix location`
11. Open the `drive_c` folder
12. Create a folder named `Daybreak` here.
![](images/faug4.png)
13. Extract the contents of the Daybreak .zip file to this new Daybreak folder
14. Go back to Faugus and right click your Guild Wars entry and select `Edit`
15. Change the path be selecting the `search` button and select the `Daybreak.exe` in the folder you created. This will be under the `/home/<username>/Faugus/` path

> **⚠️ IMPORTANT - Initialize Daybreak once**
> 
> After setting Daybreak.exe as the executable but before continuing:
>
> 1. Launch Daybreak once
> 2. Wait 10 seconds (blank/white window is expected)
> 3. Close it again
>
> This initializes the WebView2 host environment inside the prefix.

16. Download [Microsoft WebView2 from the downloads page here](https://developer.microsoft.com/en-us/microsoft-edge/webview2/)
 - Download the `Evergreen Standalone Installer (x64)`
 - Also download thethe `Fixed Version` (this will be a .cab file)

17. Open the Tools tab of your game in Faugus. And click the `Run` button.
 - Select the `MicrosoftEdgeWebView2RuntimeInstallerX64.exe` that you downloaded
 - Run the installer
 - It will likely give an error message or just close/crash once it's finished, this is fine.

18. Extract the .cab file contents to a new folder you will need to create under 
```
drive_c/Program Files (x86)/Microsoft/EdgeWebView/
```
![](images/faug7.png)

19. [Download this registry file](installer/webview2.reg) and place it in your `drive_c` folder
 - Below is a preview of the registry file. You can ignore this if you just want to download the file and follow the guide.

```
[HKEY_LOCAL_MACHINE\Software\Microsoft\EdgeUpdate]
"pv"="143.0.3650.66"
"st"=dword:00000001
"doNotSandbox"=dword:00000001

[HKEY_LOCAL_MACHINE\Software\Microsoft\EdgeWebView]
"pv"="143.0.3650.66"

[HKEY_CURRENT_USER\Software\Microsoft\Edge\WebView\Rendering]
"DisableGpu"=dword:00000001
```

![](images/faug9.png)

20. Back in Faugus, switch to the `Tools` tab and click on the `Winetricks` button in the bottom right
21. Click `Ok` with the `Select the default wineprefix` option checked
![](images/faug5.png)

22. Select regedit and click ok
![](images/faug8.png)


23. Click on the Registry menu and select `Import Registry File...`

![bottles](images/bottles10.png)

24. Choose the webview2.reg file that you downloaded earlier. After the import completes, close the registry.

![bottles](images/bottles11.png)

25. After closing the registry, switch to `Install a Windows DLL or component`

![](images/faug10.png)

26. Select `dotnetdesktop9` in the list and click `Ok`

![](images/faug11.png)

You should now be able to run Daybreak under Linux! 🎉

At this point you can either point Daybreak to your existing installation of Guild Wars or have Daybreak install Guild Wars for you in its Prefix. 

Daybreak will then handle your Mods and GWToolbox entirely. 

Mods for gMod can be found here: https://wiki.guildwars.com/wiki/Player-made_Modifications/Cartography_Index