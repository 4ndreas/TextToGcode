# TextToGcode

[![PyPI version](https://badge.fury.io/py/TextToGcode.svg)](https://badge.fury.io/py/TextToGcode) 
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Downloads](https://static.pepy.tech/personalized-badge/texttogcode?period=total&units=international_system&left_color=grey&right_color=brightgreen&left_text=Total%20Downloads)](https://pepy.tech/project/texttogcode)
[![Downloads](https://static.pepy.tech/personalized-badge/texttogcode?period=month&units=international_system&left_color=grey&right_color=brightgreen&left_text=Monthly%20Downloads)](https://pepy.tech/project/texttogcode)

 A python library you can utilize to create custom gcode commands from a string. Intended to be used to engrave or draw text with cnc machines.

![numbers](https://i.imgur.com/Gk8xTg3.png)

## Installation

install with `pip install TextToGcode` or download the file from the github if you want to use via the command line

***

## Command Line Usage

navigate to the location of TextToGcode.py and run it with

`python3 TextToGcode.py "TEXT" SIZE ROTATION MODE FEEDRATE "ON COMMAND" "OFF COMMAND" "FAST COMMAND" "SLOW COMMAND"`

the important part is that all multi word arguments are surrounded with quotation marks as seen above

***

## Library Usage

import into your project with `from ttgLib.TextToGcode import ttg`

Then you can call the ToGcode function with your arguments to output or return your gcode as a file or list:

`ttg("TEXT", SIZE, ROTATION, "MODE", FEEDRATE).toGcode("ON COMMAND", "OFF COMMAND", "FAST COMMAND", "SLOW COMMAND")`

***

## Explanation of arguments

**Text**: a string for the text you want to be transformed to gcode, accepted characters are a-z, 0-9.
***(If you put a non alphanumeric character it will be skipped!)***

**Size**: integer that represents the scale of the text in mm ***(I advise to start with 1 and increase from there)***

**Rotation**: integer in degrees of the rotation of the text

**Mode**: a string specifying the mode of return.

- **"Return"**: returns a string of gcode commands
- **"File"**: generates an `output.gcode` file in the same directory
- **"visualize"**: returns a raw list of tuples (if you want to plot them using matplotlib to visualize your path)

**Feedrate**: integer used to specify the feed rate for the gcode operations

**On Off Fast Slow Commands**: string commands for certain gcode operations. ex:

- **ON**: "M03 S500"
- **OFF**: "M05 S0"
- **FAST**: "G0"
- **SLOW**: "G1"

***

## Example code:
Below is an example snippet for returning a list of gcode strings:

```python
from ttgLib.TextToGcode import ttg
gcode = ttg("Text to Gcode",1,0,"return",1).toGcode("M02 S500","M05 S0","G0","G1")
print(gcode)
```

Output:

```python
['G1 F1', 'G21', 'G90', ' X2 Y0', 'M02 S500', 'G1 X2 Y9', 'M05 S0', 'G1 X0 Y9', 'M02 S500', 'G1 X4 Y9', 'M05 S0', 'G1 X7 Y0', 'M02 S500', 'G1 X7 Y9', 'G1 X12 Y9', 'M05 S0', 'G1 X12 Y5', 'M02 S500', 'G1 X7 Y5', 'M05 S0', 'G1 X12 Y0', 'M02 S500', 'G1 X7 Y0', 'G1 X7 Y9', 'M05 S0', 'G1 X15 Y0', 'M02 S500', 'G1 X19 Y9', 'M05 S0', 'G1 X15 Y9', 'M02 S500', 'G1 X19 Y0', 'M05 S0', 'G1 X24 Y0', 'M02 S500', 'G1 X24 Y9', 'M05 S0', 'G1 X22 Y9', 'M02 S500', 'G1 X26 Y9', 'M05 S0', 'G1 X43 Y0', 'M02 S500', 'G1 X43 Y9', 'M05 S0', 'G1 X41 Y9', 'M02 S500', 'G1 X45 Y9', 'M05 S0', 'G1 X48 Y1', 'M02 S500', 'G1 X48 Y8', 'G1 X49 Y9', 'G1 X52 Y9', 'G1 X53 Y8', 'G1 X53 Y1', 'G1 X52 Y0', 'G1 X49 Y0', 'G1 X48 Y1', 'M05 S0', 'M05 S0', 'G1 X73 Y8', 'M02 S500', 'G1 X72 Y9', 'G1 X69 Y9', 'G1 X68 Y8', 'G1 X68 Y1', 'G1 X69 Y0', 'G1 X72 Y0', 'G1 X73 Y1', 'G1 X73 Y4', 'G1 X72 Y4', 'M05 S0', 'G1 X76 Y0', 'M05 S0', 'G1 X81 Y1', 'M02 S500', 'G1 X80 Y0', 'G1 X77 Y0', 'G1 X76 Y1', 'G1 X76 Y8', 'G1 X77 Y9', 'G1 X80 Y9', 'G1 X81 Y8', 'M05 S0', 'G1 X84 Y1', 'M02 S500', 'G1 X84 Y8', 'G1 X85 Y9', 'G1 X88 Y9', 'G1 X89 Y8', 'G1 X89 Y1', 'G1 X88 Y0', 'G1 X85 Y0', 'G1 X84 Y1', 'M05 S0', 'G1 X92 Y0', 'M02 S500', 'G1 X92 Y9', 'G1 X95 Y9', 'G1 X96 Y8', 'G1 X97 Y7', 'G1 X97 Y2', 'G1 X96 Y1', 'G1 X95 Y0', 'G1 X92 Y0', 'G1 X92 Y9', 'M05 S0', 'G1 X100 Y0', 'M02 S500', 'G1 X100 Y9', 'G1 X105 Y9', 'M05 S0', 'G1 X105 Y5', 'M02 S500', 'G1 X100 Y5', 'M05 S0', 'G1 X105 Y0', 'M02 S500', 'G1 X100 Y0', 'G1 X100 Y9', 'M05 S0']
```
