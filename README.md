# TOTEM ZMK Config

Personal ZMK configuration for a 38-key TOTEM split keyboard using three Seeed XIAO nRF52840 controllers:

- left half: split peripheral
- right half: split peripheral
- dongle: split central, normally connected over USB

The repository is structured as a modern unified ZMK config/module and is intended to work with the ZMK Keymap Editor.

## Layers

0. Base
1. Direct
2. Nav
3. Num
4. Sym
5. Mouse
6. Adjust

All logical modifiers use the left-side HID modifier usages consistently:

- Ctrl -> `LCTRL`
- Alt -> `LALT`
- GUI -> `LGUI`
- Shift -> `LSHIFT`

## Build

Push the repository to GitHub. The included workflow builds:

- `totem_left`
- `totem_right`
- `totem_dongle`
- `settings_reset`

The build uses the current XIAO BLE board name: `xiao_ble//zmk`.

## First dongle pairing

When changing split roles or starting from old pairings:

1. Turn all three controllers off.
2. Flash `settings_reset` to the dongle.
3. Flash `totem_dongle` to the dongle.
4. Flash `settings_reset` to the left half, then flash `totem_left`.
5. Flash `settings_reset` to the right half, then flash `totem_right`.
6. Power-cycle the parts if they do not connect immediately.

## Keymap Editor

The editable keymap is:

`config/totem.keymap`

`config/info.json` contains the TOTEM physical layout metadata used by web keymap tools.

## Notes

- `Num + Sym` activates Adjust through a conditional layer, not a raw combo.
- Base-only typing combos are `Q + W -> Esc` and `Z + X -> Caps Word`.
- Mouse Slow movement is intentionally kept as an experiment.
- Home-row-mod and thumb layer-tap timings are initial tuning values and are expected to be adjusted after real use.
- Reset behaviors are source-specific on split keyboards: the outer Adjust key affects the physical side on which it is pressed.
