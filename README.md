# Omni Pad

Omni Pad is a compact 3×4 macropad PCB with 12 MX-compatible keys, two push-capable rotary encoders, and addressable RGB underglow. It is built around an RP2040 Zero and is intended for custom shortcuts, media controls, editing workflows, and other keyboard automation.

> **Hardware revision:** The KiCad design and manufacturing outputs are named `macropad_v3`, while this repository is the `omnipad_v4` project.

## Features

- 12 MX-compatible soldered keys arranged in a 3×4 matrix
- 2 × Bourns PEC11R-4215F-S0024 rotary encoders with push switches
- RP2040 Zero controller
- 4 × WS2812B addressable RGB LEDs for underglow
- Through-hole key switches and encoders
- Hand-solder-friendly 0805 capacitors
- KiCad schematic and PCB layout
- Gerber and drill files ready for PCB manufacturing
- 3D-printable upper and lower case models

## Repository layout

```text
.
├── BOM.csv                  Component list and sourcing metadata
├── models/
│   ├── Upper Case.stl       3D-printable top case
│   └── Bottom Case.stl      3D-printable bottom case
└── pcb/
    ├── kicad/
    │   ├── macropad_v3.kicad_pro   KiCad project
    │   ├── macropad_v3.kicad_sch   Schematic
    │   └── macropad_v3.kicad_pcb   PCB layout
    └── manufacture/          Gerbers and drill files
```

## Bill of materials

The complete component list is available in [`BOM.csv`](BOM.csv). The main electrical components are:

| Part | Quantity | Notes |
| --- | ---: | --- |
| MX-compatible switches | 12 | `MX_Solder_1.00u` footprint |
| Switch diodes | 12 | SOD-123 footprint |
| PEC11R-4215F-S0024 encoders | 2 | Rotary encoder with integrated push switch |
| WS2812B LEDs | 4 | Addressable RGB underglow |
| RP2040 Zero | 1 | Main controller |
| Capacitors | 4 | 0805 hand-solder footprint |

Check the schematic, footprint assignments, and manufacturer datasheets before ordering parts. The BOM is the source of truth for the current design revision.

## Building the hardware

### 1. Review the design

Open `pcb/kicad/macropad_v3.kicad_pro` with KiCad. Use the schematic to review the switch matrix, encoder connections, RP2040 Zero pin assignments, power, and WS2812B LED chain before fabrication.

### 2. Order the PCB

Upload the files in [`pcb/manufacture/`](pcb/manufacture/) to your PCB manufacturer. The directory includes:

- Copper, solder-mask, paste, and silkscreen Gerbers
- Board outline (`macropad_v3-Edge_Cuts.gbr`)
- PTH and NPTH drill files
- The Gerber job file

If your manufacturer supports it, upload the complete manufacturing directory as a ZIP so the layer and drill files stay together.

### 3. Assemble the board

A typical assembly order is:

1. Solder the RP2040 Zero and other small SMD components.
2. Solder the WS2812B underglow LEDs, observing their data direction and polarity.
3. Solder the 12 switch diodes.
4. Solder the two rotary encoders.
5. Solder the 12 MX-compatible switches.
6. Inspect for shorts and verify power and ground before connecting USB.

### 4. Print the case

The matching case parts are in [`models/`](models/). Print `Upper Case.stl` and `Bottom Case.stl`, then test-fit the PCB before final assembly. Confirm dimensions and mounting hardware against the current PCB before printing a large batch.

## Firmware

This repository currently contains the hardware design, manufacturing files, BOM, and case models. It does **not** include keyboard firmware or a keymap.

After assembly, the RP2040 Zero will need firmware configured for the 3×4 key matrix, both rotary encoders, their push switches, and the WS2812B underglow chain. A firmware project such as QMK or KMK can be used, but the GPIO assignments should be taken from `macropad_v3.kicad_sch` rather than assumed from the physical key positions.

## Design tools

- [KiCad](https://www.kicad.org/) for the schematic and PCB
- A Gerber viewer for checking manufacturing outputs
- A 3D-printing slicer for the case models

## Status

Omni Pad is a hardware design project. Review the schematic and PCB carefully, verify the BOM with your preferred suppliers, and perform an electrical inspection before powering a freshly assembled board.
