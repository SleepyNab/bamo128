You can use GNU screen as well, a terminal program, to communicate with bamo128 (without data/program uploading).When screen is invoked, it executes initialization commands from the files .screenrc in the user's home directory.
You can start screen with args also:
#>screen /dev/ttyUSB0 57600
The better way ist to use [arduinokermit](http://code.google.com/p/bamo128/wiki/arduinokermit) because in this terminal program is integrated a file upload possibility (flash/ram/eeprom).