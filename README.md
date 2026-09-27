# MicroPad

**Your Codex sessions, one key away.**

MicroPad is a Windows companion that puts your AI coding sessions on a clickable on-screen keyboard or a compatible physical macropad. Each assigned key opens its session, and its color shows whether that session is working, finished, or waiting for you.

You can use several keyboards at once, each with its own sessions. **You do not need a physical keyboard to use MicroPad.**

This public repository contains the portable application and this guide. The source project is private. MicroPad is an independent project, not an official OpenAI product.

## Download and start

**[Download MicroPad.exe for Windows 11 — Intel/AMD 64-bit](https://github.com/zeuzere/MicroPad/releases/latest/download/MicroPad.exe)**

1. Save `MicroPad.exe` in a folder you want to keep.
2. Double-click it. No installer or separate .NET installation is needed.
3. Look for MicroPad in the Windows system tray, near the clock. You may need to open the hidden-icons arrow.
4. Right-click its tray icon and choose **Keyboards → My keyboard**, or **Show all**.
5. Start a local Codex session. Right-click a key, choose **Edit key**, then **Assign session**. If the key has no session slot yet, choose **Add session key** first.
6. Click the assigned key to return to that session.

**A fresh installation starts in the tray only.** To open a keyboard automatically, enable **Open on application start** in that keyboard's settings.

Run only one MicroPad copy at a time. Codex must be installed and have local sessions for MicroPad to monitor. This download is the x64 build; it is not a native ARM64 release.

## What MicroPad can do

- Open a session with a mouse click or a physical key press.
- Show session status with colored overlays and supported physical key LEDs.
- Assign sessions manually, automatically, or with a mix of both.
- Pin a session so automatic assignment does not replace it.
- Swap the sessions assigned to two keys.
- Run multiple virtual keyboards and supported physical keyboards independently.
- Load keyboard profiles containing a layout, artwork, and key overlays.
- Put individual session keys in the Windows system tray.
- Remember assignments, profiles, pins, colors, and startup preferences.
- Check for new portable versions and optionally install them automatically.

## Everyday controls

| Action | What it does |
| --- | --- |
| Click an assigned on-screen key | Open its session. |
| Right-click a key → **Edit key** | Assign a session, pin or release it, enable its tray icon, or remove its session slot. |
| Right-click → **Keyboard settings** | Open the editor for that keyboard. Its name appears at the top. |
| Right-click → **Open → another keyboard** | Show another keyboard window. |
| Right-click → **Settings** | Open session mode, state colors, and application settings. |
| Drag the keyboard background | Move the keyboard. |
| Drag the settings/editor title bar | Move that window independently. |
| **Hide to tray** | Hide the keyboard while MicroPad keeps running. |
| **Exit MicroPad** | Stop the application. |

The **Open** submenu is hidden when there is only one keyboard. It refreshes when you right-click, so added, renamed, or removed keyboards appear correctly without restarting.

An unassigned key does not open a session. Right-click it to configure it. Closing a keyboard hides it; it does not quit MicroPad. Escape cancels a pending swap or closes the active editor/panel, and otherwise hides the keyboard.

### Swap two sessions with the mouse

1. Hold **Ctrl** and click the first configured key. It gets an outline.
2. Click the second configured key on the same keyboard. You may keep Ctrl held.
3. The sessions, saved destinations, and pins exchange places.

Press Escape or click the first key again to cancel. Physical key mappings and tray-icon preferences stay with their original keys. Automatic slots may subsequently change as session activity changes; use Manual mode or Hybrid pins for fixed assignments.

## Physical keyboard controls

The current physical integration is for the **wired DOIO KB16-01 Rev2 with compatible MicroPad LED firmware**. Stock firmware and other QMK devices are not automatically supported. MicroPad does not install firmware or program your keymap.

1. Configure the pad's session keys as unique **F13–F24** keys on its base layer using your keyboard's configuration tools.
2. Close VIA or any other tool using its HID connection.
3. Open **Keyboard settings**, select the device under **Hardware connection**, and click **Save keyboard**.
4. Use **Read and save keyboard layout** to read its current mapping when connected.

| Physical action | What it does |
| --- | --- |
| Tap a mapped key | Open the assigned session when you release the key. |
| Hold one key for about 2 seconds | Bind the current session in Manual mode, or bind and pin it in Hybrid mode. |
| Hold an already pinned key for about 2 seconds | Release that key back to automatic assignment in Hybrid mode. |
| Hold two mapped keys together for about 2 seconds | Swap their sessions on that keyboard. |

Binding uses the app/session currently in the foreground. When MicroPad can identify a unique session, it binds directly. Otherwise, it opens a session picker. Cancelling the picker keeps the previous binding. Pure Automatic mode does not allow manual binding.

F13–F24 provides up to **12 distinct physical session shortcuts per device**. The current input adapter handles the 16 main pads; physical knob presses and rotation are not integrated. Windows can still deliver these F-keys to the foreground app, so avoid assigning conflicting shortcuts there.

If the selected device is disconnected or busy, the keyboard remains usable on screen. Reconnecting the same available device resumes physical operation. Moving a device without a unique USB serial number to another USB port may require selecting it again.

## Manual, Automatic, and Hybrid

Choose a mode in **Settings → Sessions** for the keyboard whose settings you opened.

| Mode | Best for | Behavior |
| --- | --- | --- |
| **Manual** | Fixed assignments | Choose which session each key opens. |
| **Automatic** | Following your recent work | Available keys follow the most recently active, confirmed-open main sessions. |
| **Hybrid** | A mix of fixed and automatic keys | Unpinned keys update automatically; pinned keys keep their sessions. |

Automatic capacity depends on the number of configured session slots, not a fixed six-key limit. Subagent sessions are excluded. In Hybrid mode, manual assignment pins the selected session. You can also use **Pin this session** or **Release to automatic** in the key editor.

When MicroPad confirms a session has closed, it clears that binding. Automatic and unpinned Hybrid slots can take a replacement; Manual slots remain unassigned. A finished or idle session is not the same as a closed session. If MicroPad cannot confidently determine whether a session is still open, it preserves its existing assignment.

## Understand the colors

| Status | Default color | Meaning |
| --- | --- | --- |
| **Working** | Blue | The agent is running. |
| **Ready** | Green | A completed response has not yet been acknowledged as viewed. |
| **Needs input** | Amber | The available session data indicates it is waiting for you. |
| **Error** | Red | The session reported an error. |
| **Idle** | Gray | The session is inactive or its completed response has been viewed. |
| **Unknown** | Dark gray | MicroPad cannot confidently determine its status. |
| **Binding accepted** | Brief white flash | A binding, release, or swap succeeded. |

Opening a completed session through its key acknowledges it. Other viewed-state detection depends on the target app and the information available to MicroPad.

To change colors, open **Settings → State colors**. Type a `#RRGGBB` value, or choose a color with the wheel and brightness slider. The wheel also accepts typed hex values. **Use color** updates the draft; **Save all colors** applies the whole palette at once. Unsaved edits remain drafts and are lost when the app exits.

Colors and appearance preferences are shared across keyboards. You can also turn status LEDs, F-key labels, and the Working pulse on or off, and change overlay intensity in the keyboard editor. These appearance controls apply to all keyboards.

## Multiple keyboards and profiles

A **profile** describes how a keyboard looks: its layout, image, and key overlays. A **keyboard** is a configured instance with its own name, assignments, mode, startup choice, and optional physical device.

You can use the same profile for several keyboards without sharing their session assignments, or use a different profile for each one.

Open **Keyboard settings** from the keyboard's right-click menu. The editor always belongs to the named keyboard; there is no keyboard-selection dropdown on that page.

- **Add keyboard:** create another keyboard with one session slot initially.
- **Import profile:** load a compatible MicroPad Layout Lab version 1 JSON profile. A raw QMK JSON alone is not an importable MicroPad profile; the profile must also contain its visual information. The bundled profile works without importing anything.
- **Layout profile:** choose the appearance for this keyboard.
- **Hardware connection:** choose **Virtual only** or a supported physical device.
- **Save keyboard:** save its name, profile, and device selection.
- **Add selected key:** enable another session slot from the profile. You can also right-click an unmapped key and choose **Edit key → Add session key**.
- **Remove this keyboard:** remove that instance and its assignments after confirmation. At least one keyboard must remain.
- **Delete selected profile:** delete an unused saved profile after a warning. First change any keyboards using it to another profile. Your original imported JSON file is kept, and the last remaining profile is protected.

Virtual session slots are limited by the imported profile's keys rather than F13–F24; profiles currently support up to 512 keys. Profile artwork supports embedded PNG/JPEG images; WebP depends on the Windows image decoder. Changing a profile that removes assigned keys prompts before those assignments are removed.

The app can import visual profiles, but a full image-and-overlay design editor is not included in this release. The keyboard settings editor configures existing profiles and instances.

## Startup and the system tray

A single left-click on the main tray icon shows the selected keyboard. Right-click opens its menu.

The main tray menu contains:

- **Keyboard settings → keyboard name:** edit that keyboard, even while its on-screen keyboard is hidden.
- **Settings:** open the settings for the most recently active keyboard.
- **Keyboards → keyboard name:** show a keyboard.
- **Keyboards → Show all / Hide all:** show or hide all keyboard windows.
- **Check for updates:** check GitHub for a newer portable version.
- **Exit:** stop MicroPad.

Each keyboard's **Open on application start** checkbox saves immediately. Only checked keyboards open when MicroPad launches. If none are checked, it starts in the tray only. Showing or hiding a keyboard during use does not change this preference.

**Settings → App → Start with Windows** controls whether MicroPad itself launches when you sign in. Keep the executable in its chosen location if you enable this. The App page also offers always-on-top, centering, hiding, diagnostics, and restart as administrator.

### Light and dark appearance

In **Settings > App > Appearance**, choose **System**, **Dark**, or **Light**. System is the default and follows the Windows app theme, including changes made while MicroPad is running.

The choice applies to settings, keyboard editing, color selection, and menus, including the main system tray menu and each session icon's menu. Changes apply immediately and are saved for the next launch. Keyboard images, overlay colors, and session state colors keep their own appearance.

### Individual session tray icons

Right-click a key → **Edit key** → enable **Show this key in system tray**. Its icon displays the key label and state color; hover for the session details, and click to open the session. Right-click the icon → **Hide from tray** to remove it and uncheck that preference. The session binding remains intact.

Windows may initially put these icons in its hidden-icons area.

## Supported apps and current limits

- **Codex is the current session provider.** Claude Code, Pi, Herdr, and other agents are not integrated yet.
- Sessions must be available in local Codex data. Cloud-only sessions without local data are not monitored.
- Codex Desktop assignments open the saved session. Physical hold binding can also save a supported application's current window/tab, including Windows Terminal.
- Exact VS Code terminal integration requires the separate **MicroPad Terminal Bridge** extension. That extension is not included in this executable-only download.
- App/tab capture depends on what Windows accessibility exposes. Rebind after closing or replacing the target tab, restarting its app, or reloading the VS Code extension. MicroPad avoids guessing a replacement based on its title.
- State detection is based on available local session data. Some approval prompts or questions may not appear there; colors can lag or show Unknown. Local data formats can change between Codex versions.
- Knob Model/Reasoning settings can be saved, but turning a knob does **not** change the live model or reasoning level in this release.
- A profile for another keyboard enables its virtual appearance; it does not add physical input or LED support for that hardware.

## Updates, saved data, and removal

### Built-in portable updates

Starting with version **1.1.0**, portable MicroPad checks GitHub Releases for updates. **If you have an older copy, download the current executable once to get this feature.** Normal development builds do not use the updater.

Under **Settings → App**, you can choose:

- **Check for updates automatically** — on by default. Checks at startup and every six hours. If you are offline, MicroPad continues working.
- **Install updates automatically** — off by default. When enabled along with automatic checking, downloads and installs new versions when no binding, navigation, or open editor needs your attention.
- **Check for updates** — check now. The same action is in the tray menu.

When a new version is found, a tray notification lets you review it. Choose **Update now** or **Later**. The update downloads while the app is still running; its version, size, and SHA-256 checksum must match the GitHub release before installation.

MicroPad then closes, replaces its executable, and restarts from the same location with the keyboard windows you had open. Saved settings remain intact. The previous executable is kept beside it as `MicroPad.exe.previous` (or your executable's name followed by `.previous`). If replacement fails, the old executable remains; if the new version fails to start, the updater attempts to restore and relaunch the previous one and reports the problem. A failed update is not retried automatically over and over; use a manual check to retry.

The executable's folder must be writable. The updater does not silently request administrator access. Downloaded files and update logs are kept under the local settings folder's `Updates` directory; completed download/helper executables are cleaned up after startup. Updates contact GitHub for public release information and downloads; they do not upload your session settings.

Manual updating still works: choose **Exit**, download the new executable, replace your old copy, and launch it again. Keep the same path if you use Start with Windows.

Portable means no installation is required. Settings are stored on the computer, not inside the executable, under:

```text
%LOCALAPPDATA%\MicroPadPortable
```

The main files are `keyboard-workspace.json` for keyboards, assignments and preferences, and `keyboard-workspace-read.json` for viewed-state tracking. Exit MicroPad before backing up this folder. Copying only the executable to another PC does not carry your settings; device and app/tab bindings may need to be recreated there. The bundled runtime may extract files to Windows' temporary .NET cache.

This public download does not include anyone's personal settings or sessions. Your own settings can contain session names, IDs, and saved app destinations; keep backups private.

To remove MicroPad, turn off **Start with Windows** if enabled, choose **Exit**, and delete the executable. Delete its local settings folder only if you also want to discard your saved configuration.

## Troubleshooting

| Problem | Try this |
| --- | --- |
| Nothing appears after launch | Open the hidden tray icons, then **Keyboards → Show all**. Tray-only startup is normal when no keyboards are checked. |
| “Already running” | Open the existing tray instance, or exit it before launching another copy. |
| Cannot install an update | Check internet access, disk space, and permission to write to the executable's folder. The app keeps the previous executable. Use **Check for updates** to retry or download manually. |
| No sessions appear | Start Codex locally and send a first prompt. Check that its local session data is available under the current Windows account. |
| A click does nothing | Check that the key has a session assigned. An empty key needs a session slot and an assignment. |
| A hold opens a session picker | Automatic identification was unavailable or ambiguous. Select the intended session manually. |
| A key opens an old or unavailable destination | Bind it again with the correct session/tab in the foreground. |
| Cannot manually assign a key | Switch that keyboard from Automatic to Hybrid or Manual. |
| The physical keyboard is unavailable | Check the selected device, compatible firmware, USB connection and base layer. Close VIA. Virtual use remains available. |
| Keyboard shortcuts conflict | Remove conflicting F13–F24 shortcuts from the foreground application. |
| A window will not come to the foreground | Check whether the target app runs as administrator. MicroPad has an administrator restart option when needed. |
| LEDs remain after a crash | Reconnect the keyboard. Normal exit attempts to restore the previous LED state, but crash recovery is limited by its firmware. |

Use **Settings → App → Show diagnostics** when reporting a problem. Include what you expected, what happened, your Windows version, and whether you used a virtual or physical keyboard. Review diagnostic details before posting them publicly.
