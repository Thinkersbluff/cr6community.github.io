***

## My screen looks like this picture after flashing it ##

![image](https://github.com/user-attachments/assets/62523673-0825-4ff9-9272-e5f7756c5ebd)

If you prepared the screen-flashing SD card with a MAC, the MAC OS may have modified the .CFG file, when you copy/pasted it.  Your blue screen probably also shows 000 CFG files loaded and 000 BIN files loaded.

[Please follow these instructions very carefully, when preparing your SDCard on a MAC](https://cr6community-support-team.gitbook.io/cr6comm-touchscreen-refactored-firmware-docs/installation-guidelines/detailed-sd-card-formatting-instructions#mac-users)


If all else fails, use a utility like [balenaEtcher](https://etcher.balena.io/) to [flash this image file](https://discord.com/channels/759603746270609428/759605585246421035/1293662899205832765) to an SD card of 8Gb, 16Gb or 32Gb and flash the screen from that card.

***

## After flashing the screen, I can see the main menu screen, but I can't get the buttons to work!

This happens when you flash DGUS2 v3.5 (e.g. by flashing the Touchscreen Firmware + kernel upgrade files bundled with CF6.1) to a display that was calibrated to work with DGUS2 v4.5 or higher.

If, instead, you flash the bundled Touchscreen firmware to a screen running DGUS2v4.5 (or higher) without the "kernel upgrade files", the screen will be blank.

In either case, the problem and one solution are detailed in, "You may need the refactored DWIN_SET...", below.

[This video](https://youtu.be/otaNJFLcuQ8) also explains the problem and demonstrates how to find and flash the refactored Touchscreen firmware.

Alternatively, you can recalibrate the display to work with DGUS2v3.5, as shown at 19:40 in [this video.](https://youtu.be/0xwFGiyg4Z8?t=1180)

***

## After flashing the touch screen it only shows a black display

Four possible causes of this issue have been identified by our users:

1. The display was not running DGUS2 v3.5, after they flashed it
2. There was a loose socket in the display connector and a burned pin on the display PCB
3. There was a pinched broken wire in the display harness
4. The display was shorted to the frame, during the flashing process

***

### You may need the refactored DWIN_SET...

The CF6.1 display firmware bundled with the motherboard firmware only runs on DGUS2 v3.5. 

In June 2021, when CF6.1 was released, all CR6 printers were understood to be sold flashed and calibrated with DGUS2 v3.5 or less. The Touchscreen firmware was therefore bundled with a "kernel upgrade" folder containing three BIN files which ensured that the display OS was v3.5 when the firmware was installed.

In the first quarter of 2022, we began to hear of printers running and calibrated with DGUS2 v4.5 or higher. 
Then we learned that:
   1. Installing the DWIN_SET on DGUS2 v4.5 (i.e. not flashing the kernel upgrade files) resulted in a blank screen (clearly backlit, but no menu displayed.)
   2. Installing DGUS2 v3.5 on those displays caused problems because the v4.5 calibration was not compatible with the v3.5 OS. Users found that pressing the menu buttons did not activate the buttons.  The screen was touch-sensitive, but the printer menu was non-functional.

To resolve this problem, we have now published a refactored version of DWIN_SET and revised instructions.  The refactored version will run on all versions of DGUS2 v2.0 or higher, so no kernel upgrade files are required.

This video tutorial explains the issue and the solution: https://youtu.be/IdOybKu1nn8

***

### There may be Display connector issues (NOTE: This failure mode can also cause a display to flicker)

Pull-check the sockets in the display connector, to be sure they are locked in-place.
Take a close-up picture of the display connector header pins on the display PCB and zoom in to that, looking for any evidence of charring or discolouration.  Try lightly sanding those pins, then reconnect & test again for display operation.

e.g.:
https://cdn.discordapp.com/attachments/759605585246421035/941234783328026654/9E71DB4C-091B-4CB4-969E-C5F62D92A461.jpg

![image](https://user-images.githubusercontent.com/36551518/191604647-980a5cc0-23b8-42f2-8bcf-c28e4a41f206.png)


***

### Check the display cable where it passes behind the drawer

![image](https://user-images.githubusercontent.com/36551518/162474053-7a3f53ea-7d15-4acb-bea0-1bd0d99dc04f.png)

This cable is sometimes trapped and pinched behind the drawer.

***

### Display shorted to the frame

If you shorted the display to the frame while flashing, the blank screen _may_ be temporary.  
Because the DWIN touch screen uses SRAM, it takes a while for the error condition to clear.  Turn off the printer for 5 minutes or more and try re-flashing the display.

***

## Does it matter if I flash the touch screen or motherboard firmware first?

No - you can flash in either order or you can flash both at once. You can also flash both at once, if you wish.
Until you have flashed both motherboard and display to the same release, though, the system will not work correctly.

***

## I'm having trouble flashing the touch screen firmware / things aren't working / I'm seeing garbled or missing text

Try reflashing your touch screen firmware. Read [the flashing instructions](https://github.com/CR6Community/CR-6-touchscreen/blob/extui/src/README.md) *carefully*. The DWIN stock touch screen is *very* picky when it comes to SD cards. Sorry, we nor Creality can't change this.

***

### The screen says "Bootloader May be Confused"

![image](https://user-images.githubusercontent.com/36551518/162478581-03f59683-a397-4a41-8c1e-c13e0438b17e.png)

If the motherboard does not communicate with the display while booting, and the display has been flashed with CF6.1, then this message screen may appear.
Alternatively, you may see the progress bar fill-up, but then the process freezes.
These events usually mean that the motherboard is having trouble reading the Master Boot Record or the firmware bin file on the SD card you are using to flash the motherboard. You may need to use a different SD card.

NOTE: This problem has occured for users who successfully used the SD card to flash the display but then had trouble flashing the motherboard.  Intermittent cards sometimes work, sometimes don't...

***


## I cannot find the kernel upgrade files

NOTE:  These instructions do NOT apply if you are flashing the Refactored Firmware!

![image](https://user-images.githubusercontent.com/36551518/162477264-1bab4256-917f-46b8-ad6e-857cfe92c47b.png)

![image](https://user-images.githubusercontent.com/36551518/162472235-4d4bab85-ba4b-43b8-9def-0c7a00c0dc10.png)

Make sure that the name of the .zip file you are using starts with: "CF6.1 - Final..."  If it doesn't, then you are looking in the wrong file.  Go here [https://github.com/CR6Community/Marlin/releases/tag/v2.0.8.1-cr6-community-release-6.1](https://github.com/CR6Community/Marlin/releases/tag/v2.0.8.1-cr6-community-release-6.1), scroll to the bottom, and download the correct file.

***

## I followed one of the flashing reference videos and they don't copy any kernel upgrade files...

Be aware that the videos we posted may have been recorded before version 6.1 Final was released.  As of version 6.1, flashing the kernel files to the display is NOT OPTIONAL, even if the folks in those videos don't do it.  

[This video tutorial series](https://www.youtube.com/watch?v=Q6738aiEKkU&list=PLfDSKnF0RNcYDkxM5mYtyuvlTfMAMD-Nr) shows the correct way to find, copy and flash CF6.1-Final to your printer.
