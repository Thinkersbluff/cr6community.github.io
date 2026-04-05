***

## Are there any plans to update the CF beyond version 6.1?

Yes and No.

The published goal of the CF project has always been to clean up the CR6 source code, so that it can be merged back into the upstream Marlin master branch. 

Once the Community Firmware was stable - at version 6.1 - it was passed on to the Marlin team to perform that merge. 

This was the active Pull Request tracking the upstream activity re-integrating the CR6 Community Firmware fork into the upstream Marlin firmware: [Creality CR-6 SE #19958](https://github.com/MarlinFirmware/Marlin/pull/19958) 

Unfortunately, that Pull Request was not processed as intended and hoped by the CF developers.  The upstream Marlin team instead changed the architecture of Marlin at 2.1.x, deprecating some of the functions exploited by the CF and removing the folder and modules by which the CF developers had achieved their Marlin integration.

As of today (4 April 2026), there is no ongoing effort to update the CR6Community Firmware with Marlin.  

Version 6.1 of the CR6 Community Firmware is "frozen" at Marlin 2.0.8.1

A version 6.2 of that Marlin-based firmware is available at this fork of the original project.  It is supported by a Python Configuration wizard and it incorporates a few minor edits into 6.1, but it is _definitely not_ updated to the full Marlin 2.0.9.1 release cited in the Configuration files: [https://github.com/Thinkersbluff/CR6Community-Marlin_TB](https://github.com/Thinkersbluff/CR6Community-Marlin_TB)

A Klipper-based version of CR6Community Firmware is also available at this repository: [https://github.com/Thinkersbluff/DGUS-Reloaded_for_CR6-Klipper_Component](https://github.com/Thinkersbluff/DGUS-Reloaded_for_CR6-Klipper_Component)

The Klipper-based version continues to work with the latest version of Klipper3D. 

The Marlin-based CF does not work with any version of the Marlin firmware.

***

## The temperatures go up/down/up/down while bed leveling
![image](https://user-images.githubusercontent.com/36551518/162470386-fdb3c774-3bdc-4472-a652-4721bf7a669e.png)

Yep.
That is by design, to improve bed leveling accuracy. It impacts all probing activity.

You can turn that behaviour off by deactivating the "Better Accuracy" switch at the top of the Calibrate->Leveling->Leveling Settings screen (not recommended).

***

## I have a v1.1.0.3-ERA motherboard. What firmware do I flash?

![image](https://user-images.githubusercontent.com/36551518/162474960-f50e6ec7-eb5a-4c7e-ae5b-f2b510c71799.png)

All CF6 users on our Discord confirm to us that their ERA-based system works correctly, after flashing the v4.5.3 firmware.  You do, however, need to ensure that the optical sensor is plugged into J705 on the ERA board.  Creality firmware seems tolerant of that sensor being connected to the socket J706, but the Community Firmware is not.  

***

## My nozzle is driven into the bed

If Creality's "Black Box" ABL system on that breakout board is not sensing enough of a change from the strain gauge, it can drive the head down as far as the Marlin firmware is programmed to allow (2mm in the Community Firmware) before stopping. If the printer is not able to push the nozzle that far, the motor will just keep trying to lower the head further until you power-off the machine.  This behaviour has been known to press a dimple into expensive flexible print beds...    

1. Verify that the ABL system can detect the nozzle striking something (or vice versa)

To determine whether the Black Box is able to detect the nozzle striking the bed, try tapping on the nozzle with an allen key and watch the little blue LED on that break-out board.  If the LED flashes, then the system is working, move on to Check the Optical sensor.

2. Check that the optical sensor subsystem is working

* Ensure that the metal probe attached to the gantry is pointing straight down (some have been bent during shipping).
* Ensure that the metal probe descends in between the two short arms of the optical sensor before the nozzle reqches the bed. Some users have found that their nozzle encounters the bed before that metal tab descends into the optical sensor.  There is a printable mount on repositores like Thingiverse that allows you to mount the optical sensor higher, if required. (There's your clue that you are not the first to have this problem)
* Ensure that the optical sensor is properly connected. You can verify this by running command `M119` from a serial monitor, blocking the optical sensor, and running the command again. You should see a difference in the output, regarding the `probe_en` endstop. 

If the sensor is not working, and if you have one of the Kickstarter machines, those shipped with a spare optical sensor - try installing that.

If your optical sensor is broken and you have no spare, you can [build the firmware yourself](https://damsteen.nl/blog/2021/01/08/how-to-compile-cr6community-marlin-with-vscode-platformio) with the option '#define PROBE_ACTIVATION_SWITCH` commented out.

3. Update your firmware to version 6.1-Final

A previous release of the community firmware was (incorrectly) tolerant of the optical sensor being connected incorrectly. 
* On the 4.5.2 board, it should be connected to J1.
* On the v4.5.3 board it should be connected to port J2. 
* On the 1.1 ERA board, it should be connected to J705.
* On the BTT SKR board, it is connected to the Z-Stop connector.

NOTE: On the BTT SKR board, the red led in the Optical Sensor does not illuminate (only being fed 3.3vdc) but the sensor still works.  If you want the red led to also work, you can move the power pin over to 5vdc on the RGB connector, like this:

![Optical5vdcConnection](https://user-images.githubusercontent.com/36551518/192143211-c0f0c836-67a5-4214-99c3-45bc001a3be3.JPG)

***
## I have a BTT SKR CR6 board. How do I activate Neopixels?
In the configs folder of the CF6.1 Release code, you will find examples for Configuration.h, Configuration_adv.h and Platformio.ini, to activate Neopixels on a CR6-SE. 
[config/btt-skr-cr6-with-stock-creality-tft-neopixel](https://github.com/Thinkersbluff/CR6CommunityMarlin_BTTCR6/tree/extui/config/btt-skr-cr6-with-stock-creality-tft-neopixel)

A utility like [WinMerge](https://winmerge.org/downloads/?lang=en) is ideal, for comparing your current configuration files to those examples, and for making the equivalent changes in yours. Then recompile.

NOTE: The ellensp GitHub repo referenced in those files has since been taken down, so you need to make these two changes, to successfully compile:

If your platformio.ini contains the highlighted line, you need to replace it with this:
NeoPixel=https://github.com/bigtreetech/Adafruit_NeoPixel

![](https://media.discordapp.net/attachments/783281341180411915/966527682705760297/platformio_ini.png)

Same thing with ini/stm32f1.ini

![](https://media.discordapp.net/attachments/783281341180411915/966529189555613726/stm32f1_ini.png)


***
## My printer reboots when printing (Creality v4.5.2 boards)

Make sure your SD card isn't corrupt. Also some v4.5.2 boards do not "like" some types/brands of SD cards.

A small number of v4.5.2 boards also get overloaded by the more features that are enabled by the firmware. For most boards it isn't an issue, but some particular v4.5.2 boards are unstable. Nothing you can do, stock firmware only, for you - or upgrade to a CR-ERA v1.1.0.3 or, if you can still find one, [a BigTreeTech SKR CR6 board](https://damsteen.nl/blog/2021/01/24/bigtreetrech-skr-cr6-review).

You can also try `CF[version]-cr6-se-v4.5.2-mb-no-watchdog-[date].zip` firmware, but be aware: if the firmware does freeze then there is nothing that prevents the printer from overheating, with the watchdog timer function disabled. Use with caution!

***
## I would like to customize the Community Firmware configuration for my printer - How do I compile my own version?

Our Dev @Sebazzz posted this online guide in his blog: [https://damsteen.nl/blog/2021/01/08/how-to-compile-cr6community-marlin-with-vscode-platformio] (https://damsteen.nl/blog/2021/01/08/how-to-compile-cr6community-marlin-with-vscode-platformio)


**Please note**, that due to changes made to both Visual Studio Code and Platformio since that blog was posted:

In the section, "Download source code package", we strongly recommend that you ONLY follow option 2; "Download the Source.zip file from the latest release", which is Release 6.1, except that the files marlin.py and platformio.ini both require changes which have already been incorporated into the files on the CODE page.  

To avoid having to repeat the required modifications to platformio.ini and marlin.py, we recommend that you do download these two specific files and that you use them to replace (overwrite) the older versions of those two files, unpacked from Source.zip:
* [\platformio.ini](https://github.com/CR6Community/Marlin/blob/extui/platformio.ini)
* [\buildroot\share\PlatformIO\scripts\marlin.py](https://github.com/CR6Community/Marlin/blob/extui/buildroot/share/PlatformIO/scripts/marlin.py)


