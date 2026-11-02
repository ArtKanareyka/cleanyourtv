# This fork

A small fork of [Gathin23/cleanyourtv](https://github.com/Gathin23/cleanyourtv) that adds one
switch and keeps everything else identical:

- **`show_bluetooth_pill`** (config.xml or a theme's `config.json`, off by default): a Bluetooth
  pill in the top bar that opens the Bluetooth / remotes & accessories screen directly, so
  pairing headphones or a controller needs no trip through Settings. Hidden by `top_menu`,
  follows `icon_only_buttons`, wired into `pillKeys` and the advanced-effects pill list.

Where the standard `ACTION_BLUETOOTH_SETTINGS` has no answer, the pill falls back to Android TV's
own accessories pairing screen (`com.google.android.intent.action.CONNECT_INPUT` →
AddAccessoryActivity), then to the generic settings chain. Found on an Android 8 Philips
(TPM171E) where nothing answers the settings action and `MainSettings` is not exported — thanks
[@priku](https://github.com/Gathin23/cleanyourtv/pull/2977).

Upstream kept the launcher at a hard size budget and declined the switch for core
([#2977](https://github.com/Gathin23/cleanyourtv/pull/2977)); it lives here instead.

## Tested on

- Xiaomi TV Box S 3rd gen (MiTV-AFMU0, twilight), Google TV 14 (SDK 34), firmware V816.0.11.0

Build and install exactly as upstream: `launcher/build-and-install.sh` with `TV_HOST=<box ip>`.
