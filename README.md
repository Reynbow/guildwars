# Daybreak Launcher on Linux (Bottles) – Working Installation Guide

### 1. Create a clean bottle for Daybreak

Install bottles via: https://usebottles.com/

It should be available in your package manager for easier install.

In Bottles:

- Create new bottle → type: Gaming


![bottles2](images/bottles2.png)

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

