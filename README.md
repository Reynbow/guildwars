# Daybreak Launcher on Linux (Bottles) – Working Installation Guide

### 1. Create a clean bottle for Daybreak

Install bottles via: https://usebottles.com/

It should be available in your package manager for easier install.

In Bottles:

- Create new bottle → type: Gaming (or Custom / Application is fine)
- Architecture: 64-bit
- Windows version: Windows 10 / 11

<div style="position: relative; width: fit-content;">
  <img src="images/bottles.png" alt="bottles" style="display:block;">
  <img src="images/bottles2.png" alt="bottles2" style="position:absolute; top:90px; left:300px;">
</div>
<br>
<br>
<br>
<br>

### 2. Place Daybreak in the bottle

Once created, open the Guild Wars bottle and click on the Browse C:/ drive button:

![bottles](images/bottles3.png)

Create a new folder and name it "daybreak"

<img src="images/bottles4.png"
     alt="bottles"
     style="border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: 0 4px 10px rgba(0,0,0,0.12); border-radius: 6px;">

Download Daybreak from the official github: https://github.com/gwdevhub/Daybreak/releases

Open the downloaded .zip file and extract all the contents in to the daybreak folder you created above.

<div style="position: relative; width: fit-content;">
  <img src="images/bottles5.png" alt="bottles5" style="display:block;">
  <img src="images/bottles6.png" alt="bottles6" style="position:absolute; top:190px; left:500px;">
</div>
<br>
<br>
<br>
<br>

Extract Daybreak into the bottle's path:

```
~/.local/share/bottles/bottles/<YourBottleName>/drive_c/Daybreak/
```

**Verify:**

- `Daybreak.exe` exists inside that folder.

### 3. Download WebView2 Fixed Runtime

From [Microsoft WebView2 downloads page](https://developer.microsoft.com/en-us/microsoft-edge/webview2/):

**Download:**

- ✔ **Fixed Runtime – Evergreen Standalone CAB (x64)** (not the bootstrap installer)

### 4. Extract the CAB into the bottle

Inside your bottle, create:

```
drive_c/Program Files (x86)/Microsoft/EdgeWebView/
```

Extract the CAB contents into this folder.

You should end up with something like:

```
.../EdgeWebView/Microsoft.WebView2.FixedVersionRuntime.143.0.3650.66.x64/
```

(The version number will differ.)

### 5. Register WebView2 in the bottle's Wine registry

Inside Bottles:

**Bottle → Tools → Registry Editor (regedit)**

#### Create detection key #1

Navigate:

```
HKEY_LOCAL_MACHINE
 └ Software
   └ Microsoft
```

Right-click `Microsoft` → New → Key:

- `EdgeUpdate`

Click `EdgeUpdate`:

- Right pane → New → String Value:
  - `pv` = `143.0.3650.66` (use the version number from your folder)
- Right pane → New → DWORD (32-bit Value):
  - `st` = `1`

#### Create detection key #2

Back under:

```
HKEY_LOCAL_MACHINE\Software\Microsoft
```

Right-click → New → Key:

- `EdgeWebView`

Right pane → New → String Value:

- `pv` = `143.0.3650.66`

### 6. Fix rendering failure (prevents white window)

Still in regedit, navigate:

```
HKEY_CURRENT_USER
 └ Software
   └ Microsoft
```

Right-click `Microsoft` → New → Key:

- `Edge`

Inside:

- Right-click → New → Key:
  - `WebView`

Inside:

- Right-click → New → Key:
  - `Rendering`

Select `Rendering` and add:

| Name | Type | Value |
|------|------|-------|
| `DisableGpu` | DWORD | `1` |

This forces WebView2 to render in software mode, which works inside Wine.

### 7. Launch Daybreak inside Bottles

1. Open the bottle
2. Add `Daybreak.exe` as a program
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

