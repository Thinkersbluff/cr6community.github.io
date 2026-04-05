# You need to make an informed decision about whether or not to flash DGUS2 v3.5 kernel upgrade files to your display.
## Why does it matter?
Basically, if you flash the wrong things to your display, you can end up "bricking" your display.

## How to find which version of DGUS2 is currently installed on your display
### In a Nutshell
To find the current DGUS2 version, you flash an **_empty_** DWIN_SET folder to the display.  
What to do with that information is then explained below.

### Here is the gist of the process:  
1. Find a microSD card (SD cards are best.  HC cards might work.  XC cards might work (but often do NOT))
2. Partition the card per the Master Boot Record (MBR) standard (DOS mode on a MAC) (GUID Partition Table (GPT) will not work with the display.)
3. Format the card to FAT32, with 4096 allocation units per sector. (This requires a partition size of 16GB or less)
4. Create an EMPTY directory in the root of the card, named DWIN_SET
5. With power off, insert that card into the microSD slot on the display PCB (You'll need to take the back off the display case, to access it, if you have not previously [modified your stock display to add an extension cable.](https://www.thingiverse.com/thing:4693106))
6. Taking care not to short the PCB to anything, switch power on.
7. If the display can read your card, the screen will turn blue, the version number of DGUS2 OS currently installed on your display will be written in white across the top of the screen. (Write that down or take a picture, for future reference.)
8. You can ignore the other info on the screen.
9. Power-off
10. Remove the microSD card
11. Either:
* put the display case back together, if you need to take a time-out,  
OR   
* continue to the next steps, if you now intend to flash the Community Firmware.

### EXAMPLE:
Here is an example of a replacement display which arrived from an online vendor, in a Creality box, with no documentation:  
  
<img src="https://user-images.githubusercontent.com/36551518/229612057-d7a48e1f-7fd4-4a66-9c2b-45bb6e7400aa.png" width="300">
      
**NOTE:** DGUS2 v1.4 happens to be the version of DGUS that was installed on the Kickstarter printers.  It is quite out of date, now, but Creality still post it with the 17 May 2020 (Kickstarter) firmware on [the Creality Google Drive.](https://drive.google.com/drive/folders/10-Np-x-ZU_1rkUA9M2IH99KnLTq3AZGd).  
It is also available in the September 2020 v1.0.2 firmware downloadable from [https://forums.creality3dofficial.com/download/cr-series/cr-6-se/](https://forums.creality3dofficial.com/download/cr-series/cr-6-se/)  
  
If this is what you have on your display, you should take this opportunity to update it, as detailed below.

## Once I know which DGUS2 is on my display.  What are the "next steps"?
If you came here from "How To Flash Firmware to the CR6 printer", [go back there now](https://github.com/CR6Community/Marlin/wiki/How-To-Flash-Firmware-to-the-CR6-printer#look-for-the-latest-pre-compiled-firmware-specifically-configured-for-your-variant-in-the-releases-section-of-the-communitymarlin-repository) & complete that process.
When you get to the step where you are selecting and flashing the applicable DWIN_SET for your system, follow the instructions that match the DGUS2 version currently installed on your system.

# Troubleshooting
## If you get a blank screen when flashing an empty DWIN_SET
### Card not formatted as FAT32/4096 allocation units?
We have seen this happen when trying this with small cards (like 128Mb cards).  Double-check the format.  
You may not have noticed, but FAT32/4096 sectors is not an option for formatting smaller cards. Try to find a 4Mb or 8Mb card and try again.  
### Partitioned an XC card?
We find this display sometimes has trouble reading XC technology cards. Try to find an SD technology (e.g. 4Mb or 8Mb) card and try again.  
If your smallest cards are 32Mb, try to find one that is branded as HC technology.  
  
If you created a 16Gb partition on a 32Mb card, double-check that the sector size is 4096. The threshold for formatting with 4096 allocation units is actually slightly smaller than 16Gb of disk space. A 16Gb card reserves some disk space and only allows you to format a little over 15Gb.  If you only have 32Gb cards or larger, try resizing the partition to 15Gb and try again to flash the empty DWIN_SET.
### Multiple partitions or frequently partitioned card?
Windows Disk Manager can sometimes "mess-up" the Partition Table, if you create/delete/modify volumes and partitions on a card.
Verify that there is just one volume, one partition, and that it is reported to be a Healthy Primary (MBR) partition, not a Logical (GPT) partition.  
  
**NOTE: You may need to use a Partition Manager application (like [EaseUS Partition Manager](https://www.easeus.com/partition-manager/epm-free.html), [Paragon Partition Manager](https://www.paragon-software.com/free/pm-express/) or [AOMEI Partition Assistant](https://www.diskpart.com/free-partition-manager.html)) to repair cards which Windows Disk Manager has compromised.  
Alternatively, you might find that you can instead repair the card by formatting it in your digital camera or with a Linux-based or Android-based system, and then "repair"/reformat it in Windows.**

# By The Way: If you did not know this before, you just learned something very important about DWIN_SET and DWIN displays:

Although the displays do have a serial interface connected to the mainboard, some programming of DWIN displays can ONLY be done by loading something into a folder called DWIN_SET on a USB card and "flashing" that content to the display, by cycling power ON.

The display bootloader is actually programmed to look in the root directory of the card for that folder, by that exact name, including the capitalization. It will ignore everything else on the card.
