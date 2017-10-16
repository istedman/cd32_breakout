# cd32_breakout (Untested)
A breakout/riser board for the CD32, based on the Terriblefire design. Added extra video circuitry, some power supply essentials, PC to Amiga keyboard adaptor and an RS232 serial port. Not tested, released to show correct video circuitry and RS232 port information.

# RGB video information

The design may seem over complex but there is a good reason. The Amiga outputs 5V CMOS levels for it's sync signals. For CRT TVs, not an issue. For modern LCD TV, scan-converters and RGB to HDMI adaptors, it is an issue as the >4V signal is more than the typical 3.3V supply on the LCD TV or converter. On my SCART cable, I added a 680R resistor to attenuate the signals, here I've gone 1 step further, used 5V tolerant, 3.3V logic to drive the correct sync levels. This removes the ~1-2 pixel shift delay that the 680R resistor adds and ensure the rise and fall times are compatible with the VESA VSIS spec. The TI SN74LVC1G97DBVR device is perfect for this application, it is used as a 1 of 2 selector.

U1 and U2 are configurable little logice devices. You can either output HSync and Vsync for monitors/adaptors or CSYNC and 2.5V for RGB SCART. A jumper selects the desired mode of operation, leave off for Minimig SCART and fit to output HSync/Vsync. The AMiga DB23 connector has been disposed of, a 15 way HD (VGA) connector is used as you can easily purchase RGB + Hsync + Vsync cables or a Minimig SCART cable (https://github.com/mist-devel/mist-board/wiki/ScartCable)

The RGB outputs on the CD32 are missing the 75R series resistors, so they have been added here. They are required so that when connectoed to a TV/Monitor/adpator with 75R termination a 0.7V peak signal is seen. Without these resistors the receiver will see a 2x signal (1.4V) which may exceed the dynamic range of some video ADCs/decoders. This causes video colour issues.

IC5 is the 5V to 3.3V LDO converter. C5 must be either a Tantalum, Tantalum polymer or electrolytic capacitor. DO NOT FIT A CERAMIC, it will be unstable. Read this to understand why http://www.ti.com/lit/an/snva167a/snva167a.pdf and enjoy pole/zero analysis :)

# RS232 interface

This is a simple interface, it has TTL level TX/RX and by using IC1, RS232 style serial levels. Connection is via JP2 and was intended for debug using Diagrom. Serial port speed is limited to 56K at best on the CD32.

# PS/2 to Amiga keyboard interface

A clone of sorts, of the IBMKEY25 design from http://aminet.net/docs/hard/epic13.lha
The PIC16C84 is expensive to purchase now, so a PIC16F627A is provisioned for. If you use the RC oscillator and a few tweaks, the original software should work. You could also use the MMKEYBOARD-16f627.HEX from the MMKeyboard archive, this is un-tested. If I get the time, I'll fix the firmware for this.

# PCB layout

A routed but un-tested PCB has been provided. The PCB is 127x62mm, the same size as the DCE SX32 shuttleboard. A fixing hole is provided to screw this board into the CD32.

I've added some power supply decoupling capacitors, the EMC engineer in me demands this and large +5V and ground copper pours fill the PCB. This helps provide a low inductance power supply and increases PCB yield (less chance of over-etching).

FMV signals have been disconnected to save space for routing.

Use at your own risk, I've taken every care with the design but have not tested it as of October 2017.
