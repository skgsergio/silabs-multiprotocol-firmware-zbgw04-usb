# Multiprotocol/MultiPAN RCP Firmware for USB Dongles ZB-GW04 based on ZYZBP008 SM-011

Firmware repository aiming to keep up with Home Assistant's [Silicon Labs
Multiprotocol Addon][silabs-multiprotocol] required firmware version.

Original source: [SiliconLabs Multiprotocol (OpenThread+Zigbee) RCP
(rcp-uart-802154)][silabs-gecko]

**⚠️ DISCLAIMER:** Use these firmware files at your own risk. I will upload them
after testing them myself, however, I only have one USB Dongle and cannot
guarantee they will work for all, as I am not an expert on these devices.

[silabs-multiprotocol]: https://github.com/home-assistant/addons/tree/master/silabs-multiprotocol
[silabs-gecko]: https://github.com/SiliconLabs/gecko_sdk

## Firmware configuration parameters

| ZB-GW04 revision ➡️<br />⬇️ Setting ⬇️             | v1.1<br />(Without Hardware Flow Control) | v1.2<br />(With Hardware Flow Control) |
|-------------------------------------------------|-------------------------------------------|----------------------------------------|
| Board                                           | Custom Board                              | Custom Board                           |
| Target Device                                   | EFR32MG21A020F768IM32                     | EFR32MG21A020F768IM32                  |
| RAIL Utility, PTI: Selected Module              | None                                      | None                                   |
| CPC Secondary - UART: Flow Control              | None                                      | CTS/RTS                                |
| CPC Secondary - UART: RX                        | PB00                                      | PB00                                   |
| CPC Secondary - UART: TX                        | PB01                                      | PB01                                   |
| CPC Secondary - UART: CTS                       | None                                      | PD03                                   |
| CPC Secondary - UART: RTS                       | None                                      | PD04                                   |
| CPC Security                                    | Disabled Encryption                       | Disabled Encryption                    |
| High Frequency Crystal Oscillator (HFXO): CTUNE | 128                                       | 128                                    |

<!-- commander.exe gbl create rcp-uart-802154....gbl --app rcp-uart-802154....s37 -->

## Firmware file naming schema

```
ZB-GW04_vX.Y_GeckoSDK_vX.Y.Z_rcp-uart-802154_xxxxfc_115200.gbl
`-----´ `--´ `-------------´ `-------------´ `----´ `----´
   |     |          |               |          |       |
   |     |          |               |          |       '- Baudrate
   |     |          |               |          |
   |     |          |               |          |- nohwfc = No Hardware Flow Control
   |     |          |               |          |- hwfc   = Hardware Flow Control
   |     |          |               |          '- swfc   = Software Flow Control
   |     |          |               |
   |     |          |               |- rcp-uart-802154 = Multiprotocol (OpenThread+Zigbee) RCP Firmware
   |     |          |               '- ncp-uart-hw     = Zigbee NCP Firmware
   |     |          |
   |     |          '- Gecko SDK version X.Y.Z
   |     |
   |     '- Dongle Hardware Revision
   |
   '- Dongle Hardware Name
```

**ℹ️ NOTE:** NCP firmwares in this repo are not tested in depth, I only build
them for ZigBee sniffing purposes using [`bellows dump`][bellows]. They are
built with the default firmware source parameters (configuring the CTUNE and
UART) and adding the Manufacturing Library (mfglib) for the sniffing
capability.

[bellows]: https://github.com/zigpy/bellows

## Flashing instructions

Use [universal-silabs-flasher][universal-silabs-flasher] as follows:

```sh
universal-silabs-flasher \
    --device /dev/ttyUSB0 \
    --baudrate XXXXXX \
    flash \
    --firmware FIRMWARE_FILE.gbl \
    --allow-cross-flashing
```

Set the baudrate parameter to the baudrate of the current firmware in the USB
Dongle, from factory it comes with a `115200` baudrate firmware and here I build
firmwares with `115200` or `230400`, it is specified in the firmware file
name.

If the wrong baudrate is used the flasher will fail with the message: `Error:
Failed to probe running application type`.

[universal-silabs-flasher]: https://github.com/NabuCasa/universal-silabs-flasher

## Versions

The following table lists which firmware you should use based on Home
Assistant's Silicon Labs Multiprotocol Addon version.

This table only lists Addon versions which introduced a required firmware
change, this means that versions in between versions listed in the table must
use the version from the previous listed version. For example, if you are using
Addon version 0.11.4 you must use the firmware listed for the 0.11.0 version and
not the one listed for the 0.12.0.

**⚠️ IMPORTANT:** Pick the correct firmware version for your dongle
revision. Firmware with hardware flow control WON'T work in dongles that doesn't
support it. So please check carefully which dongle revision you own.

| Silicon Labs Multiprotocol Addon Version | Gecko SDK | Firmware Files                                                                                                                                                                                                                                   |
|------------------------------------------|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0.13.0                                   | v4.2.1    | [`ZB-GW04 v1.1 (w/o hardware flow control)`](./firmware/ZB-GW04_v1.1_GeckoSDK_v4.2.1_rcp-uart-802154_nohwfc_115200.gbl)<br />[`ZB-GW04 v1.2 (w/ hardware flow control)`](./firmware/ZB-GW04_v1.2_GeckoSDK_v4.2.1_rcp-uart-802154_hwfc_230400.gbl) |
| 0.12.0                                   | v4.1.4    | [`ZB-GW04 v1.1 (w/o hardware flow control)`](./firmware/ZB-GW04_v1.1_GeckoSDK_v4.1.4_rcp-uart-802154_nohwfc_115200.gbl)<br />[`ZB-GW04 v1.2 (w/ hardware flow control)`](./firmware/ZB-GW04_v1.2_GeckoSDK_v4.1.4_rcp-uart-802154_hwfc_115200.gbl) |
| 0.11.0                                   | v4.2.0    | [`ZB-GW04 v1.1 (w/o hardware flow control)`](./firmware/ZB-GW04_v1.1_GeckoSDK_v4.2.0_rcp-uart-802154_nohwfc_115200.gbl)<br />[`ZB-GW04 v1.2 (w/ hardware flow control)`](./firmware/ZB-GW04_v1.2_GeckoSDK_v4.2.0_rcp-uart-802154_hwfc_115200.gbl)                           |
| 0.6.1                                    | v4.1.2    | `-`                                                                                                                                                                                                                                              |
| 0.5.1                                    | v4.1.1    | `-`                                                                                                                                                                                                                                              |
| 0.5.0                                    | v4.1.0    | `-`                                                                                                                                                                                                                                              |
| 0.4.0                                    | v4.0.2    | `-`                                                                                                                                                                                                                                              |
| 0.2.0                                    | v4.0.1    | `-`                                                                                                                                                                                                                                              |
