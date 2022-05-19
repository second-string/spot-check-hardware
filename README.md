# spot-check-hardware
Board design and assembly files for the Spot Check project

* Firmware repo: https://github.com/dot4qu/spot-check-firmware
* Backend API repo: https://github.com/dot4qu/spot-check-api
* Configuration iOS app repo: https://github.com/dot4qu/spot-check-ios

## Rev 1
The OG. This was an ESP chip that ran the main application logic that then communicated serially over UART to an ATMega328p to display the text on the LED strips (as the LED text libraries are only developed for Arduino). Zero support for this, I don't think I ever got the serial communication working super well since I had no protocol and the ESP would spew nonsense signals on boot. Oh to be young and naive again (just kidding I still am).

## Rev 2
The main, working revision for properly displaying text on an LED strip ticker with only an ESP32 driving everything. Powered from a 5V 1.5A+ barrel jack.

## Rev 3
Huge rework and addition from rev 2. Adds:
* USB to UART IC for power and programming instead of UART header (still on board for backup use if needed)
* Battery charger IC for supporting battery powered operation instead of wall outlet power
* Integrated e-ink driver circuit using shift register, boost converter to produce +22/-20V, additional regulators to filter to +/-15V, and a small-pitch FPC connector to connect to e-ink display
* Switch to ESP32-WROVER for additional on-module SRAM needed to run `epdiy` open source e-ink firmware

## Rev 3.1
**Use this version!!**
Fixes the issues in rev 3, mainly:
* Adds the missing capacitor between BTST and SW output of BQ24196 battery charger
* Switches the ESP footprint to the correct ESP32-WROVER footprint (all I/O on sides and longer length, no I/O on bottom like WROOM)
* Add 1uF cap acros ESP32 EN pin to slow its rise time enough to allow DTR/RTS auto-programming circuit to work
* Removed all the now-unneccesary zero ohm resistors
