# Phantom Veil Beta Testing Hub

Welcome to the Phantom Veil Beta! Your testing is paramount to guaranteeing our privacy engine operates identically across thousands of uniquely configured devices.

This repository serves as the official distribution channel for our beta binaries. You **will not** find the source code here, but rather our pre-compiled beta installers alongside comprehensive verification instructions.

## 📦 Downloads

- [**Android APK (v1.0.0)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/phantom-veil-v1.0.0.apk)
- [**Chrome Extension (v1.0.0)**](https://github.com/insidious88657/phantom-veil-releases/releases/download/v1.0.0/phantom-veil-chrome-v1.0.0.zip)

---

## 🛠️ Installation Instructions

### Chrome Extension
1. Download `phantom-veil-chrome-v1.0.0.zip` and extract/unzip the folder.
2. Open Chrome and navigate to `chrome://extensions/`.
3. Enable **Developer Mode** using the toggle in the top right corner.
4. Click **"Load unpacked"** and select the extracted `chrome-mv3` folder.
5. The extension should now be installed and ready! Pin it to your toolbar for easy access.

### Android APK
1. Download `phantom-veil-v1.0.0.apk` directly to your Android device.
2. Tap the downloaded file to install.
3. If prompted, select **"Settings"** and enable **"Allow from this source"** to let your browser/file manager install the app.
4. Launch Phantom Veil to begin.

---

## ✅ Comprehensive Testing Checklist

As you progress through this list, please notify the developer so we can formally check these items off. Below you will find specific instructions on how to verify each feature is working under the hood.

### 🌐 Chrome Extension

- [ ] **Heuristic Tracker Detection & Basic Blocking**
  - **How to verify:** Navigate to an ad-heavy site like `cnn.com` or `nytimes.com`. 
    1. Open the extension popup: Verify the "Privacy Score Dashboard" updates dynamically and the blocked tracker count increases.
    2. Open the "Audit Feed" in the extension menu: Ensure it populates with requests in real-time.
    3. Check the Engine: Go to `chrome://extensions/`, find Phantom Veil, and click `background.js` (or Service Worker) to open its DevTools Console. Look for ML model detection logs.
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

- [ ] **P2P Video & Voice Calling (Permissions & Negotiation)**
  - **How to verify:** Accept an incoming call from the Chrome Extension.
    1. Verify Android correctly asks for runtime permissions for the Camera and Microphone.
    2. Ensure audio plays through the correct speaker and the camera orientation is correct.
    3. Test muting your microphone and ensuring the Desktop extension stops receiving audio.

---

*Thank you for helping us solidify Phantom Veil! Your testing logs and bug reports are invaluable to the privacy mesh.*
