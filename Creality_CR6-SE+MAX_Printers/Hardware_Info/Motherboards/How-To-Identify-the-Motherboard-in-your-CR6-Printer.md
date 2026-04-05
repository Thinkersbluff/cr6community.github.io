***

## How do I know if I have a Creality v4.5.2 or v4.5.3 or ERA1.1 motherboard?

- You can open your printer - the motherboard version is printed on the face of the board, as highlighted in the pictures below.
- IF you know that the motherboard in your printer was never replaced, then these guidelines may help you make a reasonable guess:
   - If you have a CR-6 with a serial number before December 2020 (P202J*[month]*K[number]) you will have a v4.5.2 motherboard
   - If your stock firmware was v1.0.3.7 or v1.0.2 you have a v4.5.2 motherboard
   - If your stock firmware was v1.4.x or higher, you have a v4.5.3 or 1.1 ERA motherboard
![4 5 2 mainboard_annotated](https://user-images.githubusercontent.com/36551518/162257740-e127402d-8512-4769-b223-45379f0c8396.png)
![4 5 3 mainboard_annotated](https://user-images.githubusercontent.com/36551518/162257804-8ad60c80-5942-4d10-9fb0-1f1588cabb02.png)
![era1 1 0 3_Layout](https://user-images.githubusercontent.com/36551518/162259301-2d5b5bdf-805c-48fa-a4d7-64a25cd79884.jpg)

And this is the BTT SKR CR6 motherboard, in case you have none of the above...

![BTTskrCR6](https://user-images.githubusercontent.com/36551518/192142774-d5500af4-7ef0-41ef-8e0e-2436ed213f85.jpg)

***

## I don't want to open my printer. What happens if I install the firmware for the v4.5.3 motherboard on my v4.5.2 motherboard?

No smoke - or at least, not due to the firmware. 

However:
* During homing the printer won't be able to read the optical sensor on the gantry, so it won't know when to listen to the strain gauge and may drive the nozzle into the print bed. 
* You will see a "Heaters Failed" warning if you try to heat the bed or nozzle, because Creality changed which pins they connect the heaters to, after 4.5.2, and Marlin notices if the temperature readings don't increase when it turns a heater on.
* The part cooling fan will not respond to ON/OFF commands

pins_CREALITY_4.5.2.h reads:

* #define BOARD_NAME "Creality v4.5.2"
* #define HEATER_0_PIN                        PA1   // HEATER1
* #define HEATER_BED_PIN                      PA2   // HOT BED
* #define FAN_PIN                             PA0   // FAN
* #define PROBE_ACTIVATION_SWITCH_PIN         PC6   // Optoswitch to Enable Z Probe

pins_CREALITY_4.5.3.h reads: (same file apparently applies to the ERA board)

* #define HEATER_0_PIN                        PB14  // HEATER1
* #define HEATER_BED_PIN                      PB13  // HOT BED
* #define FAN_PIN                             PB15  // FAN
* #define PROBE_ACTIVATION_SWITCH_PIN         PB2   // Optoswitch to Enable Z Probe
* #define J1_PIN                              PA0
* #define J2_PIN                              PB2
* #define J3_PIN                              PA15
* #define J4_PIN                              PB12
