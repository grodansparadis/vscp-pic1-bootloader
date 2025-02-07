<h1>VSCP PIC1 Bootloader</h1>
VSCP Microchip PIC18F bootloader for use with VSCP over CAN 

This bootloader will work with the VSCP PIC1 algorithm of VSCP Works. For info see 
http://ww1.microchip.com/downloads/en/AppNotes/00247a.pdf 
This bootloader expects a slightly modified version of the bootloader described but 
in most aspects it is the same. The changes just makes it works along side an installed
CAN4VSCP system.

Use file/export in MPLAB(x) after build to write the HEX file.

When programmed into a device and activated (byte 0 in EEPROM is 0xff on startup or the status
button (RC0) is held low on startup) a confirm bootloader mode CAN message with id=0x000014nn/0x000015nn 
and no data will be sent. Node id (nn) (least eight bits of id) is taken from EEPROM byte 1. For a freshly 
written bootloader nn=0xfe and this is also true for a bootloader that is entered by holding the init. button 
and power a board. If the board has been forced in to bootloader mode by the VSCP firmware nn will be the
nickname the node had at that time.

If byte 0 in EEPROM is not oxff on startup a normal boot of the relocated code (offset=0x800) will take place.
Hex files for device programming is available here under the release tab on this site.

On reset id=0x000014fe/0x000015fe should be seen from a device with a pic1 bootloader installed. The nickname 
0xfe is fetched from EEPROM address = 1 and for the bootloader to start the content at EEPROM address= 0 should 
hold 0xff. In all other cases the application code will be started. 

The application program should start at offset 0x800

Ake Hedman, Grodans Paradis AB
akhe@grodansparadis.com
