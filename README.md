# Butter Chicken

Two-person, end-to-end encrypted chat. Each person runs the app on their own computer and opens it in their own browser at `http://localhost:3000`. Messages are encrypted in your browser before they leave your computer, and your history is stored only on your devices.

This repository contains only what you need to install and run the app. There is no source code to build.

## 1. Requirements

- **Node.js 24.x** (check with `node --version`). Download from https://nodejs.org if needed.
- npm (installed with Node.js).

## 2. Install globally

Download `butter-chicken-1.0.0.tgz` from this repository (click the file, then **Download raw file**), or clone the repository:

```bash
git clone https://github.com/Syed-Samieudeen/butter-chicken-install.git
cd butter-chicken-install
```

Install the app globally from the bundle:

```bash
npm install --global ./butter-chicken-1.0.0.tgz
butter-chicken --version
```

### Windows: if `npm` cannot install globally (permission error)

Use a user-level npm folder instead of system folders. In PowerShell:

```powershell
npm config set prefix "$env:LOCALAPPDATA\npm-global"
$env:Path = "$env:LOCALAPPDATA\npm-global;$env:Path"
npm install --global .\butter-chicken-1.0.0.tgz
butter-chicken --version
```

To keep it working in new terminals, add `%LOCALAPPDATA%\npm-global` to your **user** PATH (Windows Settings → Environment Variables), then reopen the terminal.

If PowerShell blocks the `butter-chicken.ps1` script, run `butter-chicken.cmd` instead, or use Command Prompt.

### macOS / Linux: user-level npm folder

```bash
npm config set prefix "$HOME/.npm-global"
export PATH="$HOME/.npm-global/bin:$PATH"
npm install --global ./butter-chicken-1.0.0.tgz
butter-chicken --version
```

Add the `export PATH=...` line to your shell startup file (`~/.bashrc` or `~/.zshrc`) to keep it.

## 3. Run it once and find your config file

```bash
butter-chicken
```

The terminal prints a **Config file** path and a **Local UI** address (normally `http://localhost:3000`). Leave this terminal open while you use the app. Stop it later with **Ctrl+C**.

## 4. Connect through the Butter Chicken relay

Both you and your friend must use **exactly the same** relay line in your config file.

1. Stop the app with Ctrl+C.
2. Open the **Config file** path printed in step 3 (create it if it does not exist).
3. Add this line (or copy `.env.example` from this repository and use its contents):

   ```dotenv
   BC_CLOUDFLARE_RELAY=butterchickenworker.bakri-downtime-sub.workers.dev
   ```

4. Save the file and run `butter-chicken` again.

## 5. Create your identity

1. Open **http://localhost:3000** in your browser (this is your own computer only).
2. Create your identity with your name and a strong passphrase (at least 12 characters). **There is no account recovery.** Keep the passphrase safe.
3. Never copy another person's data folder or keys. Each person creates their own identity.

## 6. Pair with your friend (once)

1. Person A: **Pair devices** → **Create invitation**. Send the complete invitation text or QR code to Person B privately. It expires in 10 minutes.
2. Person B: **Pair devices** → paste the invitation (or scan the QR) → **Connect to friend**.
3. Both of you compare **every group** of the security code on a trusted channel (call or in person). Only continue if they match.
4. Both people choose **I verified the code**.
5. Send a test message in each direction.

Keep the app running and unlocked on both computers to receive messages. Messages sent while your friend is offline are kept encrypted on your computer and delivered when they come back online.

## Updating

When a new `butter-chicken-*.tgz` is published:

```bash
npm install --global ./butter-chicken-<new-version>.tgz
```

Your history and identity are kept in your user data folder, which the install does not change. Back up that folder while the app is stopped if you want a copy.

## Troubleshooting

- **`butter-chicken` not found:** open a new terminal. Check the PATH steps above, or run `npm prefix -g` to find where npm installs global commands.
- **Internet shows "relay offline":** check that the config line matches exactly on both computers, the app was restarted, and your internet connection works.
- **Friend offline:** both apps must be running and unlocked.
- **Identity changed warning:** stop and confirm with your friend before doing anything else.
- **Port 3000 in use:** set `BC_UI_PORT` to another port in the config file.
- **Stopping:** Ctrl+C in the terminal running `butter-chicken`.

## Privacy and security

- Messages are encrypted on your device. The relay only forwards and temporarily stores encrypted data.
- The relay URL is public configuration. It is not a password, and it does not contain your identity.
- This is not an audited product. It has no forward secrecy. Malware or someone with access to your unlocked computer can read your messages.
