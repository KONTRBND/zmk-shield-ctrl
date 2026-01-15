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
