Arduino Basic
=============
A complete BASIC interpreter for the Arduino, using a PS/2 keyboard, and SPI OLED screen. The BASIC supports almost all the usual features, with float and string variables, multi-dimensional arrays, FOR-NEXT, GOSUB-RETURN, etc. Saving and Loading from EEPROM is supported, as well as auto-running a program on power-up. You can also read and write from the analog and digital pins.

[![Demo](http://img.youtube.com/vi/JB5RXoO1IwQ/0.jpg)](http://www.youtube.com/watch?v=JB5RXoO1IwQ)

Prerequisites
-------------
1: An Arduino with at least 2k of RAM. i.e. UNO/Duemilanove/etc. It should also work on the MEGA but is untested. I think the sketch is too big for the Leonardo, since it looks like the bootloader uses more RAM on this model.

2: A PS/2 Keyboard. See http://playground.arduino.cc/Main/PS2Keyboard for wiring details.

3: An SSD1306 based OLED Screen connected using SPI. See e.g. http://www.adafruit.com/product/938. I think it should also work fine with the 128x32 version - you'll just need to change a couple of defines.

4: (Optional) A Piezoelectric buzzer for keyboard clicks and other sounds.

Getting Started
---------------
1: Download the zip file, unpack and copy the *folder* to your arduino sketches directory.

2: Install the PS/2 keyboard library if required. I've included the version I used in the zip file.

3: Install the SSD1306ASCII library. The normal Adafruit library is too RAM hungry for this project, so I'm using a massively cut down driver instead. I've modified this library a bit to get fast SPI transfers which improved the screen updating speed by a factor of about 4. The modified version is included in the zip file.

For both libraries, unzip the files and copy the *folder* to your arduino libraries directory.

4: Check your wiring corresponds to the pins in the comments/defines at the top of the Arduino_BASIC file.

BASIC Language
--------------
```
Arithmetic operators: + - * / MOD
Comparisons: <> (not equals) > >= < <=
Logical: AND, OR, NOT

Expressions can be numerical e.g. 5*(3+2), or string "Hello "+"world".
Only the addition operator is supported on strings (plus the functions below).

Commands
PRINT <expr>;<expr>... e.g. PRINT "A=";a
LET variable = <expr> e.g. LET A$="Hello".
variable = <expr> e.g. A=5
LIST [start],[end] e.g. LIST or LIST 10,100
RUN [lineNumber]
GOTO lineNumber
REM <comment> e.g. REM ** My Program ***
STOP
CONT (continue from a STOP)
INPUT variable e.g. INPUT a$ or INPUT a(5,3)
IF <expr> THEN cmd e.g. IF a>10 THEN a = 0: GOTO 20
FOR variable = start TO end STEP step
NEXT variable
NEW
GOSUB lineNumber
RETURN
DIM variable(n1,n2...)
CLS
PAUSE milliseconds
POSITION x,y sets the cursor
PIN pinNum, value (0 = low, non-zero = high)
PINMODE pinNum, mode ( 0 = input, 1 = output)
LOAD (from EEPROM)
SAVE (to EEPROM) e.g. use SAVE + to set auto-run on boot flag

"Pseudo-indentifiers"
INKEY$ - returns (and eats) the last key pressed buffer (non-blocking). e.g. PRINT INKEY$
RND - random number betweeen 0 and 1. e.g. LET a = RND

Functions
LEN(string)
VAL(string) e.g. PRINT VAL("1+2")
INT(number)
STR$(number)
LEFT$(string,n)
RIGHT$(string,n)
MID$(string,start,n)
PINREAD(pin)
ANALOGRD(pin)


```
