# Install as app

AeroPlus Deco is a Progressive Web App (PWA) — once installed, it runs like a native app: home screen icon, full-screen view, works offline.

## Why install

- **Faster opening** — no browser address bar, fewer taps
- **Offline use** — once loaded, the app runs without internet (your saved plans stay accessible)
- **Looks like a real app** — full-screen, your icon on the home screen
- **Separate from browsing data** — clearing your browser cookies doesn't wipe the app

## iOS (iPhone / iPad)

1. Open **sjjan.github.io/aeroplus-deco** in **Safari** (Chrome on iOS doesn't support PWA install)
2. Tap the **Share** button (square with up arrow) in the toolbar
3. Scroll down and tap **Add to Home Screen**
4. Edit the name if you want, then **Add**

The AeroPlus Deco icon now appears on your home screen. Tapping it opens the app in its own window — no browser chrome.

## Android

1. Open **sjjan.github.io/aeroplus-deco** in **Chrome** (or another Chromium browser)
2. Tap the **⋮ menu** (top right)
3. Tap **Install app** or **Add to Home screen**
4. Confirm

Some Android browsers will auto-prompt you on first visit. If you dismissed the prompt, the menu option is still there.

## Desktop (macOS, Windows, Linux)

In **Chrome / Edge / Brave**:

1. Open **sjjan.github.io/aeroplus-deco**
2. Look for the **install icon** in the address bar (a small computer or download icon, varies by browser)
3. Click it, then confirm

The app gets a dedicated launcher in your Applications/Programs list and runs in its own window.

**Safari (macOS)** does not currently support PWA install on desktop. You can still bookmark the page for quick access.

**Firefox** does not currently support PWA install. Use Chrome/Edge/Brave on Firefox-only machines.

## Verifying offline mode

After installing:

1. Open the app once (it caches itself)
2. Turn off your device's network
3. Open the app again — it should load normally

If it doesn't, the cache may not have populated yet. Open the app once with network connected, navigate around (open a few menus, calculate a plan), then try offline again.

## Updating

PWAs update automatically when you re-open the app with network connected. The app checks for a new version in the background and applies it on the next launch.

If you suspect you're stuck on an old version:

- **iOS Safari**: Delete the home-screen icon and re-add (forces a fresh install)
- **Android Chrome**: ⋮ → Settings → Site Settings → All sites → sjjan.github.io → Clear data, then re-install
- **Desktop**: Browser → Settings → Site Settings → sjjan.github.io → Clear data, then re-install

The app's version is shown in the header (small text below "AeroPlus Deco").

## What works offline

Once installed:

- ✅ Calculate dive plans
- ✅ Save and load plans (in localStorage)
- ✅ All calculators (Best mix, MOD/END, gas blending)
- ✅ Share links (they're just text — generation works offline)
- ✅ Print / Save as PDF
- ✅ Import from JSON or pasted link

What requires network:

- ❌ License activation/deactivation (Polar API)
- ❌ Opening external references (e.g. the Andy Davis article link)
- ❌ Updating the app to a new version

## Removing the installed app

- **iOS**: Long-press the home-screen icon → Remove App
- **Android**: Long-press the icon → Uninstall (or App info → Uninstall)
- **Desktop**: Browser → Settings → Site Settings → sjjan.github.io → Uninstall, or right-click the launcher

Your saved plans live in browser storage — if you uninstall and reinstall, they may persist or not depending on whether browser data is also cleared. **Back up your plans to JSON before uninstalling** if they matter to you.
