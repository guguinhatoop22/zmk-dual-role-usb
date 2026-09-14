# ZMK Dual Role USB Module (`zmk-dual-role-usb`)

A standalone [ZMK](https://zmk.dev/) module enabling dynamic dual-role switching (Central / Peripheral in the same build) for split keyboard halves.

## Overview

- **Central Mode (USB plug detected)**: Left half acts as standard Central, scans for Right half, forwards keystrokes to host via USB/BLE.
- **Peripheral Mode (Battery / Dongle in range)**: Left half acts as split peripheral, connecting directly to a dedicated Dongle Central alongside the Right half.
- **Open Advertising**: Ensures smooth reconnect between phone/PC host sessions and dongle sessions without stale directed advertising locks.

## Installation

Add this module to your `config/west.yml`:

```yaml
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: guguinhatoop22
      url-base: https://github.com/guguinhatoop22
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: main
      import: app/west.yml
    - name: zmk-dual-role-usb
      remote: guguinhatoop22
      revision: main
```

Enable in your hybrid half `.conf`:

```conf
CONFIG_ZMK_DUAL_ROLE_USB=y
CONFIG_ZMK_DUAL_ROLE_PROMOTE_DELAY_MS=6000
```

Enable in your right half `.conf` (open advertising):

```conf
CONFIG_ZMK_SPLIT_PERIPHERAL_OPEN_ADV=y
```

## License

MIT © [guguinhatoop22](https://github.com/guguinhatoop22)
