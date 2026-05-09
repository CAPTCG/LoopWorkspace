# EversenseKit Test Build

## Instructions & What's New

---

## Part 1 — Build Instructions

There are two ways to build and install the app on your iPhone. Choose whichever suits you best. Both methods produce an identical app.

---

### Method A — Browser Build (No Mac Required)

This method builds the app entirely in your web browser using GitHub Actions and delivers it to your iPhone via the TestFlight app. You can use any computer, tablet, or iPad — no Mac needed.

#### Before You Start
- A free GitHub account — create one at github.com if you don't have one
- A paid Apple Developer account ($99/year) — needed to distribute via TestFlight
- The TestFlight app installed on your iPhone

#### Step 1 — Fork the Repository
- Sign in to GitHub in your browser
- Go to: github.com/CAPTCG/LoopWorkspace
- Click the **Fork** button (top right) and fork it to your own GitHub account
- Make sure the `feat/eversense` branch is selected in your fork

#### Step 2 — Add Your Secrets
GitHub Actions needs six Secrets from your Apple Developer account to sign and deliver the app. In your forked repository go to **Settings → Secrets and Variables → Actions** and add each of the following:

- `TEAMID` — your 10-character Apple Developer Team ID
- `FASTLANE_ISSUER_ID` — from App Store Connect → Keys
- `FASTLANE_KEY_ID` — from App Store Connect → Keys
- `FASTLANE_KEY` — the full contents of your .p8 key file
- `GH_PAT` — a GitHub Personal Access Token with repo and workflow scopes
- `MATCH_PASSWORD` — any strong password you choose (used to encrypt certificates)

#### Step 3 — Run the Actions
In your forked repository, go to the **Actions** tab and run each action in order:

- **Action 1: Validate Secrets** — confirms your secrets are correct
- **Action 2: Add Identifiers** — registers the app with Apple
- **Action 3: Create Certificates** — generates signing certificates (first time only)
- **Action 4: Build Loop** — builds the app and sends it to TestFlight (~25 minutes)

#### Step 4 — Install via TestFlight
- Open the TestFlight app on your iPhone
- The Loop build will appear once Apple has processed it (allow up to 30 minutes after the build completes)
- Tap **Install**

#### Step 5 — Add Your Eversense CGM
- Open Loop on your iPhone
- Go to **Settings → CGM**
- Select **Eversense** and follow the on-screen setup to connect your transmitter and enter your DMS account credentials

---

### Method B — Xcode Build (Mac Required)

This method builds the app directly on your Mac using Xcode and installs it straight to your iPhone.

#### Before You Start
- A Mac with Xcode installed
- An Apple Developer account signed in to Xcode
- An iPhone connected to your Mac with a USB cable

#### Step 1 — Clone the Repository
Open the Terminal app on your Mac and paste this command:

```bash
cd ~/Downloads
git clone --recurse-submodules -b feat/eversense \
  https://github.com/CAPTCG/LoopWorkspace.git
```

This will download everything needed. It may take a few minutes.

#### Step 2 — Open in Xcode
Paste this command into Terminal:

```bash
open ~/Downloads/LoopWorkspace/LoopWorkspace.xcworkspace
```

#### Step 3 — Set Your Development Team
- In Xcode, click on **Loop** in the left sidebar
- Select each target (Loop, Loop Status Extension, etc.) and under **Signing & Capabilities** choose your Apple Developer account from the Team dropdown

#### Step 4 — Connect Your iPhone
- Plug your iPhone into your Mac
- Select your iPhone from the scheme dropdown at the top of Xcode
- Trust the Mac on your iPhone if prompted

#### Step 5 — Build and Install
- Press **⌘R** (or click the Play button) to build and install
- The app will launch on your iPhone when the build completes

#### Step 6 — Add Your Eversense CGM
- Open Loop on your iPhone
- Go to **Settings → CGM**
- Select **Eversense** and follow the on-screen setup to connect your transmitter and enter your DMS account credentials

---

## Part 2 — What's New

We have added several new features to the Eversense plugin that bring it in line with the official Android app.

### 1. Transmitter Battery
The transmitter battery percentage is now shown on the Loop home screen status area and in the Eversense settings screen, so you always know when your transmitter needs charging.

### 2. DMS Portal Sync
After every glucose reading, the app now automatically uploads your data to the Eversense DMS web portal — the same portal sync that the official Android app performs. This means your clinician or care team can see your data on the portal in real time. For this to work, your DMS account username and password must be entered during setup.

Three things are uploaded after each reading:
- Your latest glucose value, trend arrow, signal strength, and battery level (updates the "Last Sync" date on the portal)
- Your glucose history (populates the Sensor Glucose table)
- Device diagnostic logs (required by Senseonics)

### 3. Alarms
The app now correctly receives and handles push alarms from the transmitter (for example, high/low glucose alerts), matching the behaviour of the Android app.

### 4. Transmitter Not Placed Detection
If the app detects that the transmitter is not properly placed on the sensor (three consecutive failed connection attempts), it will now notify Loop — consistent with how the Android app handles this.

### 5. Diagnostic Mode for Sensor Placement
When you go through the sensor placement guide in the app, it now automatically puts the transmitter into diagnostic mode — the same way the Android app does — to assist with accurate placement detection.

---

## Reporting Issues

Please open an issue in this repository or contact Craig directly with:
- A description of any unexpected behaviour
- Which feature it relates to (from the list above)
- Which build method you used (Browser or Xcode)
- Your iPhone model and iOS version
- Your Xcode version if applicable (Xcode → About Xcode)
