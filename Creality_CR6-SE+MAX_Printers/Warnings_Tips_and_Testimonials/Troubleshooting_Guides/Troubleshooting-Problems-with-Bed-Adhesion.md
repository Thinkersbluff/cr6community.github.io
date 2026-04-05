***

## I have leveling issues / my prints don't stick to the bed
There are two primary causes for this problem:

1. Your printer may not be configured correctly, to keep the nozzle at the correct distance from the surface of the print bed.
2. Your print bed might not be clean

***

### I think I have leveling issues
#### Your Z-Offset may be wrong

The Z-offset measured by CF6.1 may not be the same as with your previous firmware. 
  There is no assurance that 0.20mm - as recommended by Creality on their stock firmware - will be correct with the Community Firmware. 
  Use the Calibrate menu to measure the new Z Offset. The new value will be stored for you automatically.

***

#### Your Automatic Bed Leveling (ABL) system may not be working well.  

  One of the most significant differences between the Creality stock firmware and the Community Firmware is the starkly different design philosophy of the ABL function.
- The Creality firmware performs ABL with a series of rapid hard "knocks" to the bed. 
- The Community Firmware performs ABL with a series of slow soft taps, and with the Heaters cycled Off/On at each touch, to reduce electrical noise. (A behaviour you can switch off by deactivating the "Better Accuracy" switch at the top of the Calibrate->Leveling->Leveling Settings screen)

  Ideally, the difference between the actual Z position at which the nozzle strikes the bed and the Z position recorded at the point when the ABL system records the "bed-striking" event should be precisely equal to the Z-Offset value, every time.  When the Community Firmware development team began this project, they found that, instead, the Z Offset value on the stock printer tended to vary significantly, from one time to the next, which compromised both print adhesion and print quality.  The actual design of the ABL system has not been released by Creality. The CF6.1 developers have instead done their best to reverse-engineer its design and to hypothesize and anticipate its vulnerabilities to error. They then designed the Community firmware to make the best possible use of Creality's actual hardware/firmware design, treating it as a "Black Box" that they could not modify.  The CF6.1 developer's design decisions may be impacting your printer's performance.  Review each of these carefully, to see whether you might be having one of these known issues:
* You may have deactivated "Better (Probing) Accuracy"
* The Probe Activation Force may be too high

***

#### You may have deactivated "Better (Probing) Accuracy"

  To mitigate the risk that the ABL function might be compromised by Electro-Magnetic Interference (EMI) from the heaters and fans, the Community Firmware - by default - turns-off the heaters and the part cooling fan during each probing event. (The hot end cooling fan is not controllable, so that remains an unmitigated risk.)  

 To accommodate users for whom the impact of the heater cycling behaviour on the nozzle temperature is unacceptable, the Community Firmware includes a "Better Accuracy" button.  (Note: this setting impacts all probing activity  i.e. both Homing and ABL)
This behaviour can be switched off by deactivating the "Better Accuracy" switch at the top of the Calibrate->Leveling->Leveling Settings screen. The Developers caution that doing so may compromise the quality of your ABL mesh.

***

#### The Probe Activation Force may be too high

![image](https://user-images.githubusercontent.com/36551518/162486028-a8c7c636-cf12-4960-b081-a58b30bf45f9.png)
![image](https://user-images.githubusercontent.com/36551518/162486288-77c97acd-badb-4ff5-b7ab-e0e3ed522391.png)
_(Picture credits - @Sebazzz)_

The probe activation force may be too high, or there may be an unintended static force stressing the gauge.  
Our users often report that Creality deliver their CR6 printers with high probe activation forces (often 500-1000g or more), while CF6.1 users often find they need to reduce that activation force to ~150g to stop the probe from pushing the bed down at each probe point.  [This blog by Community Firmware Developer @Sebazzz](https://damsteen.nl/blog/2021/04/19/on-strain-gauge-leveling) explains why and how to tune the probe activation force to work better with CF6.1. (Note: this adjustment impacts all probing activity  i.e. both Homing and ABL)

These lighter activation forces can also make CR6 printers running the CF6.1 firmware more vulnerable to slight stress biases applied to the gauge sensor, through seemingly innocent practices like tie-wrapping the nozzle wire harnesses, or tying the Bowden tube to the wire harness.  Ideally, the measured Z-Offset value should still be  0.20mm, +/- 0.2mm.  If your Z Offset is varying significantly between measurements, then something about your system's physical configuration is putting a variable stress on the gauge, which may not have been noticeable on the Creality stock configuration of firmware and activation force.

If the measured ABL mesh values and/or the measured Z=0 (Home) value are higher than actual, the printer will try to print the first layer too high above the bed, resulting in poor adhesion and poor line separation, as if the Z-Offset was too high.  (It can also cause an incorrect Z-Offset measurement, which will have the opposite effect on the print. (i.e. Measured Z-Offset too high->prints too close to the bed.  ABL measurements too high->prints too far away from the bed.))  If probe measurements are lower than actual (e.g. if the probe is deflecting the bed downward before sensing the bed) then the printer will try to print too close to the bed, possibly even trying to gouge a track in the bed.  This effect is typically seen around the edges of the bed, since the center of the bed sits on the carriage and tends to resist deflection (as long as the eccentric nuts are correctly tightened.)

***

### My prints still don't stick to the bed

Sometimes, bad adhesion is just about cleanliness (or the lack thereof.)  A little bit of finger grease can go a long way, when heated to 50-70 degC.  Like oil in a frying pan, it does not stay only where you put it. Like the food in that pan, plastic will not stick to oil or grease.

Try cleaning your bed with hot water and dish soap. 

If your print bed is PEI or PEX, try roughing-up the surface with 000 steel wool or 1200-grit sandpaper.

If you are desperate, you might try an adhesion helper, like hairspray, glue stick, or one of the bespoke commercial products.
