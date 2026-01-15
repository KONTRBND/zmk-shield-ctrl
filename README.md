# CTRL 3x4 - ZMK Shield

> [!WARNING]
> This is a **prototype shield** built for a very specific hardware setup.

The **CTRL 3x4** is a custom ZMK shield designed for a small MacroPad with a 3x4 key matrix and an LED display.  
It was developed under tight pin constraints, which led to several intentional design decisions that limit portability.

## Supported Hardware

> [!IMPORTANT]
> This shield is only supported on the *Seeed Studio XIAO nRF52840*.

Other boards, including other XIAO variants, are not unsupported.

Pin assignments, SPI usage, and GPIO access are tightly coupled to the XIAO nRF52840.  
Using this shield on a different board will require modifications and is not expected to work out of the box.

## Integration with a ZMK Config

To use this shield in a `zmk-config` repository, it must be added as an external module and referenced during the build.

### 1. Add the shield as a West dependency

Add this repository to the `west.yml` file of your `zmk-config`:

```yaml
manifest:
  remotes:
    - name: kontrbnd
      url-base: https://github.com/KONTRBND
  projects:
    - name: zmk-shield-ctrl
      remote: kontrbnd
      revision: main
```

If your config already uses other external modules, merge this entry into the existing manifest.

### 2. Enable the shield in your build

When building ZMK, specify the shield explicitly:

```sh
west build -b seeed_xiao_nrf52840 -- -DSHIELD=ctrl
```

If you are using a GitHub-Actions-based build, add `ctrl` to the `shield` field of the corresponding job.

## Features

- 3x4 key matrix (12 keys)
- LED display
- ZMK-compatible shield module

## Design Decisions and Limitations

### NFC Pin Repurposing

Due to limited available GPIOs on the XIAO nRF52840:

- The NFC pins are repurposed as regular GPIOs
- NFC functionality is permanently disabled

This trade-off was necessary to gain additional usable IO.

### Custom SPI Instance

An SPI instance (`spi2`) is redefined for the display.

This was done to:
- Free pins used by the default SPI instances
- Reclaim `SPIM_SIMO` for general-purpose GPIO use

As a result, the SPI configuration is intentionally non-standard and board-specific.

## Project Status

> [!CAUTION]
> This project is a **prototype**.
>
> - APIs and configuration may change
> - Hardware assumptions are baked in
> - No compatibility guarantees are made

If you plan to reuse parts of this shield, treat it as a reference or starting point, not a drop-in solution.
