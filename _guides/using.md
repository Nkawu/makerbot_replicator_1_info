---
layout: page
title: Using
description: Using the Makerbot Replicator 1
order: 2
---

# {{ page.title }}

- TOC
{::options toc_levels="2,3" /}
{:toc}

Regarding dual extrusion, i.e. printing in 2 colors - just don't! The dual extruders are convenient to keep 2 different filaments loaded, but use only one at a time. Ideally you want to remove the nozzle not in use to avoid knocking print jobs of the bed.
{:.ui.tiny.message}

### General Overview

There are 4 different pieces of software involved in the process to produce a 3D printed object:

1. **CAD (Computer-Aided Design) Software** This is software run on your desktop computer to create a 3-dimensional design of the object you are trying to print. Examples are Fusion 360, TinkerCAD, SketchUp, FreeCAD and many more. Most have a steep learning curve, but time well spent to master the software of your choice. This step is not required as "ready to print" designs can be downloaded from Thingiverse, Thangs, etc.
1. **Slicer Software** This software also runs on your desktop computer. The software converts a geometric model produced by CAD (usually `STL`) into 3D printer instructiones (`G-CODE`). It literally slices the design into thin layers and produces printer instructions to print each layer. Examples are SuperSlicer (or PrusaSlicer / Slic3r), Cura, etc. This can also be a tricky step to master as you need to expirement with settings if, for example your print doesn't stick to the base plate, warps, etc.
1. **Web Interface** Not all printers will have this, but it enables you to control and monitor all aspects of your printer and print jobs, remotely via your desktop computer or phone even. Most popular in this category is [**OctoPrint**](https://docs.octoprint.org/en/master/). This is usually installed on a Raspberry Pi and connected via USB directly to your printer.
1. **Printer Firmware** This is the (usually manufacturer supplied) software that is installed on the printer itself. This software interprets the instructions (`G-CODE`) and instructs the printer where to move to and extrude filament. Usually controlled via an interface and display on the printer. The Makerbot Replicator works best with **Sailfish** firmware.

### Review the Sailfish firmware documentation

* [Front Panel Operation](http://www.sailfishfirmware.com/doc/ui.html#x11-100003)
* [Leveling the Build Plate](http://www.sailfishfirmware.com/doc/basic-usage-leveling.html#x6-50002.1)

### Menu Navigation

Most menu options don't need to be touched, refer to [Front Panel Operation](http://www.sailfishfirmware.com/doc/ui.html#x11-100003) for more info. When you see this :warning: an option can render the printer inoperable!
{:.ui.tiny.warning.message}

Here are some of the commonly used menu options:

* Print from SD - Browse and select files to print from the SD card
* Preheat
    * Start Preheating - heat your printer based on the selections below without starting to print
    * Right Extruder [ON/OFF]
    * Left Extruder [ON/OFF]
    * Platform [ON/OFF]
* Utilities
    * Monitor Mode - current temperatures of heating elements, if enabled also target temperatures
    * Filament Loading - load, unload and change filament in any extruder
        * Unload right
        * Load right
        * Unload left
        * Load left
    * Preheat Settings - set the preheat temperatures for each of the heating elements
        * Right Extruder [220]
        * Left Extruder [220]
        * Platform [50]
    * General Settings - :warning:
    * Level Build Plate - set up printer to level build plate
    * Home Axes - utility to home the axes, first X and Y, and then Z
    * Bot Statistics - displays usage information printer
    * Filamanent Odometer - display lifetime filament usage in meters
    * Profiles - save up to four preheat and home offsets settings, and quickly recall them
        * ABS
        * PLA
        * Profile3
        * Profile4
    * Home Offsets - :warning: change the home offsets, which define the center of the build plate (0,0,0) relative to the endstops
    * Toolhead Offsets - :warning: change the X and Y toolhead offsets which describe the spacing between the two extruder nozzles
    * Jog Mode - move the extruder and build plate
    * En/Disable Steppers - change the status of all stepper motors
    * Calibrate Nozzles - :warning: enter nozzle calibration indices after calibration print
    * Restore Settings - :warning: restore all factory settings save for the home offsets and toolhead offsets
    * Eeprom - :warning: EEPROM utilities
    * Version Information - printer version information

### Bed Levelling

* Before starting, it's a good idea to lower the build plate by turning in (clockwise) all 4 bed asjustment screws underneath the build plate a few turns. This ensures the extruder nozzle will clear the build plate.
* Pre-heat the build plate by selecting **Preheat**. Only the **Platform** needs to be set to [ON]
* Allow the build plate 10+ minutes to heat soak
* Select **Utilities** -> **Level Build Plate**
* Printer will home the axes, first X and Y, and then Z
* Once homed, the extruder will be moved to the center of the build plate
* Move the extruder nozzle roughly over the right-rear adjustment screw
* Use a sheet of printer paper (roughly 0.1mm thick) and adjust the screw until you feel *slight* resistance when sliding the paper between the nozzle and the build plate. If the plate doesn't move, give the other 3 screw 1/2 a turn out (counter-clockwise) and try again.
* Repeat this process in the rear-left, then front-left and finally front-right positions
* Repeat all 4 positions to confirm you get the same amount of drag everywhere
* Once satisfied, push the controller button a few times to end leveling mode

If your platform is too low, your prints might not stick to the surface, and if it's too high, the nozzles could damage the platform surface.
{:.ui.small.warning.message}


### Loading Filament

* Remove the filament guide tube from the top of the extruder. Make sure to hold down the gray ring that connects the tube to the Stepstruder -- just pulling on the tube won’t work.
* Make sure there is no filament in the extruder, otherwise remove it first.
* Place a roll of filament on the spool holder with the filament feeding from the bottom. Feed the filament into the guide tubes from the back until you see it come out at the front.
* Select **Utilities** -> **Filament Loading** -> **Load Left/Right**
* The extruder will heat up to the temperature set up in **Utilities** -> **Preheat Settings** -> **Left/Right Extruder**
* Once the nozzle is at temperature, the printer will beep and start feeding. Push the lever on the extruder down and insert the filament as far down as it will go. Release the lever. The filament should start feeding into the extruder. If not, push the lever and pull the filament out slightly.
* Once the filament starts being extruded through the nozzle, klet it run for 30-60 sec to purge the extruder.
* Push the center button on the controller to stop the process.

### Unloading Filament

* Remove the filament guide tube from the top of the extruder. Make sure to hold down the gray ring that connects the tube to the Stepstruder -- just pulling on the tube won’t work.
* Select **Utilities** -> **Filament Loading** -> **Unload Left/Right**
* The extruder will heat up to the temperature set up in **Utilities** -> **Preheat Settings** -> **Left/Right Extruder**
* Once the nozzle is at temperature, the printer will beep and start running. Push the lever on the extruder down and pull the filament out of the extruder.
* Push the center button on the controller to stop the process.

### Setting up your Slicer

An example configuration is provided only for [SuperSlicer](https://github.com/supermerill/SuperSlicer)
{:.ui.small.info.message}

* An initial configuration bundle can be downloaded [SuperSlicer_config_bundle.ini]({{ site.url }}{{ site.baseurl }}/download/SuperSlicer_config_bundle.ini)
* In SuperSlicer go to **File** -> **Import** -> **Import Config Bundle...** to import the bundle
* You may need to adjust filament extrusion temperatures based on your filament
* Adjust print settings like infill etc and slice!
* Click the **Slice Now** button to slice the model according to your settings
* Click the **Export G-code** button to save a g-code file, or click the **G** button right next to it to send the g-code file directly to Octoprint as defined in the **Physical Printer** settings in SuperSlicer. 

### Preparation
1. Power on Replicator
1. Level bed (if it hasn't been done recently)
1. Load filament
1. Prime filament

### Steps
1. Design/Download STL file
1. Slice STL file into G-CODE file with the slicer

#### Using SD card
1. Convert G-CODE file to X3G file using GPX
1. Save X3G file onto SD card and insert into Replicator
1. Select file using the control pad and LCD display
1. Print!

### OR

#### Using OctoPrint
1. Power on the Raspberry Pi
1. Access the OctoPrint UI on a web browser
1. Connect OctoPrint to the Replicator
1. Upload G-CODE file from Octoprint or send it directly to OctoPrint from your slicer
1. GPX plugin in Octoprint will automatically convert G-CODE to X3G
1. Select file on the Octoprint UI in a web browser
1. Print while watching progress remotely with the webcam!

It is recommended that the extruder warm up at printing temperature for a good 5-10 minutes before attempting a first noodle when starting from cold. After it's warmed up, some prefer to "idle" at about 160C between builds. It's cold enough that the nozzle doesn't ooze and you're less likely to get a rising pool of molten ABS in the barrel.
{:.ui.small.info.message}
