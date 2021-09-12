---
layout: page
title: Configuration
description: Makerbot Replicator 1 Configuration
order: 4
---
# {{ page.title }}

- TOC
{::options toc_levels="2,3" /}
{:toc}

## Slicer

### Approach

Typically three versions of the Makerbot Replicator are created in the slicer:

* Right Extruder
* Left Extruder
* Dual Extrusion

Each printer configuration will be identical, **EXCEPT** for different start G-CODE option for the printer.

### Typical Slicer Settings

Setting | Value
------- | -----
Bed Shape | Rectangular
Width/X | 225 mm
Depth / Y | 145 mm
Height / Z | 150 mm
Origin | Center of bed
Origin X | 112.5 mm
Origin Y | 72.5 mm
Extruders | 1 or 2
G-CODE Flavor | RepRap
Start G-CODE | As shown below
End G-CODE | As shown below
Nozzle diameter | 0.4mm
Filament | 1.75mm
Max print speed | 100 mm/s

The Makerbot Replicator's firmware will handle moost of the advanced settings like acceleration, print head spacing, etc automatically, these do not have to be set.
{:.ui.small.info.message}

### Slicer Configuration

The Makerbot Replicator will need **start** and **end** G-CODE sections added to your slicer software. This will ensure your prints work as expected. The following G-CODE examples include substitution variables for **SuperSlicer**, other slicers like **Ultimaker Cura** may use different variables

#### Start G-CODE Right Extruder Only

```gcode
; **** begin start.gcode Replicator 1 Dual Right Extruder****
M73 P0 ; enable show build progress
G90 ; set positioning to absolute
M127 ; disable fan
;
; set temps and assert Vref
M140 S[first_layer_bed_temperature] ; heat bed up to first layer temperature
M104 S[first_layer_temperature] T0 ;  set right extruder temperature to first layer temperature
M104 S0 T1 ; set left extruder to 0
G130 X118 Y118 A118 B118 ; set stepper vrefs to default
; let the Z stepper vref stay at eeprom level (probably 40)
;
; home and set coordinates
T0 ; home on the right extruder
G28 X Y Z ; home XYZ at default home feedrates
G92 X0 Y0 Z0 A0 B0 ; define this as Z=0, the other coords are technically unnecessary but x3g requires them so gpx will make some up
G1 Z5 F500 ; move Z 5mm away so we can carefully hit the limit switch
G161 Z F100 ; home Z slowly to give more consistent first layer height
M132 X Y Z A B; recall stored home offsets for XYZ axes
;
; move extruder to waiting position then wait for heatup
G1 Z30 F1100 ; move Z to waiting height
G1 X110 Y-72 F2500 ; move to waiting position
M116 ; wait for everything to reach target temperature
;
; wipe and prime extruder
G1 Y-75 F2500 ; move off the bed
G1 Z0 F1100 ; move nozzle to level with bed
G1 Y-71 F4000 ; chop off any ooze on the front of the bed
G1 Z[first_layer_height] F1100 ; move to first layer height
G1 X66 F2500 ; move to prime start position
G1 X-117 E24 F2000 ; extrude a line of filament across the front edge of the bed (3mm from the front edge)
G1 Y-68 F2000
G1 X-104 Y-71 F4000 ; cross the extruded line to close the loop
G1 X-96 F4000 ; wipe across the line (X direction)
G1 X-86 Y-76 F6000 ; Move back for an additional wipe (Y direction)
G92 E0 ; set E to 0 again because the slicer's next extrusion is relative to this 0
M73 P1 ;@body (notify GPX body has started)
; **** end start.gcode ****
```

#### Start G-CODE Left Extruder Only

```gcode
; **** begin start.gcode Replicator 1 Dual Left Extruder****
M73 P0 ; enable show build progress
G90 ; set positioning to absolute
M127 ; disable fan
;
; set temps and assert Vref
M140 S[first_layer_bed_temperature] ; heat bed up to first layer temperature
M104 S0 T0 ;  set right extruder temperature to 0
M104 S[first_layer_temperature] T1 ; set left extruder to first layer temperature
G130 X118 Y118 A118 B118 ; set stepper vrefs to default
; let the Z stepper vref stay at eeprom level (probably 40)
;
; home and set coordinates
T0 ; home on the right extruder
G28 X Y Z ; home XYZ at default home feedrates
G92 X0 Y0 Z0 A0 B0 ; define this as Z=0, the other coords are technically unnecessary but x3g requires them so gpx will make some up
G1 Z5 F500 ; move Z 5mm away so we can carefully hit the limit switch
G161 Z F100 ; home Z slowly to give more consistent first layer height
M132 X Y Z A B; recall stored home offsets for XYZ axes
;
; move extruder to waiting position then wait for heatup
G1 Z30 F1100 ; move Z to waiting height
G1 X110 Y-72 F2500 ; move to waiting position
T1 ; switch to the left extruder
M116 ; wait for everything to reach target temperature
;
; wipe and prime extruder
G1 Y-75 F2500 ; move off the bed
G1 Z0 F1100 ; move nozzle to level with bed
G1 Y-71 F4000 ; chop off any ooze on the front of the bed
G1 Z[first_layer_height] F1100 ; move to first layer height
G1 X66 F2500 ; move to prime start position
G1 X-117 E24 F2000 ; extrude a line of filament across the front edge of the bed (3mm from the front edge)
G1 Y-68 F2000
G1 X-104 Y-71 F4000 ; cross the extruded line to close the loop
G1 X-96 F4000 ; wipe across the line (X direction)
G1 X-86 Y-76 F6000 ; Move back for an additional wipe (Y direction)
G92 E0 ; set E to 0 again because the slicer's next extrusion is relative to this 0
M73 P1 ;@body (notify GPX body has started)
; **** end start.gcode ****
```

#### Start G-CODE Dual Extrusion

```gcode
; **** begin start.gcode Replicator 1 Dual Both Extruders****
M73 P0 ; enable show build progress
G90 ; set positioning to absolute
M127 ; disable fan
;
; set temps and assert Vref
M140 S[first_layer_bed_temperature] ; heat bed up to first layer temperature
M104 S[first_layer_temperature] T0 ;  set right extruder temperature to first layer temperature
M104 S[first_layer_temperature] T1 ; set left extruder to first layer temperature
G130 X118 Y118 A118 B118 ; set stepper vrefs to default
; let the Z stepper vref stay at eeprom level (probably 40)
;
; home and set coordinates
T0 ; home on the right extruder
G28 X Y Z ; home XYZ at default home feedrates
G92 X0 Y0 Z0 A0 B0 ; define this as Z=0, the other coords are technically unnecessary but x3g requires them so gpx will make some up
G1 Z5 F500 ; move Z 5mm away so we can carefully hit the limit switch
G161 Z F100 ; home Z slowly to give more consistent first layer height
M132 X Y Z A B; recall stored home offsets for XYZ axes
;
; move extruder to waiting position then wait for heatup
G1 Z30 F1100 ; move Z to waiting height
G1 X110 Y-72 F2500 ; move to waiting position
M116 ; wait for everything to reach target temperature
;
; wipe and prime left extruder
T1 ; switch to the left extruder
G1 Y-75 F2500 ; move off the bed
G1 Z0 F1100 ; move nozzle to level with bed
G1 Y-71 F4000 ; chop off any ooze on the front of the bed
G1 Z[first_layer_height] F1100 ; move to first layer height
G1 X66 F2500 ; move to prime start position
G1 X-117 E24 F2000 ; extrude a line of filament across the front edge of the bed (3mm from the front edge)
G1 Y-68 F2000
G1 X-104 Y-71 F4000 ; cross the extruded line to close the loop
G1 X-96 F4000 ; wipe across the line (X direction)
G1 X-86 Y-76 F6000 ; Move back for an additional wipe (Y direction)
G92 E0 ; set E to 0 again because the slicer's next extrusion is relative to this 0
;
; wipe and prime right extruder
T0 ; switch to the left extruder
G1 Y-75 F2500 ; move off the bed
G1 Z0 F1100 ; move nozzle to level with bed
G1 Y-69 F4000 ; chop off any ooze on the front of the bed
G1 Z[first_layer_height] F1100 ; move to first layer height
G1 X66 F2500 ; move to prime start position
G1 X-117 E24 F2000 ; extrude a line of filament across the front edge of the bed (3mm from the front edge)
G1 Y-66 F2000
G1 X-104 Y-69 F4000 ; cross the extruded line to close the loop
G1 X-96 F4000 ; wipe across the line (X direction)
G1 X-86 Y-74 F6000 ; Move back for an additional wipe (Y direction)
G92 E0 ; set E to 0 again because the slicer's next extrusion is relative to this 0
;
M73 P1 ;@body (notify GPX body has started)
; **** end start.gcode ****
```
#### End G-CODE

```gcode
; **** begin end.gcode Replicator 1 Dual ****
M73 P100; end build progress
M127; disable fan
M140 S0 T0; set bed temperature to 0
M104 S0 T0; set right extruder temperature to 0
M104 S0 T1; set left extruder temperature to 0
G1 Z150 F1100 ; send Z axis to bottom of machine
T0 ; Next job assumes T0 is the current tool
M18; disable all stepper motors
M70 P5 (PRINT COMPLETE)
M72 P1; Play Ta-Da song
; **** end end.gcode ****
```

#### Ultimaker Cura G-CODE Replacement Patterns

Substitute the following tokens in the G-CODE above for use with Ultimaker Cura:

SuperSlicer | Ultimaker Cura
----------- | --------------
\[first_layer_bed_temperature] | {material_bed_temperature_layer_0}
\[first_layer_temperature] | {material_print_temperature_layer_0}
\[first_layer_height] | {layer_height_0}

If you are using Dual Extrusion with the Ultimaker Cura, you cannot use the provided printer configuration for the Makerbot Replicator, as you will not be able to define a second extruder. The solution is to add a **Custom** printer. Most of the seetings can be copied from the Makerbot Replicator setup.
{:.ui.small.info.message}
