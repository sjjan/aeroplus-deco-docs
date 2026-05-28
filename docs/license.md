# License & trial

AeroPlus Deco is paid software with a free trial. This page explains how the trial and licensing work.

## Free trial

When you first open the app, you get **14 days of free use** — full functionality, no limits. The trial counter shows in the header.

- The trial clock starts from your first visit, **per device** (it's stored in your browser's localStorage)
- Re-installing the app or clearing browser data may or may not reset the clock, depending on browser specifics — but it's not the intended path
- No personal data is collected for the trial

After the trial expires, the app prompts for a license key. Existing plans remain visible but the calculator is locked until activation.

## Purchasing

Tap **App menu → License → Purchase**. This opens the **Polar** checkout in a new tab.

Polar handles payment, EU VAT, and license key delivery. After purchase:

1. You receive an **email from Polar** with subject "Your AeroPlus Deco license"
2. The email contains your license key (looks like `XXXX-XXXX-XXXX-XXXX`)
3. Open the License page in the app and tap **Activate**
4. Paste your key, tap **Activate**

If activation succeeds, the app shows:

> ✓ License active
> Thank you for supporting AeroPlus Deco.

## Activation details

| Aspect | Detail |
|---|---|
| Devices per license | **3 maximum** |
| Trial reset | None — activate to continue after 14 days |
| Validation | Online check against Polar's API on activation |
| Offline use | Yes, indefinitely once activated |
| Re-activation cost | None — same license key, same Polar account |

## Switching devices

If you want to use your license on a different device than one of your activated three:

1. On the device you want to **remove**: **App menu → License → Remove this device from license**
2. On the new device: **App menu → License → Activate**, enter the same key

The deactivation talks to the Polar API to free up the slot, then you can activate the new device.

If you can't access the old device (lost, sold, broken), contact support — Polar can free up a slot manually:

- Email **support@aeroplus-deco.com** with your license key
- Include the rough activation date or proof of purchase

## What you're paying for

- **Lifetime access** to AeroPlus Deco — no monthly subscription
- **Free updates** for the same major version (and a generous grace period for major upgrades)
- **No ads, no tracking, no telemetry** — the app stays clean
- **Email support** at support@aeroplus-deco.com

You're explicitly not paying for: data hosting (the app stores nothing on a server), analytics, or any premium tier — there's only one tier.

## Refunds

Polar handles refund requests within 14 days of purchase. Email **support@aeroplus-deco.com** if you want to request one.

## Privacy of activation

When you activate or deactivate a license, the only network traffic is to the Polar API (api.polar.sh). The app sends:

- Your license key
- A device label (browser-derived; can be customized)
- The action (activate / deactivate)

Polar's privacy policy applies to your payment and account data; AeroPlus Deco itself doesn't add or store anything.

## License key issues

### "License key not found"

- Double-check the key matches the email exactly (no leading/trailing spaces)
- Confirm you're on the right account if multiple Polar customers

### "All devices used"

- Remove a device from the License page on another already-activated device
- Or email support for a manual reset

### "Network error during activation"

- Confirm you have internet access
- The activation requires reaching api.polar.sh; corporate firewalls may block it
- Try from a different network if necessary

### "License expired"

- Email support — the license should be lifetime; an expired status is a system issue
