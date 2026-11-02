# This fork

A small fork of [Gathin23/cleanyourtv](https://github.com/Gathin23/cleanyourtv) that adds one
switch and retargets two pills, keeping everything else identical:

- **`show_bluetooth_pill`** (config.xml or a theme's `config.json`, off by default): a Bluetooth
  pill in the top bar. Hidden by `top_menu`, follows `icon_only_buttons`, wired into `pillKeys`
  and the advanced-effects pill list.
- **The pills open the target screens, not the settings menu.** On Xiaomi's Google TV 14
  (MiTV-AFMU0) both `WIFI_SETTINGS` and `BLUETOOTH_SETTINGS` answer with a MainSettings alias, so
  the stock pills only reach the generic settings menu (found on TV, 2026-11-02). Here the
  network pill opens the stock connectivity list directly, and the Bluetooth pill opens Android
  TV's own accessories pairing screen (`com.google.android.intent.action.CONNECT_INPUT` →
  AddAccessoryActivity) — pairing headphones or a controller in one click. Both fall back to the
  standard chain where the target screen does not exist (an Android 8 Philips,
  [@priku](https://github.com/Gathin23/cleanyourtv/pull/2977)).
- **Permission, disclosed:** opening AddAccessoryActivity needs the caller to hold
  `BLUETOOTH_CONNECT` on Android 12+. The launcher never asks at runtime — like upstream's
  ACCESS_FINE_LOCATION, `build-and-install.sh` grants it over ADB at install time. Without that
  grant the pill falls back to the Bluetooth settings chain. No Bluetooth scan, no device list,
  nothing else touches Bluetooth.

Where the standard `ACTION_BLUETOOTH_SETTINGS` has no answer at all, the pill falls back further
to the generic settings chain (the "not available" toast).

Upstream kept the launcher at a hard size budget and declined the switch for core
([#2977](https://github.com/Gathin23/cleanyourtv/pull/2977)); it lives here instead.

## Tested on

- Xiaomi TV Box S 3rd gen (MiTV-AFMU0, twilight), Google TV 14 (SDK 34), firmware V816.0.11.0

Build and install exactly as upstream: `launcher/build-and-install.sh` with `TV_HOST=<box ip>`.
