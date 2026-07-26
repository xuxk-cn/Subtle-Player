# Subtle Player (Weiying) User Manual

> **Subtle Player / 微影 (Weiying)** — A "low-profile" local video player designed for discreet viewing at work.
> Core value: **Hide fast, restore fast, stay out of the way**.

---

## 1. Product Overview

### 1.1 What is Subtle Player?

Subtle Player is not a traditional cinema-grade video player. It solves a very specific use case:

- You want to keep a video playing in the background while you code, edit documents, or reply to messages
- You want the player to stay unobtrusive, not steal focus, and not draw immediate attention
- When someone approaches or before you share your screen, the player can hide and mute itself faster than you can react manually

In one sentence: **This is a discreet-viewing tool whose core strengths are quick stowage, low visual presence, and seamless restoration.**

### 1.2 Technical Architecture

Subtle Player uses a dual-window architecture: "Console + Independent Playback Window":

| Layer | Technology | Description |
|---|---|---|
| Desktop Container | Electron 37+ | Handles windows, tray, shortcuts, and auto-hide logic |
| Playback Backend | mpv.exe (JSON IPC communication) | Handles actual video decoding and playback with excellent performance |
| UI | Native HTML/CSS/JS | Lightweight console with zero framework dependencies |
| Face Detection | Chromium FaceDetector API | **Runs 100% locally; no images are uploaded** |
| License Encryption | AES-256-GCM | End-to-end encrypted license files |

### 1.3 Editions & Pricing

| Edition | Description | Price |
|---|---|---|
| **Free Trial** | Full features for 7 days after first launch (equivalent to Standard) | Free |
| **Standard** | Unlocks mouse/keyboard input auto-hide | ¥19.90 / $9.99 |
| **Pro** | Standard + camera face detection auto-hide | ¥79.00 |

> During the trial period you can experience all core capabilities including auto-hide, resume playback, window snapping, playback speed control, etc. If not activated after the trial expires, the auto-hide feature will be disabled; only basic playback and manual hide remain available.

---

## 2. Quick Start

### 2.1 First Launch

After you double-click and run the program:

1. **System tray icon appears** — The Subtle Player icon shows up in the bottom-right taskbar; right-click for a quick menu
2. **Console window opens** — This is your control center (NOT the playback window!)
3. **7-day trial starts automatically** — No registration required; enjoy full Standard Edition features immediately
4. **mpv playback engine auto-detection** — The program automatically searches for a usable mpv.exe

### 2.2 Play Your First Video

There are 4 ways to open a video:

| Method | Action |
|---|---|
| **Button** | Click "Open Video" at the top of the console |
| **Shortcut** | Press `Ctrl + Alt + O` |
| **Tray Menu** | Right-click the tray icon → Open Video |
| **Recent Files** | Click a history entry in the "Recent" column of the console |

After opening, the mpv independent playback window pops up and starts playing.

### 2.3 Core Keyboard Shortcuts (Global)

The following shortcuts work anywhere, regardless of which window is focused:

| Shortcut | Function | Notes |
|---|---|---|
| `Ctrl + Alt + H` | **Hide / Restore** the playback window | The most frequently used "panic key" |
| `Ctrl + Alt + O` | Open a video file | Opens the file picker dialog |
| `Ctrl + Alt + P` | Play / Pause | Toggles playback state |
| `Ctrl + Alt + M` | Mute / Unmute | One-click mute |
| `Ctrl + Alt + S` | Open Settings panel | Preference configuration |

> **Important**: When you press the shortcut combinations above, the program executes the corresponding action and **will NOT trigger auto-hide**. All other regular keys will still trigger input-based auto-hide.

---

## 3. Core Features in Detail

### 3.1 🔥 Auto-Hide (The Defining Differentiator)

This is Subtle Player's most important feature. There are two automatic trigger modes:

#### Mode 1: Mouse / Keyboard Input Trigger (Enabled by default, Standard Edition and above)

**Trigger conditions** (all must be true simultaneously):
- Video is currently playing (not paused)
- "Auto-hide on mouse/keyboard input" is enabled in Settings
- License status is valid (in trial / activated Standard or above)
- Not within the cooldown period

**Trigger actions**:
1. mpv playback window **disappears immediately**
2. Audio **mutes instantly**
3. Optionally pauses playback depending on your settings

**Detection mechanisms**:
- **Mouse movement**: Cursor position is polled every 16 ms; any detected movement triggers the action
- **Keyboard input**: A PowerShell subprocess calls Win32 `GetAsyncKeyState` to listen to global keyboard events (excluding modifier keys Ctrl/Alt/Shift/Win); any non-modifier keypress triggers the action

**Cooldown period** (debounce protection):
- Default 1.2 seconds, adjustable in Settings to 0.8 / 1.2 / 2.0 / 3.0 seconds
- After hiding, re-triggering is suppressed briefly to avoid being immediately hidden again after restore

#### Mode 2: Camera Face Detection Trigger (Must be enabled manually, Pro Edition — under development)

**Privacy commitments**:
- ❌ No images or feature vectors are ever uploaded to any server
- ❌ No camera frames are saved to disk
- ❌ The camera is never silently enabled in the background
- ✅ All detection runs entirely within the local Chromium engine
- ✅ Only a binary "Owner / Non-owner" classification is performed

**How to use**:
1. Settings → Enable "Auto-hide when face detected"
2. For first-time use, click "Enroll Owner" → Face the camera directly for 1-2 seconds
3. The program generates a grayscale facial feature vector (16×16 normalized)
4. When a face appears in the camera frame, it is compared against the owner template
5. **Non-owner face** OR **multiple faces** detected for 2 consecutive frames → Hide immediately

**Detection parameters**:
- Similarity threshold: 0.17 (Euclidean distance)
- Consecutive frame trigger: 2 frames
- Detection interval: Per-frame polling

### 3.2 Quick Restore

After hiding, use any of the following methods to restore — **all state is fully recovered**:

| Restore Method | Action |
|---|---|
| Shortcut | `Ctrl + Alt + H` |
| Console Button | Click the "Restore" button |
| Tray Menu | Right-click tray → Resume last playback / Show Player |

**What gets restored**:
- ✅ Playback window display position
- ✅ Video playback progress (accurate to the second)
- ✅ Volume and mute state
- ✅ Playback speed setting
- ✅ Current video file
- ✅ Pause / Play state (per your settings)

### 3.3 Resume Playback (Bookmark)

The program automatically remembers your playback state (stored in `%APPDATA%/moyu-player/settings.json`):

- **Last file path** — One-click "Resume last playback" after startup
- **Last progress position** — Continues from exactly where you left off
- **Last volume** — 70% (default)
- **Last mute state** — Remembers whether audio was muted
- **Recent files list** — Saves up to 8 history entries with one-click clear

### 3.4 Playback Speed Control

The console offers 6 speed presets:
- 0.5x (Slow)
- 0.75x
- 1x (Normal)
- 1.25x
- 1.5x
- 2x (Fast)

### 3.5 Network Video Playback

Subtle Player also supports playing public network videos from multiple platforms directly — just paste the share link:

**Supported platforms**:
- Douyin (v.douyin.com)
- Xiaohongshu / RED (xiaohongshu.com)
- Bilibili (bilibili.com / b23.tv)
- TikTok (tiktok.com)
- YouTube (youtube.com / youtu.be)
- Instagram (instagram.com)
- Other platforms available by custom request

**How to use**:
1. Click the "Network Video" button at the top of the console
2. Paste the share text or link (Douyin share-codes are supported: e.g. "… https://v.douyin.com/xxx/ Copy this link")
3. Click "Play" to start playback

**Special notes**:
- TikTok uses the TikWM public API specifically to obtain watermark-free direct links (bypasses Cloudflare 403)
- For YouTube / Instagram / TikTok playback, SOCKS5 proxies are automatically converted to HTTP proxies (solves mpv stream-stalling issue)
- Per-platform cookies can be configured (browser export / file import) to play login-required content
- Recent-files history records webpage URLs, not short-lived direct links — keeps history clean and reusable

---

## 4. Console Interface Walkthrough

The console uses a three-column layout + bottom diagnostics area:

### 4.1 Top Hero Bar

```
┌──────────────────────────────────────────────────────────────┐
│ [7-Day Free Trial]  Subtle Player              [In Trial]    │
│ mpv-powered local playback with intelligent auto-hide.       │
│            [Open Video] [Network Video] [Resume Last] [Hide] │
└──────────────────────────────────────────────────────────────┘
```

### 4.2 Left Column: Playback Controls

- **Current File** + **Playback Position** (00:00 / Duration) displayed in real-time
- **Progress slider** — Drag to seek, precision 0.1%
- **Volume slider** — 0-100, default 70
- **Control button row**: Play/Pause · Stop · Replay · Mute · Speed dropdown
- **Status message text** — Displays various real-time status messages

### 4.3 Middle Column: Recent Files + Settings

- **Recent files list** — Up to 8 entries; click to play, one-click "Clear"
- **Settings button** — Opens the full Settings panel

### 4.4 Right Column: License Status

- **Trial days remaining** — Live countdown
- **Action buttons**: WeChat/Alipay ¥19.9 · Enter email · Pay · "I have paid, please send activation code" · Check email for message · Copy license code · Activate · Enter email + activation code · Activate Standard Edition

### 4.5 Bottom: Diagnostics Panel (Collapsible)

- Three buttons: **Refresh / Copy / Log**
- Displayed content: App version, test mode, mpv detected path, recent files count, sample video status, startup log path
- One-click export of full JSON diagnostics file (handy for technical troubleshooting)

### 4.6 Settings Dialog (Ctrl+Alt+S)

**Behavior Settings**:
| Toggle | Default | Description |
|---|---|---|
| Auto-hide on mouse/keyboard input | ✅ On | Core feature |
| Auto-hide when face detected | ❌ Off | Pro Edition — under development |
| Pause playback when hidden | ✅ On | Pauses on hide so progress is not consumed |
| Resume playback when restored | ✅ On | Continues playback automatically on restore |
| Cooldown period | 1.2 seconds | Prevents repeated triggers |
| Window size | Medium | 4 presets: Small / Medium / Large / XL |
| UI Language | Simplified Chinese | Switch between Chinese and English |

**Management section**:
- Export Settings / Import Settings — One-click migration when switching devices
- Detect mpv / Select mpv
- Shortcut list — View descriptions of the 5 default shortcuts

**Owner Recognition section**:
- Enroll Owner / Clear Owner
- Status display: Enrolled / Not enrolled

---

## 5. System Tray Menu

Right-click the Subtle Player icon in the bottom-right corner for quick access to nearly all functionality:

```
Subtle Player (Right-click tray)
├─ Restore Console
├─ Open Video
├─ Resume Last Playback
├─ Open Sample Video
├─ Recent (Up to 8 files, submenu)
├─ Play / Pause
├─ Stop Playback
├─ Replay From Start
├─ Mute
├─ Show Player (mpv window)
├─ Reveal File Location (Locate current video in Explorer)
├─ Settings (submenu)
│   ├─ Window Snap → Top-Left / Top-Center / Top-Right / Center-Left / Center-Right / Bottom-Left / Bottom-Right
│   ├─ Window Size → Small / Medium / Large / XL
│   ├─ Export Settings
│   └─ Import Settings
├─ Detect mpv
├─ Select mpv
├─ Open Startup Log
├─ Export Diagnostics
├─ Purchase (WeChat / Alipay)
├─ Import License File
└─ Quit
```

---

## 6. Window Management

### 6.1 Dual-Window Design

| Window | Responsibility | Notes |
|---|---|---|
| **Console Window** | Settings, controls, status | Standard framed Electron window; closing it quits the application |
| **mpv Playback Window** | Video frame rendering | Borderless, titlebar-less; managed by the independent mpv process |

**Advantages**:
- A playback crash never takes down the console (restore entry always exists)
- Auto-hide only hides the playback window; the console stays ready
- Console can be minimized to taskbar without interrupting viewing

### 6.2 Size Presets

The console offers 4 size tiers:

| Preset | Dimensions |
|---|---|
| Small | 760 × 560 |
| Medium (default) | 920 × 640 |
| Large | 1080 × 720 |
| Extra Large | 1260 × 820 |

### 6.3 Multi-Monitor Safe Fallback

If the previously saved window position is no longer visible (e.g. you unplugged an external monitor), the program automatically:
1. Checks the work area of all connected displays
2. If the old position has zero overlap with any visible area → Discards the stale coordinates
3. Re-positions the window on the primary display using the default size

---

## 7. Troubleshooting

| Problem | Possible Causes | Solution |
|---|---|---|
| **mpv not detected** | mpv.exe is not in standard search paths | Console → Settings → Click "Select mpv.exe" to manually locate it, or place mpv.exe in the `vendor/mpv/` directory |
| **Auto-hide is not working** | Trial period expired / Standard not activated; video is paused; toggle is off; still in cooldown | Check license status → Confirm the video is playing → Verify settings toggle → Wait for cooldown to elapse |
| **Face detection unavailable** | Camera not connected / in use; Chromium FaceDetector API unsupported in this environment; owner template not enrolled | Check Device Manager → Enroll owner first → View detailed status in the diagnostics panel |
| **Video restarts from beginning after restore** | "Resume playback when restored" toggle is off | Settings → Turn on "Resume playback when restored" |
| **Console window cannot be found** | Minimized to taskbar; moved to a monitor that was disconnected | Check the taskbar icon; right-click tray → Restore Console; restart the app (it will automatically fall back to primary display) |
| **Shortcuts have no effect** | Conflict with another app's shortcuts; global registration failed | Close conflicting software; the console buttons still work |
| **Where is the startup log** | Troubleshooting startup issues | Console → Diagnostics → "Log" button; or directly at `%APPDATA%\moyu-player\startup-debug.log` |
| **Exporting diagnostics** | Need to send information to developers for troubleshooting | Diagnostics → "Copy" or "Export" the JSON file |

---

## 8. Tips & Best Practices

1. **Drag the mpv window to a corner of your secondary monitor** and keep your primary display focused on work; watch the video from your peripheral vision
2. **Recommended cooldown: 1-2 seconds** — Too short causes frequent false triggers (e.g. typing right after restore), too long compromises situational readiness
3. **Export settings as a backup** — After finishing configuration, export the JSON immediately for instant migration to a new machine
4. **Ctrl+Alt+H is your fastest panic key** — Developing muscle memory for this is more reliable than any auto-hide mechanism
5. **Face detection is ideal for open-office layouts** — Recommended for scenarios where colleagues frequently walk behind you (enable after enrolling your face)
6. **Snap the console to center-right or bottom-right** — Does not obstruct the core editing area of your IDE
7. **Don't clear your recent files** — Saves you the hassle of navigating the file manager every single time
8. **Suspect mpv is hung?** Tray → Select mpv → Re-specify the path and the playback engine auto-restarts

---

## 9. Privacy & Security Commitments

Subtle Player places extreme emphasis on user privacy by design, especially around facial recognition:

| Activity | Performed? |
|---|---|
| Upload camera footage to any server | ❌ Absolutely never |
| Save camera recordings or screenshots | ❌ Absolutely never |
| Upload facial feature vectors anywhere | ❌ Absolutely never |
| Silently enable the camera in the background | ❌ Always requires an explicit manual toggle click |
| Store full raw images locally | ❌ Only stores a 16×16 normalized grayscale vector |
| Send any usage analytics or telemetry | ❌ No telemetry, no tracking of any kind |
| Read browser history or filesystem indiscriminately | ❌ Only accesses video files the user explicitly chooses |

Trial-period redundancy storage exists solely to deter trial-reset abuse and contains no user identity data — only a timestamp plus cryptographic signature.

---

> **In summary**: Subtle Player does three things exceptionally well —
> ① **Low visual footprint** (dual-window separation + window snapping + size presets)
> ② **Blazing-fast concealment when risk appears** (16ms-grade mouse/keyboard polling + global keyboard hook + instant hide+mute)
> ③ **Pinpoint-accurate restoration once the coast is clear** (100% recovery of progress / volume / file / window state)
>
> This is not just a cute concept toy. It is a genuine "productivity tool for discreet viewing" that you can truly leave running every single day at work.
