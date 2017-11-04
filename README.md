These are the source files for building the MMDVMHost, the program that interfaces to the MMDVM or DVMega on the one side, and a suitable network on the other. It supports D-Star, DMR, P25 Phase 1, and System Fusion.

On the D-Star side the MMDVMHost interfaces with the ircDDB Gateway, on DMR it can connect to BrandMeister, DMR+, HB Link, XLX or [DMRGateway](https://github.com/g4klx/DMRGateway) (to connect to multiple DMR networks at once) on System Fusion it connects to the YSF Gateway. On P25 it connects to the P25 Gateway.

It builds on 32-bit and 64-bit Linux as well as on Windows using Visual Studio 2017 on x86 and x64. It can optionally control various Displays. Currently these are:

- HD44780 (sizes 2x16, 2x40, 4x16, 4x20)
	- Support for HD44780 via 4 bit GPIO connection (user selectable pins)
	- Adafruit 16x2 LCD+Keypad Kits (I2C)
	- Connection via PCF8574 GPIO Extender (I2C)
- Nextion TFTs (sizes 2.4", 2.8", 3.2" and 3.5")
- TFT display sold by Hobbytronics in UK
- OLED 128x64 (SSD1306)
- LCDproc
The Nextion displays can connect to the UART on the Raspberry Pi, or via a USB to TTL serial converter like the FT-232RL. It may also be connected to the UART output of the MMDVM modem (Arduino Due, STM32, Teensy), or to the UART output on the UMP.

The HD44780 displays are integrated with wiringPi for Raspberry Pi based platforms.

The Hobbytronics TFT Display, which is a Pi-Hat, connects to the UART on the Raspbery Pi.

The OLED display needs a extra library see OLED.md

The LCDproc support enables the use of a multitude of other LCD screens. See the [supported devices](http://lcdproc.omnipotent.net/hardware.php3) page on the LCDproc website for more info.


********  NOTE from EA5SW *********


Now Nextion Screen is more complex, all development are made in a Raspberry Pi, is tested in Rpi2 & Rpi3 and use some routines of this hardware, It's possible that only work in Rpi and not in Orange Pi or similar

Are made with DMR only in mind for Hotspots, so only use Timeslot2 and not tested in mixed mode (P25,Dstar,etc)
The code made a new screens for OLED and Nextion screens.

OLED code is more simple, as the screen are small and monocrome, and Nextion display a lot more of information.

At this time displays:

Some extra information::
Locator, City and Frequency.

Real IP number at startup od Pi, etho or wlan detects.
Temperature of Raspberry Pi.
Real time Smeter for MMDVM Modems that outs RSSI information (MMDVM modes with radios as Motorola,for example)
Fake Smeters for the rests of types (DVMEGA,HS_HAT,etc)
Change of colors in sequence Idle/RX/TX of Hotspot.
Talker Alias display of information send by master.
Decode of TG number and display of picture associated to this TG. Now TG's are the EA most used.
Decode of Callsign Prefix and display of picture associated to this Prefix.Now are the EA,EB & EC prefix
Decode of 9990 and 4000 commands also displaying pictures
Decode of own callsign and display of own picture.
Remote Reboot and Shutdown of Pi eligible by sysop via DMR

Install & Run:

Compile and copy Nextion.ini at /home/pi directory

You need to Edit Nextion.ini to suit your callsign,information and TG & Prefixes that acces those picture in the Nextion Screen.

Explanation:

The editable pics are 200x100 and 100x50 pixels

Open the Nextion HMI in Editor and observe the picture list 
Also Open the Nextion.ini file in a editor to see references

0-19 are semi-fixed pictures, change the 8 & 9 with the replace opcion for your own callsign picture

20-29 are the prefixes pictures 3 diferents  prefixes are allocated for every pic, in Nextion.ini section [WPX] you see PXA0,PXB0 and PXC0 and the  prefixes EA0 EB0 and EC0 When you transmit or receive a transmission from these prefixes are displayed the pic 20
If the transmission comes from EA2,EB2 or EC2 prefixes, display picture 21 and all  others.

The TG list are from picture 30 to picture 94, and works same that prefix, the list are in the [TGP] part of Nextion.ini

example:
the TG localed in (TG0=214) when receive a transmission of this TG displays the picture 30 in the Nextion, 214 (EA national Talkgroup) have the picture 30
example of chaange: If yoy want receive the 3100 USA Talkgroup  replace the image in the Nextion display (picture 30) for a USA Flag, change the entry in Nextion.ini TG0=214 for TG0=3100

Remember that any change in Nextion.ini are needed to change in the Nextion Screen and upload again to the display.

Last section are remote control: [CONTROL]
You control if is active when ONOFF=1 or deactivate when ONOFF=0
SHUT=99998 are Shutdown TG to transmit to shutdown the Pi
REBO=99999 are Reboot TG to transmit to shutdown the Pi
Only the Owner  callsign are allowed to TX into those TG to activate functions.

Thanks to the effort of:
G4KLX, ON7LDS,G0WFV, VK6LS & more for code
EA4ATS for all graphics, a very BIG JOB !!
EA5DHO for test,test,test,test and TEST and ideas!!

73 & DX from EA5SW


This software is licenced under the GPL v2 and is intended for amateur and educational use only. Use of this software for commercial purposes is strictly forbidden.
