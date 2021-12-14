# GrBLDC3
Uno Shield for grblDD: closed loop spindle VFD + 4 stepper drivers

Main Controller PCB for GG3.  Hardware version 3B
This is the 1st PCB shipped in GG3.

PCB designed in KiCAD.

Changes (from the previous prototype PCB):

-3-pin header order changed from VGS to VSG (e.g. from +-X to +X-).  This creates an incompatibility issue with GG2 units, which will require a pin swap.

-Removed Door Switch (which also restored previous gap for zip tie).

-Vref changed to 1.78 volts (added 1k series with pulldown).

-Added two additional stepper power modes, to reduce power consumption at idle, and to (briefly) increase power if X axis is binding, or if BLDC controller is bogged down in a corner.

-Stepper X1 is now disabled unless A0_STEP_X1_EN is pulled high... this pin is shared with 64M1 reset, which means that when the X1 stepper (only) is disabled, the spindle will not spin.

-Replaced 2x1 screw terminal probe connector with 5x1 SIP.  This is now the only wire harness that goes to LED PCB.  24V and 5V are current limited on this PCB, so that metal chips contacting LED PCB don't affect GrBLDC.

-Added Zener protection diode to 5V rail, in the hope that if 24V finds its way onto that rail, the zener will short it out... this will of course burn out the zener, but hopefully by then the PTC on the Uno will have opened.

-Fixed incorrect pinout on A4910 (pins 39 & 40 swapped).

-BLDC Hall connector changed from 1x5 to 2x3, to make assembling easier.  6th pin is now connected to spindle wipers.

-Removed 2x3 64M1 programming header; connected SPI to Arduino pins instead.  328p can now program this part in-situ (via temporarily loading SPI bitbang firmware onto 328p).

-Emergency stop now pulls BLDC and stepper drivers into reset.

-Emergency stop interface to 328p fixed, such that computer can now pulse reset line during firmware updates.  When estop enabled, 328p continuously held in reset.

-Z stepper connector changed to 2x2, so that it fits through gantry bushings.

-24V/GND/GND 45 degree connector now fits (moved fan connector and capacitors).


New Parts:  
LED PCB:  
102-5777-ND  
Get longer right angle SIPs for LED PCB  
LED - 732-5660-1-ND  