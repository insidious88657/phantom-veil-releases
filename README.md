# Phantom Veil Beta Testing Hub

Welcome to the Phantom Veil Beta! Your testing is paramount to guaranteeing our privacy engine operates identically across thousands of uniquely configured devices.

This repository serves as the official distribution channel for our beta binaries. You **will not** find the source code here, but rather our pre-compiled beta installers alongside comprehensive verification instructions.

## 📦 Downloads

- [**Android APK (v1.0.0)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/phantom-veil-v1.0.0.apk)
- [**Chrome Extension (v1.0.0)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/phantom-veil-chrome-v1.0.0.zip)
- [**Firefox Extension (v1.0.0)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/phantom-veil-firefox-v1.0.0.zip)
- [**macOS (Apple Silicon)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/Phantom.Veil_1.0.0_aarch64.dmg)
- [**Windows Setup (.exe)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/Phantom.Veil_1.0.0_x64-setup.exe)
- [**Windows Installer (.msi)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/Phantom.Veil_1.0.0_x64_en-US.msi)
- [**Linux (AppImage)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/Phantom.Veil_1.0.0_amd64.AppImage)
- [**Linux (.deb)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/Phantom.Veil_1.0.0_amd64.deb)
- [**Linux (.rpm)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/Phantom.Veil-1.0.0-1.x86_64.rpm)

---

## 🛠️ Installation Instructions

### Chrome Extension
1. Download `phantom-veil-chrome-v1.0.0.zip` and extract/unzip the folder.
2. Open Chrome and navigate to `chrome://extensions/`.
3. Enable **Developer Mode** using the toggle in the top right corner.
4. Click **"Load unpacked"** and select the extracted `chrome-mv3` folder.
5. The extension should now be installed and ready! Pin it to your toolbar for easy access.

### Firefox Extension
1. Download `phantom-veil-firefox-v1.0.0.zip` (do not extract it).
2. Open Firefox and navigate to `about:debugging#/runtime/this-firefox`.
3. Click the **"Load Temporary Add-on..."** button.
4. Select the downloaded `.zip` file.
5. The extension is now temporarily installed for your current session!

### Android APK
1. Download `phantom-veil-v1.0.0.apk` directly to your Android device.
2. Tap the downloaded file to install.
3. If prompted, select **"Settings"** and enable **"Allow from this source"** to let your browser/file manager install the app.
4. Launch Phantom Veil to begin.

### Desktop Applications (macOS, Windows, Linux)
1. Download the installer matching your OS from the "Downloads" section above.
2. Note: Because these are unsigned beta builds, your OS may flag them as unrecognized.
   - **Windows:** If Microsoft Defender SmartScreen appears, click **"More info"** -> **"Run anyway"**.
   - **macOS:** If Finder prevents opening the DMG, `Control-click` (or right-click) the application icon and select **"Open"** from the contextual menu.
   - **Linux:** For `.AppImage`, ensure you make the file executable `chmod +x Phantom.Veil_1.0.0_amd64.AppImage` before running.
3. Complete the installation and launch the app.

---

## ✅ Comprehensive Testing Checklist

As you progress through this list, please notify the developer so we can formally check these items off. Below you will find specific instructions on how to verify each feature is working under the hood.

### 🌐 Web Extensions (Chrome & Firefox)

- [ ] **Heuristic Tracker Detection & Basic Blocking**
  - **How to verify:** Navigate to an ad-heavy site like `cnn.com` or `nytimes.com`. 
    1. Open the extension popup: Verify the "Privacy Score Dashboard" updates dynamically and the blocked tracker count increases.
    2. Open the "Audit Feed" in the extension menu: Ensure it populates with requests in real-time.
    3. Check the Engine: Go to `chrome://extensions/` (or `about:debugging` in Firefox), find Phantom Veil, and click `background.js` (or "Inspect" in Firefox) to open its DevTools Console. Look for ML model detection logs.
    4. General Network check: In the website's devtools Network tab, you should see requests to known endpoints (like `google-analytics`) blocked by the client (colored red in Chrome).

- [ ] **Aggressive Protection Mode**
  - **How to verify:** Open the Extension Settings and toggle "Aggressive Protection Mode". 
    1. Check the Service Worker console again: You should see a log demonstrating `declarativeNetRequest` rules updating dynamically (e.g. `VeilMode = Aggressive`).
    2. Try browsing normal sites and report any broken website functionality to ensure aggressive blocking isn't destructive.

- [ ] **Decoy Traffic Generation**
  - **How to verify:** Toggle Decoy Traffic ON in the settings. 
    1. In the extension's Service Worker console, observe the logs—you should see periodic notifications that phantom/harmless background requests are being executed against well-known CDN domains to obscure your footprint.

- [ ] **Cross-Device Mesh Messaging (E2E Encrypted)**
  - **How to verify:** Open the extension's `CommsPanel`. Open the Android App on another device.
    1. Ensure the WebSocket relay connects successfully.
    2. Exchange chat messages between the extension and the Android app. 
    3. Verify network latency feels acceptable and messages encrypt/decrypt visually if logs permit.

- [ ] **Cross-Device P2P Media (Voice & Video Calling)**
  - **How to verify:** Using the `CallsPanel` in the extension, initiate a call with your Android app.
    1. Ensure Chrome prompts you for Microphone/Camera permissions.
    2. Verify the WebRTC connection establishes successfully and audio/video feeds are stable.

### 📱 Android Application

- [ ] **Successful Installation & Boot**
  - **How to verify:** Ensure the app does not crash upon opening. Verify UI layouts scale properly for your screen size.

- [ ] **Cross-Device Mesh Messaging (Receiver & Sender)**
  - **How to verify:** Use the messaging dashboard to communicate with a connected Chrome Extension. 
    1. Test sending long strings of text.
    2. Force close the app and reopen it to ensure the state or WebSocket relay handles disconnection gracefully.

- [x] **P2P Voice Calling (Android ↔ Android) ✅ VERIFIED**
  - **Status:** Fully tested and working as of April 9th, 2026.
  - **What was verified:**
    1. Voice calls connect successfully between two Android devices (Samsung Galaxy & Moto G).
    2. Bidirectional audio confirmed — both caller and receiver hear each other clearly.
    3. Incoming call modal displays with Accept/Decline buttons on the receiving device.
    4. Call termination propagates correctly to both sides when either party hangs up.
    5. Call history is recorded on both devices.
    6. TURN relay (Metered.ca) successfully routes media through carrier-grade NAT.
  - **Known limitations:**
    - Screen sharing (`getDisplayMedia`) is not available in Android WebView — shows a friendly error.
    - Video calling UI is present but not yet verified with front-facing camera streams.

- [ ] **P2P Video Calling (Camera Streams)**
  - **How to verify:** Accept an incoming video call from another device.
    1. Verify Android correctly asks for runtime permissions for the Camera and Microphone.
    2. Ensure the camera orientation is correct and video feed is stable.
    3. Test muting your microphone and toggling video on/off.

### 💻 Desktop Applications (macOS, Windows, Linux)

- [ ] **System Installation & Integration**
  - **How to verify:** Install the application locally.
    1. Verify the application installs correctly into the Applications/Program Files directory.
    2. Verify the uninstaller correctly cleans up the files if testing on Windows/Linux.

- [ ] **Cross-Device Mesh Messaging**
  - **How to verify:** Open the desktop app and communicate with either the Android or Chrome Extension instance.
    1. Ensure the UI feels responsive outside of the browser context.
    2. Check for native OS notifications on incoming messages (if supported).

- [ ] **P2P Media (Camera & Mic Routing)**
  - **How to verify:** Start a call from the Desktop App to the Android App.
    1. Check OS privacy settings to ensure the Desktop App explicitly requests access to your Camera and Microphone.
    2. Try changing your audio or video source within the desktop app (if settings exist) and ensure the WebRTC stream updates.

---

*Thank you for helping us solidify Phantom Veil! Your testing logs and bug reports are invaluable to the privacy mesh.*
