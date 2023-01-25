# Multiprotocol/MultiPAN RCP Firmware for USB Dongles ZB-GW04 based on ZYZBP008 SM-011

Firmware repository aiming to keep up with Home Assistant's [Silicon Labs
Multiprotocol Addon][silabs-multiprotocol] required firmware version.

**DISCLAIMER:** Use these firmware files at your own risk. I will upload them
after testing them myself, however, I only have one USB Dongle and cannot
guarantee they will work for all, as I am not an expert on these devices.

| Configuration                                   | Value                                                                   |
|-------------------------------------------------|-------------------------------------------------------------------------|
| Project                                         | [Multiprotocol (OpenThread+Zigbee) RCP (rcp-uart-802154)][silabs-gecko] |
| Board                                           | Custom Board                                                            |
| Target Device                                   | EFR32MG21A020F768IM32                                                   |
| RAIL Utility, PTI: Selected Module              | None                                                                    |
| CPC Secondary - UART: RX                        | PB00                                                                    |
| CPC Secondary - UART: TX                        | PB01                                                                    |
| CPC Secondary - UART: Flow Control              | None                                                                    |
| CPC Security                                    | Disabled encryption                                                     |
| High Frequency Crystal Oscillator (HFXO): CTUNE | 128                                                                     |

<!-- commander.exe gbl create rcp-uart-802154....gbl --app rcp-uart-802154....s37 -->

[silabs-multiprotocol]: https://github.com/home-assistant/addons/tree/master/silabs-multiprotocol
[silabs-gecko]: https://github.com/SiliconLabs/gecko_sdk

## Flashing instructions

Use [universal-silabs-flasher][universal-silabs-flasher] as follows:

```sh
universal-silabs-flasher \
    --device /dev/ttyUSB0 \
    --bootloader-baudrate 115200 \
    --baudrate 115200 \
    flash \
    --firmware firmware_file.gbl \
    --allow-downgrades \
    --allow-cross-flashing
```

[universal-silabs-flasher]: https://github.com/NabuCasa/universal-silabs-flasher

## Versions

The following table lists which firmware you should use based on Home
Assistant's Silicon Labs Multiprotocol Addon version.

This table only lists Addon versions which introduced a required firmware
change, this means that versions in between versions listed in the table must
use the version from the previous listed version. For example, if you are using
Addon version 0.11.4 you must use the firmware listed for the 0.11.0 version and
not the one listed for the 0.12.0.

| Silicon Labs Multiprotocol Addon Version | Gecko SDK | Firmware File                                                                      |
|------------------------------------------|-----------|------------------------------------------------------------------------------------|
| 0.12.0                                   | v4.1.4    | [`rcp-uart-802154_nsw_115200_v4.1.4.gbl`](./rcp-uart-802154_nsw_115200_v4.1.4.gbl) |
| 0.11.0                                   | v4.2.0    | [`rcp-uart-802154_nsw_115200_v4.2.0.gbl`](./rcp-uart-802154_nsw_115200_v4.2.0.gbl) |
| 0.6.1                                    | v4.1.2    | `-`                                                                                |
| 0.5.1                                    | v4.1.1    | `-`                                                                                |
| 0.5.0                                    | v4.1.0    | `-`                                                                                |
| 0.4.0                                    | v4.0.2    | `-`                                                                                |
| 0.2.0                                    | v4.0.1    | `-`                                                                                |
