Serial port transfer tool between PCs and ICE Felix HCs
Runs on Windows command line.

ICE Felix HC computers are Romanian Sinclar Spectrum computer clones.
Reliable transfer with built in BASIC commands can be achieved at 4800 BAUD, not higher.
Using machine code routines on HC can speed up the transfer up to 19600 BAUD.

1. Creating a passive adapter to match the HC serial port pins to standard ones. Pinout pictures are included. 2 DB9 male connectors are required.
HC		PC
1-CTS---7-RTS
2-RTS---8-CTS
3-Rx----3-Tx
4-Tx----2-Rx
6-GND---5-GND


2. Setting up a transfer:
A. PC to HC
- On HC, type these commands: 
	FORMAT "b";4800: LOAD *"b"SCREEN$
- On PC, 
	- prepare a SCREEN$ file (lenght 6912), named 1.scr for example, 
	- notice in device manager what's the name of the COM port, COM1 for example
	- and type command in the command prompt: COM2HC.exe 1.scr
- You'll notice the screen file is loading with around 3200 BAUD.

B. HC to PC
- On HC, type these commands:
	FORMAT "b";4800: SAVE *"b"SCREEN$
- On PC, type this command:
	COM2HC 1.scr -c COM1 -d HC2PC
- You will notice that the the file 1.scr is created and has lenght 6912.

3. Command line arguments are:
- file name, mandatory
-c: COM port name, default COM1
-d: direction, HC2PC or PC2HC, default PC2HC
-a: block address for HC, default 0
-l: block lenght, default is file lenght
-t: block type, 0=Program, 3=Bytes, default 3
-b: baud rate, default 4800
-nh: no header, default is yes, to send the 9 byte header expected by LOAD *"b" commands. Not needed for machine code routines running on HC.
	
