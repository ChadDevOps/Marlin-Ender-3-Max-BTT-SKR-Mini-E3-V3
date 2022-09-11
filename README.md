# Marlin-Ender-3-Max - BigTreeTech SKR Mini E3 V3.0 and TFT35 E3 V3.0.1 - w/ BL-Touch
This is based on my older "base/default" Marlin 3 configuration found at [Marlin-Ender-3-Max](https://github.com/ChadDevOps/Marlin-Ender-3-Max).

See Custom Mods section for hardware information.

Updated to Marlin bugfix-2.0.x branch [Jul 30, 2022 commit](https://github.com/MarlinFirmware/Marlin/commit/d1211b9f90ecdc7499c33969ab2a5f9e1b34893c)

## Settings

**Use at your own risk**  - Please note that this is highly customized for my current setup. See "Custom Mods" below for detals. I am constantly tweaking settings. Always check/verify this configuration will work with your hardware. Especially when changing stepper driver currents.

These settings have been modified from defaults (combo of Ender 3 Max and Ender 3 Pro settings), please search for "CHADDEVOPS" in the `/Marlin/*.h` files for chnages made. For defaults, see MarlinFirmware's [import-2.0.x configurations for Ender 3 Max](https://github.com/MarlinFirmware/Configurations/tree/import-2.0.x/config/examples/Creality/Ender-3%20Max) and for [Ender 3 Pro - BTT E3 3.0](https://github.com/MarlinFirmware/Configurations/tree/import-2.0.x/config/examples/Creality/Ender-3%20Pro).

`_Bootscreen.h` and `_Statusscreen.h` are included for the original LCD display. However, I am using the 'BTT TFT35 E3 V3.0.1' display. I have not tested with the old display. I'll commit the TFT35 configurations in this repo at a later date.

I would recommend the following as these can differ for every machine:

- Tune your PID for the hotend
- Tune your PID for the bed (optional)
- Calibrate E-Steps for your extruder (default is 93 for Ender 3 printers)
- Calibrate Probe Z-Offset
- Remove the Z-stop if your X-axis stops before the probe can reach the bed
- Check bed size on the config files. I changed the default size, including probing margins, as I added additonal bed clips. This is also modified under machine settings in cura.

## Process for building:

- Checkout [Marlin bugfix-2.0.x branch](https://github.com/MarlinFirmware/Marlin/tree/bugfix-2.0.x)
- Replace [platformio.ini](platformio.ini). The only change is `default_envs = STM32G0B1RE_btt`
- Replace/add the [*.h files](Marlin/) in the `/Marlin` directory.
- Customize settings based on your printer hardware.
- Build - see [Dr Vax on building the Marlin Firmware with VS Code](https://youtu.be/qPDBNBgdW6o?t=680)
- Copy firmware.bin to your SD card, remove firmware.cur

After applying a new firmware, it's best to run `M502` and `M500` to load and save the default settings. You can also run Initialize EEPROM from the lcd screen under config advanced settings. You will need to re-level the bed after issuing `M502`.

You can issue commands using pronterface or octoprint (if you have it installed on a raspberry pi - recommended)

```
Reset settings and save them to EEPROM

M502 ; reset
M500 ; saved
```

# Custom Mods - Updated Sep. 2022

In Use:

* [BIGTREETECH SKR Mini E3 V3.0 Control Board with TMC2209 UART Stepper Driver](https://amzn.to/3RAmHJN)
* [BIGTREETECH TFT35 E3 V3.0.1 Graphic Smart Display Controller Board for Ender 3 Compatible with SKR Mini E3 V3.0](https://amzn.to/3BazL1m)
* [Micro Swiss Direct Drive Extruder for Creality CR-10 / Ender 3 Printers × 1](https://store.micro-swiss.com/products/micro-swiss-direct-drive-extruder)
* [Petsfang for microswiss direct drive](https://www.thingiverse.com/thing:4775320/files) - Specifically `v2.Base.STK_2.23.stl` and `v2.MDDD.DUAL.DUCT.stl`
* 2x [WINSINN  50mm 5015 Blower Fan DC 24V](https://amzn.to/3L9wXGC)
* [WINSINN  40mm 4020 Fan Dual Ball Bearing 24V](https://amzn.to/3U1iJeR)
* [CR Touch Kit](https://amzn.to/3CVsCRv)
* [PTFE Teflon® Premium Bowden Tube](https://www.3dmakerengineering.com/collections/accessories/products/ptfe-teflon-premium-bowden-tube)
* Optional (typically use a standard brone nozzle) - [M2 Hardened High Speed Steel Nozzle - MK8 ](https://store.micro-swiss.com/collections/nozzles/products/micro-swiss-mk8-plated-m2-hardend-high-speed-steel-nozzle)
* [SIBOOR Ender 3 Accessories Dual Z Axis Kit](https://amzn.to/3iLilRr)
* [2-Pack CR10 Z axis T8 Anti Backlash Spring Loaded Nut ](https://amzn.to/3xoc8yU)
* 2x [ReliaBot 500mm T8 Tr8x8 Lead Screw and Brass Nut (Acme Thread, 2mm Pitch, 4 Starts, 8mm Lead)](https://amzn.to/3vqsgPb) - Note: a little long, will stick out top of printer - perhaps put some spinning Groots on top?
* [High Temperature CR-10 Plated Copper Heater Block for MK8 Extruder](https://amzn.to/3gtcM8M)
* [Copperhead™ Heat Break × 1 - Version: C-E](https://www.sliceengineering.com/collections/replacement-parts/products/copperhead%E2%84%A2-heat-break?variant=36827917713570)
* [Protronix Series 9 Extreme Performance Thermal Compound Paste](https://amzn.to/3xoYifI)
* [Gizmo Dorks PEI sheet](https://amzn.to/3mQ7442)
* [310mm x 320mm Borosilicate Glass Plate](https://amzn.to/3khk4x)
* [Extra Bed Clips Clamp Compatible with Ender 3 ](https://amzn.to/3B6gCxC)
* Aluminum foil under glass plate to fix leveling (if needed)

Not in use, but available:

* [3dmakerengineering.com Tungsten Carbide 3D Printer Nozzle](https://www.3dmakerengineering.com/collections/3d-printer-nozzles/products/tungsten-carbide-3d-printer-nozzle?variant=14784857112631)

### Printer Config - run/send in terminal

In order to use this config with the mods listed above, run the following commands (or modify as needed):

```
;M301 P62.0409 I7.6030 D126.5634 ; tung carb tip
M301 P43.4599 I4.6234 D102.1308 ; std bronze tip

M204 P500 ; set accel
M201 Z100; Set Z max accel to 300
M203 Z10; Set Z max feedrate to 300
M203 E150; Set E max feedrate
M900 K0.1 ;set linear advance pla

;M851 Z-2.74; Z probe height for tung carb tip
M851 Z-2.56; Z probe height for std bronze tips ;-2.6

; -------
; PLA - SET ESTEPS to YOUR PLA!
; -------
M92 E139.45932

M500 ;save
M501 ;load

M503 ; display crap
```

## Cura Start Code and machine settings.

### Machine Settings

- X width = 296
- Y width = 300
- Z height = 340
- x min = -65 mm
- y min = -57 mm
- x max = 41 mm
- y max = 46 mm
- gantry height = 25 mm
- Fan Speed: Set to 30% to 50% for PLA

### Cura Start Code

After leveling the bed, and saving it to EEPROM (`M500`), add the UBL section in your start code. You do not need to run a bed-level before every print. This will load the mesh if you have already leveled your bed. Also pre-heat the bed before leveling due to expansion.

```
; Ender 3 Custom Start G-code
G92 E0 ; Reset Extruder

M220 S100 ;Reset Feedrate
M221 S100 ;Reset Flowrate

M140 S{material_bed_temperature_layer_0} ;Start heating bed
M190 S{material_bed_temperature_layer_0} ;Wait for bed to reach temp before proceeding

G28 X Y Z ;Home

;M205 J0.2 ;Junction Deviation
M900 K0.11 ;set linear advance pla

M104 S{material_print_temperature_layer_0} ;Start heating extruder
M109 S{material_print_temperature_layer_0} ; Wait for Extruder temperature

;M420 S1 ; Load bed mesh - marlin (disabled as using UBL)

; UBL
G29 F 10.0 ; Set Fade Height for correction at 10.0 mm.
G29 A ; Activate the UBL System.
G29 L0 ; Load Mesh from slot 0
M420 S1 V; Turn on using bed mesh

G92 E0
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X295 Y20 Z0.3 F5000.0 ; Move to start position
G1 X295 Y295.0 Z0.3 F2000 E30 ; Draw the first line
G1 X293 Y295.0 Z0.3 F5000.0 ; Move to side a little
G1 X293 Y20 Z0.3 F2000 E50 ; Draw the second line

G92 E0 ; Reset Extruder
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X293 Y16 Z0.2 F5000.0 ; Move over to prevent blob squish
G92 E0
```

## The Printer

<img src="./Ender3-Max.jpg?raw=true" width="250">
