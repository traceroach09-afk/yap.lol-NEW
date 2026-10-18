# yaps.lol

Run the networked site with Node.js 18 or newer:

```sh
npm start
```

## Linux setup

The project uses Node.js built-in modules only, so it runs on Linux without installing npm packages. Install Node.js 18 or newer using your Linux distribution's package manager or the official Node.js installer. Then open a terminal in this project directory and run:

```sh
node --version
npm start
```

Open [http://localhost:3000](http://localhost:3000). Stop the server with `Ctrl+C`. If you downloaded a ZIP, extract the complete folder first and keep `assets/yaps-logo.png` in place.

Open [http://localhost:3000](http://localhost:3000). To let other devices on the same network use it, open `http://<this-computer's-local-IP>:3000` on those devices while the server is running. The server binds to all network interfaces and stores accounts, profiles, and community templates in `data/db.json`.

## Staff workspace

The creator account `itsmebaked` is always enabled as staff. Additional staff usernames can be added with `YAPS_STAFF_USERNAMES` (comma-separated usernames). The account must already exist in the network database; accounts created by opening files with `file://` are browser-local and cannot access the network staff workspace. Staff usernames cannot be claimed through public sign-up while configured. To add staff accounts on Windows PowerShell:

```powershell
$env:YAPS_STAFF_USERNAMES = "othername,anothername"
npm start
```

On macOS or Linux:

```sh
YAPS_STAFF_USERNAMES="othername,anothername" npm start
```

Staff members sign in to the app and open `/staff.html` (or use the Staff workspace link in the account dashboard). On another device on the same network, open `http://<server-IP>:3000/staff.html` after signing in. The staff panel reads the shared account database, syncs badge assignments and staff activity, and applies account warnings, suspensions, bans, kicks, and removals on the server. Bans block future sign-ins; kicks revoke active sessions; 24-hour suspensions expire automatically. Accounts created by opening `index.html` directly with `file://` stay in that browser and are not part of the network database. The current app does not collect user reports, so the live report queue is empty. The database is a local JSON file, so use persistent storage and HTTPS before exposing it outside a trusted network.

New visitors can create an account from the home page. Passwords are stored as scrypt hashes; profile data and uploaded media are stored in the local JSON database. Keep `data/db.json` private and back it up if you need to retain accounts. This is a lightweight single-machine app and is intended for local/LAN use; put it behind HTTPS and a production database before exposing it publicly.

Opening `index.html` directly with `file://` supports local account creation and login for a private preview. Those accounts and profiles are saved in that browser only. Run `npm start` and use the server URL for network accounts, shared templates, and profile links such as `http://localhost:3000/itsmebaked`. Public profile pages refresh saved changes about every five seconds.

The same commands work on Windows, macOS, and Linux. For a public deployment, configure persistent storage for the `data` directory or move account data to a database; otherwise local database changes may not survive a host restart or redeploy.

## Windows installer

Run `yaps.lol-setup.exe` to install the site under `%LOCALAPPDATA%\yaps.lol` and launch it in your browser at `http://localhost:3000`. The installer requires Node.js 18 or newer on the computer and available on `PATH`. Keep the opened server window running while you use the site; close it to stop the local server. Your account data stays in the installed folder's `data` directory.
