# GKTools MI v4.0 Plotter firmware

An Arduino Nano based GRBL setup with support for servo

This version requires the `.hex` file to be directly uploaded, as the bootloader takes too much space

This was hacked together from the 0.9j version of GRBL and https://github.com/robottini/grbl-servo

## Gcode configuration

    $0=10 (step pulse, usec) (Step pulse time, microseconds)
    $1=25 (step idle delay, msec) (Step idle delay, milliseconds)
    $2=0 (step port invert mask:00000000) (Step pulse invert, mask)
    $3=0 (dir port invert mask:00000000) (Step direction invert, mask)
    $4=0 (step enable invert, bool) (Invert step enable pin, boolean)
    $5=0 (limit pins invert, bool) (Invert limit pins, boolean)
    $6=0 (probe pin invert, bool) (Invert probe pin, boolean)
    $10=3 (status report mask:00000011) (Status report options, mask)
    $11=0.010 (junction deviation, mm) (Junction deviation, millimeters)
    $12=0.002 (arc tolerance, mm) (Arc tolerance, millimeters)
    $13=0 (report inches, bool) (Report in inches, boolean)
    $20=1 (soft limits, bool) (Soft limits enable, boolean)
    $21=1 (hard limits, bool) (Hard limits enable, boolean)
    $22=1 (homing cycle, bool) (Homing cycle enable, boolean)
    $23=3 (homing dir invert mask:00000011) (Homing direction invert, mask)
    $24=1000.000 (homing feed, mm/min) (Homing locate feed rate, mm/min)
    $25=5000.000 (homing seek, mm/min) (Homing search seek rate, mm/min)
    $26=250 (homing debounce, msec) (Homing switch debounce delay, milliseconds)
    $27=2.000 (homing pull-off, mm) (Homing switch pull-off distance, millimeters)
    $100=100.000 (x, step/mm) (X-axis steps per millimeter)
    $101=100.000 (y, step/mm) (Y-axis steps per millimeter)
    $102=100.000 (z, step/mm) (Z-axis steps per millimeter)
    $110=15000.000 (x max rate, mm/min) (X-axis maximum rate, mm/min)
    $111=15000.000 (y max rate, mm/min) (Y-axis maximum rate, mm/min)
    $112=15000.000 (z max rate, mm/min) (Z-axis maximum rate, mm/min)
    $120=1000.000 (x accel, mm/sec^2) (X-axis acceleration, mm/sec^2)
    $121=1000.000 (y accel, mm/sec^2) (Y-axis acceleration, mm/sec^2)
    $122=1000.000 (z accel, mm/sec^2) (Z-axis acceleration, mm/sec^2)
    $130=230.000 (x max travel, mm) (X-axis maximum travel, millimeters)
    $131=335.000 (y max travel, mm) (Y-axis maximum travel, millimeters)
    $132=1.000 (z max travel, mm) (Z-axis maximum travel, millimeters)

***

![GitHub Logo](https://github.com/gnea/gnea-Media/blob/master/Grbl%20Logo/Grbl%20Logo%20250px.png?raw=true)
***

### Grbl v1.1 has been released [here](https://github.com/gnea/grbl/releases)!
### Notice: This site will be phased out and moved to the new one!

***

Grbl is a no-compromise, high performance, low cost alternative to parallel-port-based motion control for CNC milling. It will run on a vanilla Arduino (Duemillanove/Uno) as long as it sports an Atmega 328. 

The controller is written in highly optimized C utilizing every clever feature of the AVR-chips to achieve precise timing and asynchronous operation. It is able to maintain up to 30kHz of stable, jitter free control pulses.

It accepts standards-compliant g-code and has been tested with the output of several CAM tools with no problems. Arcs, circles and helical motion are fully supported, as well as, all other primary g-code commands. Macro functions, variables, and most canned cycles are not supported, but we think GUIs can do a much better job at translating them into straight g-code anyhow.

Grbl includes full acceleration management with look ahead. That means the controller will look up to 18 motions into the future and plan its velocities ahead to deliver smooth acceleration and jerk-free cornering.

* [Licensing](https://github.com/grbl/grbl/wiki/Licensing): Grbl is free software, released under the GPLv3 license.

* For more information and help, check out our **[Wiki pages!](https://github.com/grbl/grbl/wiki)** If you find that the information is out-dated, please to help us keep it updated by editing it or notifying our community! Thanks!

* Lead Developer [_2011 - Current_]: Sungeun(Sonny) K. Jeon, Ph.D. (USA) aka @chamnit

* Lead Developer [_2009 - 2011_]: Simen Svale Skogsrud (Norway). aka The Originator/Creator/Pioneer/Father of Grbl.

***

### Official Supporters of the Grbl CNC Project
![Official Supporters](https://github.com/gnea/gnea-Media/blob/master/Contributors.png?raw=true)

***

_**Master Branch:**_
* [Grbl v0.9j Atmega328p 16mhz 115200baud with generic defaults](http://bit.ly/1I8Ey4S) _(2016-03-17)_
  - **IMPORTANT INFO WHEN UPGRADING TO GRBL v0.9 :** 
  - Baudrate is now **115200** (Up from 9600). 
  - Homing cycle updated. Located based on switch trigger, rather than release point.
  - Variable spindle is now enabled by default. Z-limit(D12) and spindle enable(D11) have switched to access the hardware PWM on D11. Homing will not work if you do not re-wire your Z-limit switch to D12.

_**Archives:**_
* [Grbl v0.9i Atmega328p 16mhz 115200baud with generic defaults](http://bit.ly/1EiviDk) 
* [Grbl v0.9g Atmega328p 16mhz 115200baud with generic defaults](http://bit.ly/1m8E1Qa) 
* [Grbl v0.8c Atmega328p 16mhz 9600baud](http://bit.ly/SSdCJE)
* [Grbl v0.7d Atmega328p 16mhz 9600baud](http://bit.ly/ZhL15G)
* [Grbl v0.6b Atmega328p 16mhz 9600baud](http://bit.ly/VD04A5)
* [Grbl v0.51 Atmega328p 16mhz 9600baud](http://bit.ly/W75BS1)
* [Grbl v0.6b Atmega168 16mhz 9600baud](http://bit.ly/SScWnE)
* [Grbl v0.51 Atmega168 16mhz 9600baud](http://bit.ly/VXyrYu)


***

## Update Summary for v0.9j
  - **Restore EEPROM feature:** A new set of restore EEPROM features to help OEMs and users reset their Grbl installation to the build defaults. See Configuring Grbl Wiki for details.
  - **More configuration options for input pins**
  - **Bug fixes including:** Soft limit error handling, disable spindle when S0, g-code reporting of G38.x.
  
## Update Summary for v0.9i
  - **IMPORTANT:**
    - **Homing cycle updated. Locates based on trigger point, rather than release point.**
    - **System tweaks: $14 cycle auto-start has been removed. No more QUEUE state.**
  - **New G-Codes** 
  - **CoreXY Support**
  - **Safety Door Support**
  - **Full Limit and Control Pin Configurability**
  - **Additional Compile-Time Feature Options**

## Update Summary for v0.9h from v0.8
  - **IMPORTANT:**
    - **Default serial baudrate is now 115200! (Up from 9600)**
    - **Z-limit(D12) and spindle enable(D11) pins have switched to support variable spindle!**
  - **Super Smooth Stepper Algorithm**
  - **Stability and Robustness Updates**
  - **(x4)+ Faster Planner**
  - **Compile-able via Arduino IDE!**
  - **G-Code Parser Overhaul**
  - **Independent Acceleration and Velocity Settings**
  - **Soft Limits**
  - **Probing**
  - **Dynamic Tool Length Offsets**
  - **Improved Arc Performance**
  - **CPU Pin Mapping**
  - **New Grbl SIMULATOR! (by @jgeisler and @ashelly)**
  - **Configurable Real-time Status Reporting**
  - **Updated Homing Routine**
  - **Optional Limit Pin Sharing**
  - **Optional Variable Spindle Speed Output**
  - **Additional Compile-Time Feature Options**

-
``` 
List of Supported G-Codes in Grbl v0.9 Master:
  - Non-Modal Commands: G4, G10L2, G10L20, G28, G30, G28.1, G30.1, G53, G92, G92.1
  - Motion Modes: G0, G1, G2, G3, G38.2, G38.3, G38.4, G38.5, G80
  - Feed Rate Modes: G93, G94
  - Unit Modes: G20, G21
  - Distance Modes: G90, G91
  - Arc IJK Distance Modes: G91.1
  - Plane Select Modes: G17, G18, G19
  - Tool Length Offset Modes: G43.1, G49
  - Cutter Compensation Modes: G40
  - Coordinate System Modes: G54, G55, G56, G57, G58, G59
  - Control Modes: G61
  - Program Flow: M0, M1, M2, M30*
  - Coolant Control: M7*, M8, M9
  - Spindle Control: M3, M4, M5
  - Valid Non-Command Words: F, I, J, K, L, N, P, R, S, T, X, Y, Z
```
