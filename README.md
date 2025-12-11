# Daybreak Launcher on Linux (Bottles) – Working Installation Guide

### 1. Create a clean bottle for Daybreak

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
9. Right click your Guild Wars entry in Faugus and click `Open prefix location`
10. Open the `drive_c` folder
11. Create a folder named `Daybreak` here.
![](images/faug4.png)
12. Extract the contents of the Daybreak .zip file to this new Daybreak folder
13. Go back to Faugus and right click your Guild Wars entry and select `Edit`
14. Change the path be selecting the `search` button and select the `Daybreak.exe` in the folder you created. This will be under the `/home/<username>/Faugus/` path

15. Download [Microsoft WebView2 from the downloads page here](https://developer.microsoft.com/en-us/microsoft-edge/webview2/)
 - ensure you download the `Fixed Version`
 - this will be a .cab file

16. Extract the .cab file contents to a new folder you will need to create under 
```
drive_c/Program Files (x86)/Microsoft/EdgeWebView/
```

![](images/faug7.png)
17. Back in Faugus, switch to the `Tools` tab and click on the `Winetricks` button in the bottom right

18. Click `Ok` with the `Select the default wineprefix` option checked
![](images/faug5.png)

19. Select regedit and click ok
![](images/faug8.png)


### 2. Place Daybreak in the bottle

Once created, open the Guild Wars bottle and click on the Browse C:/ drive button:

![bottles](images/bottles3.png)

Create a new folder and name it "daybreak"

Download Daybreak from the official github: https://github.com/gwdevhub/Daybreak/releases

Open the downloaded .zip file and extract all the contents in to the daybreak folder you created above.



### 3. Download WebView2 Fixed Version

From [Microsoft WebView2 downloads page](https://developer.microsoft.com/en-us/microsoft-edge/webview2/):

**Download:**

- ✔ **Fixed Version** (not the Bootstrapper or Standalone Installer)

### 4. Extract the CAB into the bottle

Inside your bottle, create the EdgeWebView folder:

```
drive_c/Program Files (x86)/Microsoft/EdgeWebView/
```

Extract the CAB contents into this folder.

You should end up with something like:

```
.../EdgeWebView/Microsoft.WebView2.FixedVersionRuntime.143.0.3650.66.x64/
```

(The version number may differ.)

### 5. Register WebView2 in the bottle's Wine registry

First, [download the WebView2 registry file here.](installer/webview2.reg)

Then inside Bottles, click the Browse button and save the webview2.reg file to this path, in the "drive_c" folder.

![bottles](images/bottles3.png)

Next, open the registry editor in Bottles.

**Bottle → Tools → Registry Editor (regedit)**

![bottles](images/bottles8.png)


Click on the Registry menu and `Import Registry File...`

![bottles](images/bottles10.png)

Choose the webview2.reg file that you downloaded earlier.


![bottles](images/bottles11.png)

After the import completes, close the registry.



### 6. Install dependencies

1. Open the `Dependencies` on the options category

![bottles](images/bottles12.png)

2. Install the below dependencies by clicking on the name in the list:
    - `dotnetcoredesktop9`
    - `vcredist2015`
    - `vcredist2022`

![bottles](images/bottles13.png)


### 7. Launch Daybreak inside Bottles

1. Add `Daybreak.exe` as a program via the `+ Add Shortcuts...` button
2. The `Daybreak.exe` will be in the `drive_c/daybreak/` folder you created earlier.
3. Launch it

You should now get:

- ✔ Proper UI instead of white blank screen
- ✔ Working WebView2 runtime
- ✔ Normal Daybreak functionality

## Why this works

- WebView2 installers rarely function under Bottles
- Extracting the runtime bypasses MSI failures
- Registry keys trick Daybreak into detecting WebView2
- GPU fallback avoids Wine WebView compositor errors

## Result

Daybreak works correctly under Bottles without requiring Lutris or Faugus.

