### behavior of arduino boards and arduino bootloader ###
Arduino boards are equipped with a minimal bootloader and monitor program. There are diverse variants of arduino boards (and bootloaders) and I am not a specialist for this topic (correct me, if somewhat is wrong here).<br>
I'm only writing about the boards arduino duemilanove and arduino Mega.<br>
I think, the explanations can be applied to other boards also.<br>

The fuses bits in this arduinos are programmed for:<br>
- 2 K word bootsection<br>
- start after reset at boot section<br>
- interrupt vector table at address 0<br>
The arduinos are programmed with the bootloader in the 2K word bootsections and a serial communication rate of 57600 baud.<br>

After reset or power up the arduino waits for chars from serial line. If no chars (or wrong chars) are send to the board, the bootloader jumps to address 0000 whether there is an application program or not.<br>
If chars and bytes are received from the bootloader and the sequenze of bytes is conform with the stk500v1 "upload programs format" you can upload a program (or data) in the flash (or eeprom).<br>
The arduino board can be resetted at power on, the button at board or via the DTR-control line of the serial RS232 interface per software. This is useful when you want to restart the monitor per pc program.<br>
<br>
<br>
<i>You can reset arduino boards per software from pc over the serial USB-cable.</i><br>
The software activates the DTR control line of serial port and a capacitor at the board produces an reset impuls.<br>
The arduino integrated development environment (IDE) or avrdude (with the programmer option -carduino) use this software reset for bootloading.<br>
The bootloader shipped with the arduino board waits after reset about 1/2 second for characters from serial USB-port.<br>
If it no chars received, it starts the application program at address 0 (if there is such program!).<br>
If chars were received, the bootloader checks the chars.<br>
If the chars are control sequences of the stk500V1 uploading protocol, uploading software is started. The Arduino-IDE and avrdude send this sequences for uploading.<br>
Within the 1/2 second after reset you can send some '!' chars from a terminal and the bootloader switches to the simple monitor integrated in some arduino bootloaders.<br>
I hope this description is correct!!!<br><br>
<h3>Bamo128 as arduino bootloader</h3>
Bamo128 uploads software and data with the stk500V1 protocol.<br>
After reset it waits about 1/2 second for chars from serial USB port.<br>
If it received such, it jumps to the uploading code and bamo128 (how the arduino boards) upload software.<br>
In the other case (no chars received), it jumps to the monitor and waits endlessly for bamo128 monitor commands.<br>
The main difference is, that arduino boards start applications if no chars were received after reset, but bamo128 jumps to the monitor.<br>
You must start the application with the monitor command:<br>
#> g 0<br>
explicitely.<br>
Feel free to change this behavior in the open bamo128 software.<br>