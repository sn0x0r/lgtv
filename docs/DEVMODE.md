# Install the launcher with Developer Mode

This puts the launcher on the TV as a normal app, with no root. It does not take over the Home button; for that you open the launcher yourself (see "Open it quickly" below).

Tested target: LG OLED65G1, webOS 6, firmware 03.53.45. Menu names may differ slightly on other firmware.

## 1. Get the .ipk

Either:

- Download it from GitHub: Actions → "Build launcher" → the latest run → artifact `launcher-ipk` (a zip holding `works.partridge.webos-launcher_1.0.2_all.ipk`).
- Or build it yourself with Node 22:

  ```sh
  cd launcher
  npm ci --ignore-scripts
  npm run build
  npm run package      # writes build/works.partridge.webos-launcher_1.0.2_all.ipk
  ```

## 2. Turn on Developer Mode on the TV

1. Create a free LG developer account at <https://webostv.developer.lge.com>.
2. On the TV, install the **Developer Mode** app from the LG Content Store and open it.
3. Sign in with the developer account and switch **Dev Mode Status** on. The TV restarts.
4. Open Developer Mode again and switch **Key Server** on. Note the TV's IP address and the passphrase it shows.

Keep the PC and the TV on the same network.

## 3. Install the app

**Easiest: webOS Dev Manager** (desktop app, <https://github.com/webosbrew/dev-manager-desktop>).

1. Add a device: pick the TV, enter its IP and the passphrase from step 2.
2. Go to Apps → Install, and choose the `.ipk`.
3. "Launcher" now shows up on the TV's Home row.

**Or the LG command line** (installed in `launcher/node_modules` by `npm ci`):

```sh
cd launcher
npx ares-setup-device            # add a device named "tv": the TV's IP, port 9922, user prisoner
npx ares-novacom --device tv --getkey   # enter the passphrase shown on the TV
npx ares-install --device tv build/works.partridge.webos-launcher_1.0.2_all.ipk
npx ares-launch  --device tv works.partridge.webos-launcher
```

## 4. Keep the Developer Mode session alive

Developer Mode runs on a timer. The Developer Mode app shows the time left; press **Extend** there before it runs out. Dev Manager can also renew the session from the PC. If the timer runs out, Developer Mode switches off and sideloaded apps, including the launcher, are removed; turn it on again and reinstall.

## 5. Open it quickly

- On Home, choose Edit App List and move **Launcher** to the first spot.
- Assign it to a number key: hold a number button on the remote and pick Launcher, so a long press opens it.

## Add your own apps

The launcher only shows apps it has in its catalogue (`launcher/src/config/catalog.ts`), filtered to what is installed. Regional apps are missing from it. To add one:

1. Open the app on the TV, then run `npx ares-launch --device tv --running` to see its app ID.
2. Copy `launcher/src/config/catalog.local.example.ts` to `catalog.local.ts`, add the app, rebuild and reinstall. `catalog.local.ts` is git-ignored, so it stays on your machine.

## Undo

Uninstall it in Dev Manager or with `npx ares-install --device tv --remove works.partridge.webos-launcher`, then switch Dev Mode Status off in the Developer Mode app.
