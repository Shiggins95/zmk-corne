# Flashing Firmware

This repo builds firmware via GitHub Actions (see `.github/workflows/build.yml` and `build.yaml`), producing two files each run:

- `corne_left-nice_nano_v2-zmk.uf2`
- `corne_right-nice_nano_v2-zmk.uf2`

Both are bundled with the `nice_view` display.

## Steps

1. **Push your changes** (or open a PR) — GitHub Actions builds automatically.
2. On the GitHub repo, go to the **Actions** tab → the latest workflow run → scroll down to **Artifacts** → download the zip (usually named `firmware`). Unzip it to get the two `.uf2` files.
3. **Flash one half at a time**:
   1. Connect that half to your computer via USB-C.
   2. Put it into bootloader mode by double-tapping the reset button on the nice_nano (a small side button, or a pogo-pin/pad depending on board revision). It should then show up on your computer as a USB mass-storage drive, usually named `NICENANO`.
   3. **Drag and drop** the matching `.uf2` file onto that drive:
      - `corne_left-nice_nano_v2-zmk.uf2` → left half
      - `corne_right-nice_nano_v2-zmk.uf2` → right half

      The board will auto-reboot into the new firmware once the copy finishes (drive disappears).
   4. Disconnect and repeat the above for the other half.

## Notes

- Flashing firmware does **not** wipe Bluetooth pairings. Bond data lives in a separate flash "settings" partition that a normal `.uf2` flash doesn't touch — only the application code is replaced. Bonds are only cleared by an explicit action (`BT_CLR` key) or flashing a dedicated `settings_reset.uf2`.
- Only firmware changes (keymap/config) require reflashing — you don't need to touch `west.yml` or `build.yaml` unless the board/shield/manifest itself changes.
