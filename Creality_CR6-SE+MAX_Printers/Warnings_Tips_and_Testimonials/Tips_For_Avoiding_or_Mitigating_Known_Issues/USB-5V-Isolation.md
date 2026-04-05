# Does this tip apply to my motherboard?
- New ERA 1.1.0.3 - No, does NOT apply. Creality changed the design of this board, to eliminate the mixing of USB 5vdc power.
- "Old" ERA 1.1.0.3 - Maybe? Creality does not renumber its boards when making some changes. See "What can I do.." below for more.
- 4.5.3 - Yes
- 4.5.2 - Yes
- BTT SKR CR6 - Yes.

# How does this 5vdc get in via the USB port?
On motherboards affected by this issue, there is typically a diode connecting the 5vdc power pin on the USB connector to the motherboard Vcc bus, allowing the two 5vdc supplies to "mix".  Any external usb device connected to that port through a data or power cable will likely provide +5vdc power on that pin.

# Is this a common issue? 
Yes, at least prior to the 1.1.0.3-ERA motherboards.  This particular issue is not limited to CR6 or Creality printers, either.  

# What kind of problems can it cause?
The nature and significance of problems caused by external devices connected to the USB port on CR6 printers can vary. On some printers, the display remains lit when the printer power is turned off.
On some, the mainboard processor may not reset properly when printer power is cycled, which can in-turn cause strange behaviours from the printer.

# What can I do, to block the 5vdc?
## On the latest (1.1.0.3-ERA) boards
You do not need to do anything. According to the knowledgeable on Reddit, Creality has started leaving that diode (designated D601) off the board.  

## On "older" 1.1.0.3-ERA boards
Since Creality does not consistently change board number when changing configuration, it is worth checking for the diode D601.  If you do find it installed, you can unsolder or cut it off.

## On the 4.5.3 board
You can unsolder or cut off diode D17.

## On the 4.5.2 board
You can unsolder or cut off diode D18.

<img src="https://cdn.discordapp.com/attachments/759605585246421035/984167878817353818/image0.jpg" width="600">

## On the BTT SKR CR6 board
We don't know whether it is diode D13 or not.  If you figure it out, please let us know we will update this tip.  
If you are not a gambler, please try one of the following alternatives.

## Alternatively
### You can modify the cable itself
- A small piece of tape over the 5vdc pin in the USB-A connector covers the power pin.  
CAUTION - I did eventually break a pin inside my laptop USB port, which I suspect may have been because of this piece of tape...
<img src="https://user-images.githubusercontent.com/36551518/172841568-362f1f99-8a65-4494-b31d-b9e8c4d39914.jpeg" width="300"> 

OR  

- You can cut the cable insulation to expose the (red) power wire and cut and insulate that.  

OR  

### You can install a power blocker between the external device and the usb cable
The Power Blough-R, for instance, is specifically marketed for this purpose.
https://www.th3dstudio.com/product/power-blough-r-pi-usb-power-blocker/  

OR  

### You can use a USB splitter with switchable ports and turn off the port power
This tip contributed by a Community member who says the port still passes data, but disconnects the power line.

# DISCLAIMER: As always, we accept no responsibility for any consequences of you acting on this advice. We do our best to help, but can not verify the correctness of all information provided. If you choose to act on this advice, understand that it is at your own risk.