***

## WAIT!  If you prefer to watch videos - you might prefer to go here, instead:** https://www.youtube.com/playlist?list=PLfDSKnF0RNcYDkxM5mYtyuvlTfMAMD-Nr

## NO, WAIT!! If your intention is to install the Community Firmware to "try", expecting to be able to revert to Creality stock firmware if you change your mind, please read the last section on this page first!  We cannot guarantee that there will be a way to revert your printer to the "as-received" condition.

# First, figure-out which "variant" of printer you have!

Creality has delivered multiple variants of CR6 printer and they do not all work with the same pre-compiled Community firmware.
Some of the modifications you make to your printer may also require you to compile your own "flavour" of this firmware.

Only you - the owner-operator of your printer - can determine with confidence to which machine you are flashing.
If you can not make this determination with confidence, you should not try to flash any firmware to your printer.  You may instead just render your printer unuseable...

e.g. Kickstarter CR6-SE printers were delivered with Creality v1.x firmware and a DGUS2 kernel which they did not include on the SD card and copies of which have not been found online.  If you flash the DGUS kernel upgrade files to such a printer, there may be no road back to restore those printers to stock.

## Identify the Model

You probably know this one - CR6 is available in two models:
1. CR6-SE
2. CR6-MAX

## Identify the Motherboard

Yes, you probably have to open the control board case to inspect the board for this one.

See this page for more details: [How To Identify the Motherboard in your CR6 Printer](https://github.com/CR6Community/Marlin/wiki/How-To-Identify-the-Motherboard-in-your-CR6-Printer)  
  
  
_(NOTE: If you decide to just guess which board is probably in there, and you guess wrong, you may plough the nozzle into the bed when you home, your heaters will not work, and the part cooling fan will not work. Your call.)_ 

## If you have installed a BTT TFT display
You can skip the following sections talking about DWIN displays - they do not apply to you.

## If you have a DWIN TFT display: identify the version of DGUS2 kernel currently installed on your display

You need to make an informed decision about whether or not to flash DGUS2 v3.5 kernel upgrade files to your display

Approximately December 2021, Creality started delivering CR6 printers with displays flashed with DGUS2* v4.5 or higher.
(*DGUS2 is the operating system on the DWIN Thin-Film Transistor (TFT) display.)

Creality makes no mention of this change in their documentation or support pages, but **you need to know what is on there, before you flash the Community 6.1-Final (or prior) Touchscreen firmware**.

* The Touchscreen firmware bundled in with the Community Firmware at versions 6.1-Final and prior is NOT compatible with DGUS2 variants other than v3.5. 
* Flashing v3.5 kernel "upgrade" files to a screen previously flashed with DGUS2 v4.5 requires additional steps to recalibrate the display and going back to stock gets even more complicated.  
* As mentioned above, Kickstarter CR6-SE printers were delivered with Creality v1.x firmware and a DGUS2 kernel which they did not include on the SD card and copies of which have not been found online.  If you flash the DGUS kernel upgrade files to such a printer, there may be no road back to restore it to stock.

Much easier all-around to just figure out what you are modifying, before you start.

### Here is [How To Identify Which DGUS2 OS is On Your DWIN Display](https://github.com/CR6Community/Marlin/wiki/How-To-Identify-Which-DGUS2-OS-is-On-Your-DWIN-Display/)

Go there, now, and come back here when you know which DWIN_SET (and DGUS2 files, if applicable) to flash to your display.

**NOTE: If you "did the guy-thing" and flashed your v4.5 system with v3.5 before reading this guide, you are now going to have to either recalibrate your display or flash back the DGUS2 for which your display touchscreen is currently calibrated.  The README with the REFACTORED firmware will guide you on how to flash back to DGUS2v4.5 or 3.5, as applicable.** [This video](https://youtu.be/0xwFGiyg4Z8) may help.

# Look for the latest pre-compiled firmware specifically configured for your variant in the Releases section of the Community/Marlin repository

The Marlin software on which the CF is based requires that some configuration "switches" be set before compiling the firmware.
The Community Firmware developers maintain a limited set of basic Community Firmware configurations in the Releases section of the repository. 

![image](https://user-images.githubusercontent.com/36551518/170330793-459bf134-32b4-4a74-956a-c41d5ad5a6b5.png)
![image](https://user-images.githubusercontent.com/36551518/170330896-b65927cf-9235-48c1-ba16-4157d1025c74.png)


If you have a modified printer that needs an unsupported configuration, you will need instead to learn how to compile your own firmware.


# Now follow the README instructions bundled in with the applicable .zip file

BUT **remember that those files were released BEFORE Creality changed the game by flashing DGUS2 v4.5 or higher to their displays, so they call for you to copy and flash the DGUS2 Kernel Upgrade files as part of the flashing process. NOW we and you know better! SO:**

## First, install the motherboard firmware
Follow the README instructions bundled with the motherboard firmware.
Once flashed, the display will no longer boot to a menu screen until you also flash the matching DWIN_SET as instructed below.
DO NOT just start installing the display firmware bundled into the motherboard zip file!

## Follow the applicable instructions HERE based on which DGUS2 you have on yours, when you get to flashing the Display Firmware!:
**NOTE: In each case, how to "flash..." is detailed in a README file bundled with the applicable firmware.**
Detailed instructions for how to flash the latest Re-Factored DWIN_SET are also posted to the default CR-6-Touchscreen repo website, at [https://cr6community-support-team.gitbook.io/cr6comm-touchscreen-refactored-firmware-docs/introduction/welcome](https://cr6community-support-team.gitbook.io/cr6comm-touchscreen-refactored-firmware-docs/introduction/welcome).  Unlike the README files bundled into the zip files, the GitBook version (and this Wiki) can be updated and corrected, as we learn from your feedback what makes sense to you and what doesn't. 

### If your current DGUS2 version is 4.5 or higher
**The DWIN touchscreen hardware calibration when running DGUS2v4.5 and higher is DIFFERENT from the calibration required to run DGUS2v3.5.**  
_**THIS is why it really matters** to figure out which version is on your system before you start flashing DWIN_SET or DGUS kernel upgrade files._  
  
**DO NOT flash any other DGUS2 Kernel files to your display.**  
  
We recommend that you now proceed to flash the Black/Grey/Red-themed Re-Factored DWIN_SET v1.1 bundled into [Re-Factored.DWIN_SET.Version1.1.2.zip](https://github.com/CR6Community/CR-6-touchscreen/releases/download/Re-Factored_v1.1/Re-Factored.DWIN_SET.Version1.1.2.zip) on [the CR6CommunityFirmware/CR-6-Touchscreen repo](https://github.com/CR6Community/CR-6-touchscreen/releases/tag/Re-Factored_v1.1)  Follow the README instructions bundled with the firmware or [follow the new online documentation here on GitBook.](https://cr6community-support-team.gitbook.io/cr6comm-touchscreen-refactored-firmware-docs/introduction/welcome)
  
Alternatively, you can proceed to flash the (Cyan-Themed) Re-Factored DWIN_SET v1 bundled into [_CR-6_new-hardware-revision-touchscreen-firmware61F_220622_v1.zip](https://github.com/CR6Community/Marlin/releases/download/v2.0.8.1-cr6-community-release-6.1/_CR-6_new-hardware-revision-touchscreen-firmware61F_220622_v1.zip) on [the CR6CommunityFirmware/Marlin repo] Follow the README instructions bundled with the firmware.  
(https://github.com/CR6Community/Marlin/releases/tag/v2.0.8.1-cr6-community-release-6.1)(However, the cyan screens are not to everyone's taste and some users are bothered by the visible jpeg artifacts.)  

### If your current DGUS2 version is 3.5
**You already have the recommended version of DGUS2 on your system. We recommend that you DO NOT flash any other DGUS2 files to your display.**  
  
You can now proceed to flash any ONE of these DWIN_SET variants to your display:  
- The original CF6.1 DWIN_SET bundled into CR-6-touchscreen-2021-06-04.zip  Follow the README instructions bundled with the firmware.
OR  
- The (Cyan-Themed) Re-Factored DWIN_SET v1 bundled into [_CR-6_new-hardware-revision-touchscreen-firmware61F_220622_v1.zip](https://github.com/CR6Community/Marlin/releases/download/v2.0.8.1-cr6-community-release-6.1/_CR-6_new-hardware-revision-touchscreen-firmware61F_220622_v1.zip) on [the CR6CommunityFirmware/Marlin repo](https://github.com/CR6Community/Marlin/releases/tag/v2.0.8.1-cr6-community-release-6.1)(Caution - the cyan screens are not to everyone's taste and some are bothered by the visible jpeg artifacts.)  Follow the README instructions bundled with the firmware.
OR  
- The Black/Grey/Red-themed Re-Factored DWIN_SET v1.1 bundled into [Re-Factored.DWIN_SET.Version1.1.2.zip](https://github.com/CR6Community/CR-6-touchscreen/releases/download/Re-Factored_v1.1/Re-Factored.DWIN_SET.Version1.1.2.zip) on [the CR6CommunityFirmware/CR-6-Touchscreen repo](https://github.com/CR6Community/CR-6-touchscreen/releases/tag/Re-Factored_v1.1) Follow the README instructions bundled with the firmware or [follow the new online documentation here on GitBook.](https://cr6community-support-team.gitbook.io/cr6comm-touchscreen-refactored-firmware-docs/introduction/welcome)

CAUTION: If you are installing this firmware on a CR6-MAX printer, the animation sequence on the Automatic Bed Leveling screen is less "elegant" in the Re-Factored firmware than in the original.  
- The original DWIN_SET displays a dot as the probe samples bed mesh points between the displayed mesh values.
- The Re-Factored version does not.

On the other hand, the Re-Factored version adds a "Leveling Settings" button to the SetUp menu AND adds a display of the last-reported thermistor values to the thermal error shutdown warning screens, in an effort to help you determine whether the problem lies with the nozzle or the bed.

We detail HOW to flash your display in: [How To Flash Firmware to the CR6 printer](https://github.com/CR6Community/Marlin/wiki/How-To-Flash-Firmware-to-the-CR6-printer/).  

### If your current DGUS2 version is between 3.6 and 4.4 (including 3.6 and 4.4)
**We recommend that you DO NOT flash any other DGUS2 files to your display.**  This will preserve your ability to flash back to the Creality stock firmware, without having to locate a copy of the particular DGUS2 kernel files for reverting your system. If, instead, you flash DGUS2v3.5 to your system (e.g. so that you can flash the original CF6.1 DWIN_SET) you will not be able to revert to the more recent DGUS2 if you subsequently decide to revert to stock.  We do not know whether Creality are using any of the DGUS2 features to support the stock DWIN_SET. You may not want to take that chance...

We recommend that you now proceed to flash the Black/Grey/Red-themed Re-Factored DWIN_SET v1.1 bundled into [Re-Factored.DWIN_SET.Version1.1.2.zip](https://github.com/CR6Community/CR-6-touchscreen/releases/download/Re-Factored_v1.1/Re-Factored.DWIN_SET.Version1.1.2.zip) on [the CR6CommunityFirmware/CR-6-Touchscreen repo](https://github.com/CR6Community/CR-6-touchscreen/releases/tag/Re-Factored_v1.1)   Follow the README instructions bundled with the firmware or [follow the new online documentation here on GitBook.](https://cr6community-support-team.gitbook.io/cr6comm-touchscreen-refactored-firmware-docs/introduction/welcome)

### If your current DGUS2 version is less than 3.5
*We recommend that you flash the DGUS2 v3.5 kernel upgrade files to your display.*  
You will find these files in the file CR-6-touchscreen-2021-06-04.zip, which is in turn zipped inside the firmware.zip file that you downloaded for your motherboard from the CR6CommunityFirmware/Marlin repo. (CR-6-touchscreen-2021-06-04.zip has the same contents, regardless of the motherboard version.)  

You can then flash any ONE of the DWIN_SET variants itemized in the section, "If your current DGUS2 version is 3.5", above.
  

# HELP! - Flashing did not work!

Rats!

While we know the firmware flashes just fine on all of our machines, we sometimes find that Creality has modified their design (e.g they changed from 4.5.3 to 1.1.0.3 motherboard, they started flashing different variations of DGUS (1.4, 3.4, 4.1, 4.5, etc.), they moved some of the pins and connectors... So we sometimes learn there really is a new problem to be debugged.  A lot of the time, though, a user has just not followed the documented instructions.  Your first best bet when flashing does not work is to go back over the instructions and figure out whether you skipped a step or did something we caution against.

The second most likely culprit is the SD card.
Sectors go bad, bootloader routines are "touchy", motherboards may work with cards that displays will not, or vice versa.
If all else fails, try deep-formatting the card.

Hopefully, the troubleshooting FAQs on this page will help you figure out what happened and how to recover: [FAQs](https://github.com/CR6Community/Marlin/wiki/Frequently-Asked-Questions-(FAQs)-about-the-CR6-Community-Firmware)

# I want to flash my printer back to Creality stock - how do I do that?

Well, as they say, "We are sorry to see you "go"."

To the best of our knowledge, the instructions on [this FAQ page](https://github.com/CR6Community/Marlin/wiki/How-To-Flash-the-Stock-Firmware-Back-to-the-CR6-printer) will enable you to revert your CR6-SE or CR6-MAX to the Creality stock firmware.  

Please let us know on the Discord #firmware-flashing channel, if you have any problems when following those instructions.