<link rel=”manifest” href=”docs/manifest.webmanifest”>

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/U6U5NPB51)  

---  

# Stock Firmware (Marlin Based) 
The official stock firmware is based on the [Marlin 2 firmware](https://marlinfw.org/) (v2.?.?).  
  

You can either  

- download the necessary `firmware.bin` file at [Anycubic's firmware & software page](https://www.anycubic.com/pages/firmware-software) (direct link to [v1.5.6.3](https://drive.google.com/file/d/10Dd68p6FUK7iA9wFi2Gw_zl9HNVkPZNn/view)) or  
- download the source code from their specific GitHub repository to compile your own:  [https://github.com/ANYCUBIC-3D/Kobra2_Neo](https://github.com/ANYCUBIC-3D/Kobra2_Neo) 
     
In case you want to build and compile your own `firmware.bin` file, you can follow the instructions of @[jojos38](https://github.com/jojos38) [Tutorial: How to build Anycubic Marlin sourcecode into a firmware.bin](https://www.reddit.com/r/anycubic/comments/y2waxu/tutorial_how_to_build_anycubic_marlin_source_code/).  
Please mind the following warning though.  

??? warning "Firmware Source Code Files Seem To Be Incomplete"   
    
    User [that-ambuj](https://github.com/that-ambuj) noticed that the file `anycubic.uvprojx` is missing (*Thanks for reaching out!*), which seems to be necessary to compile the firmware. If you have any helpful information about this or how to compile the firmware even though this file is missing, [please contribute to this GitHub discussion](https://github.com/1coderookie/Kobra2NeoInsights/discussions/5).  

---
  
## Update Procedure

To update the firmware of your printer, unzip the compressed `rar` file and copy the file `firmware.bin` onto the microSD card.  
Turn off the printer and plug the card into the cardreader which is located at the front of the frame (next to the USB connector). The card must be inserted with the contacs facing upwards.  
Then turn on your printer. You'll see a black screen with "Updating Firmware..." displayed.  
After a certain time the Anycubic logo will appear and shortly after that the regular main screen will appear.  
Shut down the printer again and take out the card (push it in a bit to unlock it and make it come out a bit, then just pull it out).  
Turn on the printer again, go to "Menu" and then "About" and check if the correct firmware version is displayed.  
If so, everything is fine. If not, check if you really copied the correct version onto the card and proceed the update again.   

---
   
## Default Settings 
In the following I'll list the (imho) most important settings from the files  

- [`../source/Marlin/Configuration.h`](https://github.com/ANYCUBIC-3D/Kobra2_Neo/blob/main/Marlin/Configuration.h) and 
- [`../source/Marlin/Configuration_adv.h`](https://github.com/ANYCUBIC-3D/Kobra2_Neo/blob/main/Marlin/Configuration_adv.h).   
   
The following represents the state of the firmware version 1.5.6.3.  
You can find the files `Configuration.h`and`Configuration_adv.h` here: [https://github.com/ANYCUBIC-3D/Kobra2_Neo/tree/master/Marlin](https://github.com/ANYCUBIC-3D/Kobra2_Neo/tree/master/Marlin)  

**Note: I'll add the content asap, until then please have a look at the files yourself.**

<!--    
#### Configuration.h      
    
``` title="(Some) Settings for Kobra 2 Neo from Configuration.h (v1.5.6.3)"
#define BAUDRATE 115200  // This setting determines the communication speed of the printer.
--
#define MOTHERBOARD BOARD_AC_TRI_F1_V1  // Choose the name from boards.h that matches your setup
--
#define DEFAULT_NOMINAL_FILAMENT_DIA 1.75 // Generally expected filament diameter (1.75, 2.85, 3.0, ...). Used for Volumetric, Filament Width Sensor, etc.
--
Sensortypes
#define TEMP_SENSOR_0 5  // HOTEND Thermistor Type: 5 : 100K thermistor - ATC Semitec 104GT-2/104NT-4-R025H42G (Used in ParCan, J-Head, and E3D) (4.7k pullup)
#define TEMP_SENSOR_BED 1 // BED Thermistor Type: 1 : 100k thermistor - best choice for EPCOS 100k (4.7k pullup)
--
// Dummy thermistor constant temperature readings, for use with 998 and 999
#define DUMMY_THERMISTOR_998_VALUE 25
#define DUMMY_THERMISTOR_999_VALUE 100
--
// Use temp sensor 1 as a redundant sensor with sensor 0. If the readings from the two sensors differ too much the print will be aborted.
//#define TEMP_SENSOR_1_AS_REDUNDANT
#define MAX_REDUNDANT_TEMP_SENSOR_DIFF 10

#define TEMP_RESIDENCY_TIME     2  // (seconds) Time to wait for hotend to "settle" in M109
#define TEMP_WINDOW              1  // (°C) Temperature proximity for the "temperature reached" timer
#define TEMP_HYSTERESIS          3  // (°C) Temperature proximity considered "close enough" to the target

#define TEMP_BED_RESIDENCY_TIME 1  // (seconds) Time to wait for bed to "settle" in M190
#define TEMP_BED_WINDOW          1  // (°C) Temperature proximity for the "temperature reached" timer
#define TEMP_BED_HYSTERESIS      3  // (°C) Temperature proximity considered "close enough" to the target

--
// Below this temperature the heater will be switched off because it probably indicates a broken thermistor wire.
#define HEATER_0_MINTEMP   5  
#define BED_MINTEMP        5  
--
// Above this temperature the heater will be switched off. This can protect components from overheating, but NOT from shorts and failures.
#define HEATER_0_MAXTEMP 275  
#define BED_MAXTEMP      120  // max target temp-10=110
--
PID
// Comment the following line to disable PID and enable bang-bang.
#define PIDTEMP
#define BANG_MAX 255     // Limits current to nozzle while in bang-bang mode; 255=full current
#define PID_MAX BANG_MAX // Limits current to nozzle while PID is active (see PID_FUNCTIONAL_RANGE below); 255=full current
#define PID_K1 0.95      // Smoothing factor within any PID loop

#define PIDTEMPBED  // If this option is enabled set PID constants below.
  #define DEFAULT_bedKp 97.1
  #define DEFAULT_bedKi 1.41
  #define DEFAULT_bedKd 1675.16
--
Extruder
#define PREVENT_COLD_EXTRUSION
#define EXTRUDE_MINTEMP 170
#define PREVENT_LENGTHY_EXTRUDE
#define EXTRUDE_MAXLENGTH 300
--
Thermal Runaway Protection
#define THERMAL_PROTECTION_HOTENDS // Enable thermal protection for all extruders
#define THERMAL_PROTECTION_BED     // Enable thermal protection for the heated bed
#define THERMAL_PROTECTION_CHAMBER // Enable thermal protection for the heated chamber
--
Enstops (note: NO max endstops!)
#define USE_XMIN_PLUG
#define USE_YMIN_PLUG
#define USE_ZMIN_PLUG
//#define USE_XMAX_PLUG
//#define USE_YMAX_PLUG
//#define USE_ZMAX_PLUG

// Mechanical endstop with COM to ground and NC to Signal uses "false" here (most common setup).
#define X_MIN_ENDSTOP_INVERTING true // Set to true to invert the logic of the endstop.
#define Y_MIN_ENDSTOP_INVERTING true // Set to true to invert the logic of the endstop.
#define Z_MIN_ENDSTOP_INVERTING false // Set to true to invert the logic of the endstop.
--
Stepper drivers
#define X_DRIVER_TYPE  TMC2208
#define Y_DRIVER_TYPE  TMC2208
#define Z_DRIVER_TYPE  TMC2208
#define E0_DRIVER_TYPE TMC2208
--
Movement settings: X, Y, Z, E0
#define DEFAULT_AXIS_STEPS_PER_UNIT   { 80, 80, 400, 103 } // Default Axis Steps Per Unit (steps/mm); Override with M92
#define DEFAULT_MAX_FEEDRATE          { 300, 300, 4, 25 }  // Default Max Feed Rate (mm/s); Override with M203   
#define DEFAULT_MAX_ACCELERATION      { 500, 500, 100, 1000 } // Default Max Acceleration (change/s) change = mm/s (Maximum start speed for accelerated moves); Override with M201
--
Default Acceleration (change/s) change = mm/s; Override with M204: M204 P = Acceleration / M204 R = Retract Acceleration / M204 T = Travel Acceleration
#define DEFAULT_ACCELERATION          500     // X, Y, Z and E acceleration for printing moves
#define DEFAULT_RETRACT_ACCELERATION  500    // E acceleration for retracts
#define DEFAULT_TRAVEL_ACCELERATION   1000    // X, Y, Z acceleration for travel (non printing) moves
--
Default Jerk limits (mm/s); Override with M205 X Y Z E ("Jerk" specifies the minimum speed change that requires acceleration. When changing speed and direction, if the difference is less than the value set here, it may happen instantaneously.)
#define CLASSIC_JERK
  #define DEFAULT_XJERK  5
  #define DEFAULT_YJERK  5
  #define DEFAULT_ZJERK  5
--
Junction Deviation Factor
#define JUNCTION_DEVIATION_MM 0.013 // (mm) Distance from real junction edge
#define JD_HANDLE_SMALL_SEGMENTS    // Use curvature estimation instead of just the junction angle for small segments (< 1mm) with large junction angles (> 135°).
--
S-Curve Acceleration (This option eliminates vibration during printing by fitting a Bézier curve to move acceleration, producing much smoother direction changes.)
#define S_CURVE_ACCELERATION
--
Probe
#define Z_MIN_PROBE_PIN AUTO_LEVEL_RX_PIN
#define FIX_MOUNTED_PROBE
#define NOZZLE_TO_PROBE_OFFSET { -20.8,0, 0 } // Probe to RIGHT of the Nozzle has a Positive X offset
// Most probes should stay away from the edges of the bed, but with NOZZLE_AS_PROBE this can be negative for a wider probing area.
#define PROBING_MARGIN_LEFT  5
#define PROBING_MARGIN_RIGHT 5
#define PROBING_MARGIN_FRONT 5
#define PROBING_MARGIN_BACK  15
#define XY_PROBE_SPEED (200*60)  // X and Y axis travel speed (mm/min) between probes
#define Z_PROBE_SPEED_FAST (4*60)  // Feedrate (mm/min) for the first approach when double-probing (MULTIPLE_PROBING == 2)
#define Z_PROBE_SPEED_SLOW (Z_PROBE_SPEED_FAST / 2)  // Feedrate (mm/min) for the "accurate" probe of each point
#define MULTIPLE_PROBING 2  //  A total of 2 does fast/slow probes with a weighted average.
// Z probes require clearance when deploying, stowing, and moving between probe points to avoid hitting the bed and other hardware. Inductive probes need space to keep from triggering early.
// Use these settings to specify the distance (mm) to raise the probe (or lower the bed). The values set here apply over and above any (negative) probe Z Offset set with NOZZLE_TO_PROBE_OFFSET, M851, or the LCD.
// Only integer values >= 1 are valid here. 
// Example: `M851 Z-5` with a CLEARANCE of 4  =>  9mm from bed to nozzle.
//     But: `M851 Z+1` with a CLEARANCE of 2  =>  2mm from bed to nozzle.
#define Z_CLEARANCE_DEPLOY_PROBE   10 // Z Clearance for Deploy/Stow
#define Z_CLEARANCE_BETWEEN_PROBES  5 // Z Clearance between probe points
#define Z_CLEARANCE_MULTI_PROBE     5 // Z Clearance between multiple probes
#define Z_PROBE_LOW_POINT          -10 // Farthest distance below the trigger-point to go before stopping
// For M851 give a range for adjusting the Z probe offset
#define Z_PROBE_OFFSET_RANGE_MIN -10
#define Z_PROBE_OFFSET_RANGE_MAX 10
// Enable the M48 repeatability test to test probe accuracy
#define Z_MIN_PROBE_REPEATABILITY_TEST
--
// @section extruder
#define DISABLE_E false             // Disable the extruder when not stepping
#define DISABLE_INACTIVE_EXTRUDER   // Keep only the active extruder enabled
--
// @section machine
// Invert the stepper direction. Change (or reverse the motor connector) if an axis goes the wrong way.
#define INVERT_X_DIR false
#define INVERT_Y_DIR false
#define INVERT_Z_DIR true
--
// @section extruder
// For direct drive extruder v9 set to true, for geared extruder set to false.
#define INVERT_E0_DIR false
--
// @section homing
#define Z_HOMING_HEIGHT  10      // (mm) Minimal Z height before homing (G28) for Z clearance above the bed, clamps, ...
// Direction of endstops when homing; 1=MAX, -1=MIN
#define X_HOME_DIR -1
#define Y_HOME_DIR -1
#define Z_HOME_DIR -1
--
// @section machine
// The size of the print bed
#define X_BED_SIZE 230
#define Y_BED_SIZE 230
// Travel limits (mm) after homing, corresponding to endstop positions.
#define X_MIN_POS -13
#define Y_MIN_POS -9
#define Z_MIN_POS -10
#define X_MAX_POS (X_BED_SIZE + 8)
#define Y_MAX_POS (Y_BED_SIZE + 8)
#define Z_MAX_POS 250
--
Filament rounout sensor
#define FILAMENT_RUNOUT_SENSOR
  #define FIL_SENSOR_OPTIONAL        true
  #define FIL_RUNOUT_ENABLED_DEFAULT true // Enable the sensor on startup. Override with M412 followed by M500.
  #define NUM_RUNOUT_SENSORS   1          // Number of sensors, up to one per extruder. Define a FIL_RUNOUT#_PIN for each.
  #define FIL_RUNOUT_STATE     LOW        // Pin state indicating that filament is NOT present.
  #define FIL_RUNOUT_PULLUP               // Use internal pullup for filament runout pins.
#define FILAMENT_RUNOUT_SCRIPT "M600" // Set one or more commands to execute on filament runout. (After 'M412 H' Marlin will ask the host to handle the process.)
--
Bed Leveling
#define AUTO_BED_LEVELING_BILINEAR  // Probe several points in a grid. You specify the rectangle and the density of sample points. The result is a mesh, best for large or uneven beds.
#define ENABLE_LEVELING_AFTER_G28  // Normally G28 leaves leveling disabled on completion. Enable one of these options to restore the prior leveling state or to always enable leveling immediately after G28.
#define PREHEAT_BEFORE_LEVELING  // Auto-leveling needs preheating
  #define LEVELING_NOZZLE_TEMP 120  // (°C) Only applies to E0 at this time; Nozzle temp 120°C
  #define LEVELING_BED_TEMP     60  // Bed temp 60°C
#define DEBUG_LEVELING_FEATURE  //  Enable detailed logging of G28, G29, M48, etc.; Turn on with the command 'M111 S32'.; NOTE: Requires a lot of PROGMEM!
#define ENABLE_LEVELING_FADE_HEIGHT  // Gradually reduce leveling correction until a set height is reached, at which point movement will be level to the machine's XY plane. The height can be set with M420 Z<height>
  #define DEFAULT_LEVELING_FADE_HEIGHT 0.0 // (mm) Default fade height.

Note: G26 Mesh Valifation Pattern tool is DEactivated! : //#define G26_MESH_VALIDATION

#define GRID_MAX_POINTS_X 5  // Set the number of grid points per dimension.
#define GRID_MAX_POINTS_Y GRID_MAX_POINTS_X
--
Homing
// Manually set the home position. Leave these undefined for automatic settings.
#define MANUAL_X_HOME_POS X_MIN_POS
#define MANUAL_Y_HOME_POS Y_MIN_POS
#define MANUAL_Z_HOME_POS 0
--
EEPROM
// Persistent storage to preserve configurable settings across reboots.
// M500 - Store settings to EEPROM.
// M501 - Read settings from EEPROM. (i.e., Throw away unsaved changes)
// M502 - Revert settings to "factory" defaults. (Follow with M500 to init the EEPROM.)
#define EEPROM_SETTINGS  // Persistent storage with M500 and M501
#define EEPROM_CHITCHAT  // Give feedback on EEPROM commands. Disable to save PROGMEM.
#define EEPROM_BOOT_SILENT  // Keep M503 quiet and only give errors during first load
#define EEPROM_AUTO_INIT  // Init EEPROM automatically on any errors.
--
Temperature - Preheat Constants
#define PREHEAT_1_LABEL       "PLA"
#define PREHEAT_1_TEMP_HOTEND 190
#define PREHEAT_1_TEMP_BED     60
#define PREHEAT_1_FAN_SPEED     0 // Value from 0 to 255

#define PREHEAT_2_LABEL       "ABS"
#define PREHEAT_2_TEMP_HOTEND 240
#define PREHEAT_2_TEMP_BED    110
#define PREHEAT_2_FAN_SPEED     0 // Value from 0 to 255
--
Nozzle Park 
// Park the nozzle at the given XYZ position on idle or G27. The "P" parameter controls the action applied to the Z axis:
// P0  (Default) If Z is below park Z raise the nozzle.
// P1  Raise the nozzle always to Z-park height.
// P2  Raise the nozzle by Z-park amount, limited to Z_MAX_POS.

#define NOZZLE_PARK_FEATURE

#if ENABLED(NOZZLE_PARK_FEATURE)
  // Specify a park position as { X, Y, Z_raise }
  #define NOZZLE_PARK_POINT { (X_MIN_POS + 10), (Y_MAX_POS - 10), 10 }
  #define NOZZLE_PARK_X_ONLY          // X move only is required to park
  //#define NOZZLE_PARK_Y_ONLY          // Y move only is required to park
  #define NOZZLE_PARK_Z_RAISE_MIN   2   // (mm) Always raise Z by at least this distance
  #define NOZZLE_PARK_XY_FEEDRATE 100   // (mm/s) X and Y axes feedrate (also used for delta Z axis)
  #define NOZZLE_PARK_Z_FEEDRATE    5   // (mm/s) Z axis feedrate (not used for delta printers)
--
/**
 * Print Job Timer
 *
 * Automatically start and stop the print job timer on M104/M109/M190.
 *
 *   M104 (hotend, no wait) - high temp = none,        low temp = stop timer
 *   M109 (hotend, wait)    - high temp = start timer, low temp = stop timer
 *   M190 (bed, wait)       - high temp = start timer, low temp = none
 *
 * The timer can also be controlled with the following commands:
 *
 *   M75 - Start the print job timer
 *   M76 - Pause the print job timer
 *   M77 - Stop the print job timer
 */
#define PRINTJOB_TIMER_AUTOSTART
--
LANGUAGE of the UI
#define LCD_LANGUAGE zh_CN  // Chinese (Simplified)
#define LCD_LANGUAGE_AUTO_SAVE 
#define LCD_LANGUAGE_2 en  // English
--
ENCODER SETTINGS
#define ENCODER_PULSES_PER_STEP 4  // This option overrides the default number of encoder pulses needed to produce one step. Should be increased for high-resolution encoders.
#define ENCODER_STEPS_PER_MENU_ITEM 1  // Use this option to override the number of step signals required to move between next/prev menu items.
--
DISPLAY
#define TFT_GENERIC  // Generic TFT with detailed options
#define TFT_DRIVER ST7796
#define TFT_INTERFACE_SPI  // Interface.
#define TFT_RES_320x240  // TFT Resolution.
#define TFT_COLOR_UI  // Marlin Default Menus, Touch Friendly, using full TFT capabilities
```
  
#### Configuration_adv.h  
  
``` title="(Some) Settings for GO from Configuration_adv.h (v1.3.4)"
Thermal Protection / Thermal Runaway -> Hotend:
#define THERMAL_PROTECTION_PERIOD 20         // Seconds
#define THERMAL_PROTECTION_HYSTERESIS 10     // Degrees Celsius
#define ADAPTIVE_FAN_SLOWING              // Slow part cooling fan if temperature drops
#define ADVANCED_PAUSE_FEATURE

Thermal Protection / Thermal Runaway -> Bed:
#define THERMAL_PROTECTION_BED_PERIOD        20 // Seconds
#define THERMAL_PROTECTION_BED_HYSTERESIS     2 // Degrees Celsius
Manual Feedrates & Smallest Z-Move using the Control Panel
#define MANUAL_FEEDRATE { 50*60, 50*60, 4*60, 2*60 } // (mm/min) Feedrates for manual moves along X, Y, Z, E from panel
#define FINE_MANUAL_MOVE 0.025 // (mm) Smallest manual Z move (< 0.1mm)

Power Loss Recovery:
#define PLR_ENABLED_DEFAULT   true // Power Loss Recovery enabled by default. (Set with 'M413 Sn' & M500)
#define POWER_LOSS_MIN_Z_CHANGE 0.05 // (mm) Minimum Z change before saving power-loss data

Babystepping (only activated for Z-Axis!):
#define BABYSTEP_INVERT_Z false           // Change if Z babysteps should go the other way
#define BABYSTEP_MILLIMETER_UNITS         // Specify BABYSTEP_MULTIPLICATOR_(XY|Z) in mm instead of micro-steps
#define BABYSTEP_MULTIPLICATOR_Z  0.02f    // (steps or mm) Steps or millimeter distance for each Z babystep
#define BABYSTEP_MULTIPLICATOR_XY 1       // (steps or mm) Steps or millimeter distance for each XY babystep

Linear Advance is NOT Activated:
//#define LIN_ADVANCE

Advanced Pause (Experimental feature for filament change support and for parking the nozzle when paused):
#define ADVANCED_PAUSE_FEATURE
  #define PAUSE_PARK_RETRACT_FEEDRATE         60  // (mm/s) Initial retract feedrate.
  #define PAUSE_PARK_RETRACT_LENGTH           20  // (mm) Initial retract.
                                                  // This short retract is done immediately, before parking the nozzle.
  #define FILAMENT_CHANGE_UNLOAD_FEEDRATE     10  // (mm/s) Unload filament feedrate. This can be pretty fast.
  #define FILAMENT_CHANGE_UNLOAD_ACCEL        25  // (mm/s^2) Lower acceleration may allow a faster feedrate.
  #define FILAMENT_CHANGE_UNLOAD_LENGTH      100  // (mm) The length of filament for a complete unload.
                                                  //   For Bowden, the full length of the tube and nozzle.
                                                  //   For direct drive, the full length of the nozzle.
                                                  //   Set to 0 for manual unloading.
  #define FILAMENT_CHANGE_SLOW_LOAD_FEEDRATE   6  // (mm/s) Slow move when starting load.
  #define FILAMENT_CHANGE_SLOW_LOAD_LENGTH     0  // (mm) Slow length, to allow time to insert material.
                                                  // 0 to disable start loading and skip to fast load only
  #define FILAMENT_CHANGE_FAST_LOAD_FEEDRATE   6  // (mm/s) Load filament feedrate. This can be pretty fast.
  #define FILAMENT_CHANGE_FAST_LOAD_ACCEL     25  // (mm/s^2) Lower acceleration may allow a faster feedrate.
  #define FILAMENT_CHANGE_FAST_LOAD_LENGTH     0  // (mm) Load length of filament, from extruder gear to nozzle.
                                                  //   For Bowden, the full length of the tube and nozzle.
                                                  //   For direct drive, the full length of the nozzle.
  //#define ADVANCED_PAUSE_CONTINUOUS_PURGE       // Purge continuously up to the purge length until interrupted.
  #define ADVANCED_PAUSE_PURGE_FEEDRATE        3  // (mm/s) Extrude feedrate (after loading). Should be slower than load feedrate.
  #define ADVANCED_PAUSE_PURGE_LENGTH         50  // (mm) Length to extrude after loading.
                                                  //   Set to 0 for manual extrusion.
                                                  //   Filament can be extruded repeatedly from the Filament Change menu
                                                  //   until extrusion is consistent, and to purge old filament.
  #define ADVANCED_PAUSE_RESUME_PRIME          0  // (mm) Extra distance to prime nozzle after returning from park.
  //#define ADVANCED_PAUSE_FANS_PAUSE             // Turn off print-cooling fans while the machine is paused.

                                                  // Filament Unload does a Retract, Delay, and Purge first:
  #define FILAMENT_UNLOAD_PURGE_RETRACT       13  // (mm) Unload initial retract length.
  #define FILAMENT_UNLOAD_PURGE_DELAY       5000  // (ms) Delay for the filament to cool after retract.
  #define FILAMENT_UNLOAD_PURGE_LENGTH         8  // (mm) An unretract is done, then this length is purged.
  #define FILAMENT_UNLOAD_PURGE_FEEDRATE      25  // (mm/s) feedrate to purge before unload

  #define PAUSE_PARK_NOZZLE_TIMEOUT           45  // (seconds) Time limit before the nozzle is turned off for safety.
  #define FILAMENT_CHANGE_ALERT_BEEPS         10  // Number of alert beeps to play when a response is needed.
  #define PAUSE_PARK_NO_STEPPER_TIMEOUT           // Enable for XYZ steppers to stay powered on during filament change.

  #define PARK_HEAD_ON_PAUSE                      // Park the nozzle during pause and filament change.
```
--->
  
---  

## Known 'Restrictions'
In case you didn't want to look into the belonging config files or the above 'summary' yourself, let me point out the (imho) most important 'restrictions' that apply to this model.  

In the following I'll list the default values for certain settings. Some of them you probably *have* to adjust (like the e-steps "E0 = 455 steps/mm)"), some of them you *can* adjust (like the maximum feed rates).  
Even though many YouTube videos and other tutorials tell you to adjust the setting for the steps of the X, Y and Z motors for calibration, I *strongly* recommend *not* doing so! The steps for the motors of the *axes* are determined by the specs of the hardware and shouldn't be changed!   
However, be careful when changing *any* settings and keep in mind what the original setting was.  

**The settings are always shown in the following order: X, Y, Z, E0 (= extruder)**   

---

### Default Axis Steps Per Unit  
```
/**
 * Default Axis Steps Per Unit (linear=steps/mm, rotational=steps/°)
 * Override with M92
 *                                      X, Y, Z [, I [, J [, K...]]], E0 [, E1[, E2...]]
 */
#define DEFAULT_AXIS_STEPS_PER_UNIT   { 80, 80, 400, 455}
```

??? info  
  
    During the calibration of your printer it might be necessary to adjust the settings of the steps for the extruder (E0).  
    Even though many YouTube videos and other tutorials tell you to adjust the setting for the steps of the X, Y and Z motors for calibration as well, I *strongly* recommend *not* doing so! The steps for the motors of the *axes* are determined by the specs of the hardware and shouldn't be changed!  

---
      
### Default Max Feed Rate 
```
/**
 * Default Max Feed Rate (linear=mm/s, rotational=°/s)
 * Override with M203
 *                                      X, Y, Z [, I [, J [, K...]]], E0 [, E1[, E2...]]
 */
#define DEFAULT_MAX_FEEDRATE          { 300, 300, 5, 25 }
```

??? warning "Limited Retraction Speed"

    So in case you were trying to find the optimum retraction speed and therefore printing retraction towers and wondered why there wasn't any real difference between e.g. 30mm/s, 40mm/s and 50mm/s, the reason is simple - they just didn't apply!  
  
    Yes, you've read correct: the retraction speed you set at your slicer got ignored in case it was higher than 25mm/s, because 25mm/s is the limit for the feed rate which is set in the firmware.  
    Kinda 'sweet', isn't it? I know what you're thinking right now, I thought the same.. ;)  

    *As you can see above, the "DEFAULT_MAX_FEEDRATE" for E0 (which is the extruder) is set to 25mm/s.*  

    So in case you want or need to set this value higher (do at your own risk though!), see the expandable box below.
  
??? example "Setting a Higher Maximum Value for Retraction Speed"  

    If you want to set a higher maximum value for the retraction speed, you can do it as in the following description (do at your own risk though!).  
    
    - Open OctoPrint or whichever program you use to get access to a terminal for sending G-codes directly to the printer.  
    - Type in `M503` to get a report of the settings. If you scroll up at the beginning of the output, you'll see these lines:  
        ```
        Recv: echo:; Maximum feedrates (units/s):
        Recv: echo:  M203 X300.00 Y300.00 Z4.00 E25.00
        ``` 
        E25.00 is the maximum retraction speed that's possible due to the default setting of the firmware. Anything above it coming from the slicer as a command is being ignored, anything lower will be taken into account (as these are the limits).  
    - Now type in e.g. `M203 E50` to set the new limit to 50mm/s (choose this value wisely and use small increments to go higher).
    - After doing so, type `M500` to store the new value in the EEPROM.  
    - To check if everything got applied and saved now, you can either query `M501` or switch off the printer, switch it on again and check the settings with `M503` again.  
        The abovementioned line should be changed to this now:  
        ```
        Recv: echo:; Maximum feedrates (units/s):
        Recv: echo:  M203 X300.00 Y300.00 Z4.00 E50.00
        ``` 
        
    Now you can start trying to find the best retraction speed that may be above 25mm/s by printing retraction towers. 

---
      
### Default Max Acceleration
  
```
/**
 * Default Max Acceleration (speed change with time) (linear=mm/(s^2), rotational=°/(s^2))
 * (Maximum start speed for accelerated moves)
 * Override with M201
 *                                      X, Y, Z [, I [, J [, K...]]], E0 [, E1[, E2...]]
 */
#define DEFAULT_MAX_ACCELERATION      { 3000, 3000, 500, 10000 }
```

---

### Default Acceleration
```
/**
 * Default Acceleration (speed change with time) (linear=mm/(s^2), rotational=°/(s^2))
 * Override with M204
 *
 *   M204 P    Acceleration
 *   M204 R    Retract Acceleration
 *   M204 T    Travel Acceleration
 */
#define DEFAULT_ACCELERATION          3000    // X, Y, Z and E acceleration for printing moves
#define DEFAULT_RETRACT_ACCELERATION  3000    // E acceleration for retracts
#define DEFAULT_TRAVEL_ACCELERATION   3000    // X, Y, Z acceleration for travel (non printing) moves
```

---

### Jerk Limits 
```
/**
 * Default Jerk limits (mm/s)
 * Override with M205 X Y Z . . . E
 *
 * "Jerk" specifies the minimum speed change that requires acceleration.
 * When changing speed and direction, if the difference is less than the
 * value set here, it may happen instantaneously.
 */
#define CLASSIC_JERK
#if ENABLED(CLASSIC_JERK)
  #define DEFAULT_XJERK 10.0
  #define DEFAULT_YJERK 10.0
  #define DEFAULT_ZJERK  0.3

...

#define DEFAULT_EJERK    5.0  // May be used by Linear Advance
```

---



---
<!--
### Linear Advance  
The useful function "Linear Advance" is NOT activated!  
This seems to be due to the fact that (afaik) there's some kind of problem with Marlin firmware versions before v2.1 and TMC2208 stepper drivers. 
-->



   
  
## Mods
Once I'll come across compiled and modded versions of the original firmware which are being offered by users, I'll list them here.  
  
!!! warning

    Use at your own risk!  

  


---

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/U6U5NPB51)  

