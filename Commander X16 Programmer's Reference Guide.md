# Commander X16 Programmer's Reference Guide

*Michael Steil, mist64@mac.com*

*This is the PRELIMINARY Programmer's Reference Guide for the Commander X16 computer. Every and any information in this document can change, as the product is still in development!*

<hr>

**IMPORTANT** **IMPORTANT** **IMPORTANT** **IMPORTANT** **IMPORTANT**
This describes the "Proto2" board revision and the emulator/ROM versions r39 and later. For the original "Proto1" board revision and emulator/ROM versions r38 and lower, check out older versions of this document that don't have this notice.
**IMPORTANT** **IMPORTANT** **IMPORTANT** **IMPORTANT** **IMPORTANT**

<hr>

**Table of contents**

<!-- generated with https://github.com/ekalinin/github-markdown-toc -->

* [Commander X16 Programmer's Reference Guide](#commander-x16-programmers-reference-guide)
   * [Overview](#overview)
   * [BASIC Programming](#basic-programming)
      * [Commodore 64 Compatibility](#commodore-64-compatibility)
      * [ISO Mode](#iso-mode)
      * [Background Color](#background-color)
      * [New Control Characters](#new-control-characters)
      * [Keyboard Layouts](#keyboard-layouts)
      * [New Statements and Functions](#new-statements-and-functions)
         * [BIN$](#bin)
         * [CHAR](#char)
         * [CLS](#cls)
         * [COLOR](#color)
         * [DOS](#dos)
         * [FRAME](#frame)
         * [GEOS](#geos)
         * [HEX$](#hex)
         * [JOY](#joy)
         * [LINE](#line)
         * [LOCATE](#locate)
         * [MON](#mon)
         * [MOUSE](#mouse)
         * [MX/MY/MB](#mxmymb)
         * [OLD](#old)
         * [PSET](#pset)
         * [RECT](#rect)
         * [RESET](#reset)
         * [SCREEN](#screen)
         * [VPEEK](#vpeek)
         * [VPOKE](#vpoke)
         * [VLOAD](#vload)
      * [Other New Features](#other-new-features)
         * [Hexadecimal and Binary Literals](#hexadecimal-and-binary-literals)
         * [Different Text Modes](#different-text-modes)
         * [LOAD into VRAM](#load-into-vram)
         * [Default Device Numbers](#default-device-numbers)
      * [Internal Representation](#internal-representation)
   * [KERNAL](#kernal)
      * [KERNAL Version](#kernal-version)
      * [Compatibility Considerations](#compatibility-considerations)
      * [Commodore 64 API Compatibility](#commodore-64-api-compatibility)
      * [Commodore 128 API Compatibility](#commodore-128-api-compatibility)
      * [New API for the Commander X16](#new-api-for-the-commander-x16)
         * [Commodore Peripheral Bus](#commodore-peripheral-bus)
            * [Function Name: MACPTR](#function-name-macptr)
         * [Clock](#clock)
            * [Function Name: clock_set_date_time](#function-name-clock_set_date_time)
            * [Function Name: clock_get_date_time](#function-name-clock_get_date_time)
         * [Keyboard](#keyboard)
            * [Function Name: kbdbuf_peek](#function-name-kbdbuf_peek)
            * [Function Name: kbdbuf_get_modifiers](#function-name-kbdbuf_get_modifiers)
            * [Function Name: kbdbuf_put](#function-name-kbdbuf_put)
         * [Mouse](#mouse-1)
            * [Function Name: mouse_config](#function-name-mouse_config)
            * [Function Name: mouse_scan](#function-name-mouse_scan)
            * [Function Name: mouse_get](#function-name-mouse_get)
         * [Joystick](#joystick)
            * [Function Name: joystick_scan](#function-name-joystick_scan)
            * [Function Name: joystick_get](#function-name-joystick_get)
         * [I2C](#i2c)
            * [Function Name: i2c_read_byte](#function-name-i2c_read_byte)
            * [Function Name: i2c_write_byte](#function-name-i2c_write_byte)
         * [Sprites](#sprites)
            * [Function Name: sprite_set_image](#function-name-sprite_set_image)
            * [Function Name: sprite_set_position](#function-name-sprite_set_position)
         * [Framebuffer](#framebuffer)
            * [Function Name: FB_init](#function-name-fb_init)
            * [Function Name: FB_get_info](#function-name-fb_get_info)
            * [Function Name: FB_set_palette](#function-name-fb_set_palette)
            * [Function Name: FB_cursor_position](#function-name-fb_cursor_position)
            * [Function Name: FB_cursor_next_line](#function-name-fb_cursor_next_line)
            * [Function Name: FB_get_pixel](#function-name-fb_get_pixel)
            * [Function Name: FB_get_pixels](#function-name-fb_get_pixels)
            * [Function Name: FB_set_pixel](#function-name-fb_set_pixel)
            * [Function Name: FB_set_pixels](#function-name-fb_set_pixels)
            * [Function Name: FB_set_8_pixels](#function-name-fb_set_8_pixels)
            * [Function Name: FB_set_8_pixels_opaque](#function-name-fb_set_8_pixels_opaque)
            * [Function Name: FB_fill_pixels](#function-name-fb_fill_pixels)
            * [Function Name: FB_filter_pixels](#function-name-fb_filter_pixels)
            * [Function Name: FB_move_pixels](#function-name-fb_move_pixels)
         * [Graphics](#graphics)
            * [Function Name: GRAPH_init](#function-name-graph_init)
            * [Function Name: GRAPH_clear](#function-name-graph_clear)
            * [Function Name: GRAPH_set_window](#function-name-graph_set_window)
            * [Function Name: GRAPH_set_colors](#function-name-graph_set_colors)
            * [Function Name: GRAPH_draw_line](#function-name-graph_draw_line)
            * [Function Name: GRAPH_draw_rect](#function-name-graph_draw_rect)
            * [Function Name: GRAPH_move_rect](#function-name-graph_move_rect)
            * [Function Name: GRAPH_draw_oval](#function-name-graph_draw_oval)
            * [Function Name: GRAPH_draw_image](#function-name-graph_draw_image)
            * [Function Name: GRAPH_set_font](#function-name-graph_set_font)
            * [Function Name: GRAPH_get_char_size](#function-name-graph_get_char_size)
            * [Function Name: GRAPH_put_char](#function-name-graph_put_char)
         * [Console](#console)
            * [Function Name: console_init](#function-name-console_init)
            * [Function Name: console_put_char](#function-name-console_put_char)
            * [Function Name: console_put_image](#function-name-console_put_image)
            * [Function Name: console_get_char](#function-name-console_get_char)
            * [Function Name: console_set_paging_message](#function-name-console_set_paging_message)
         * [Other](#other)
            * [Function Name: memory_fill](#function-name-memory_fill)
            * [Function Name: memory_copy](#function-name-memory_copy)
            * [Function Name: memory_crc](#function-name-memory_crc)
            * [Function Name: memory_decompress](#function-name-memory_decompress)
            * [Function Name: entropy_get](#function-name-entropy_get)
            * [Function Name: monitor](#function-name-monitor)
            * [Function Name: enter_basic](#function-name-enter_basic)
            * [Function Name: screen_mode](#function-name-screen_mode)
            * [Function Name: screen_set_charset](#function-name-screen_set_charset)
            * [Function Name: JSRFAR](#function-name-jsrfar)
   * [Math Library](#math-library)
      * [Format Conversions](#format-conversions)
      * [Math Functions](#math-functions)
      * [Movement](#movement)
      * [X16 Additions](#x16-additions)
      * [Notes](#notes)
   * [Machine Language Monitor](#machine-language-monitor)
   * [Memory Map](#memory-map)
      * [Banked Memory](#banked-memory)
      * [ROM Allocations](#rom-allocations)
      * [RAM Contents](#ram-contents)
         * [Zero Page](#zero-page)
         * [Banking](#banking)
      * [I/O Area](#io-area)
   * [Video Programming](#video-programming)
   * [Sound Programming](#sound-programming)
   * [I/O Programming](#io-programming)
      * [Custom keyboard scan code handler](#custom-keyboard-scan-code-handler)
      * [I2C Bus](#i2c-bus)
         * [System Management Controller](#system-management-controller)
         * [Real-Time-Clock](#real-time-clock)


## Overview

The Commander X16 is a modern home computer in the philosophy of Commodore computers like the VIC-20 and the C64.

**Features:**

* 8-bit 65C02 CPU at 8 MHz
* 512 KB or 2 MB RAM
* 512 KB ROM
* VERA video controller
	* up to 640x480 resolution
	* 256 colors from a palette of 4096
	* 128 sprites
	* VGA, NTSC and RGB output
* *[sound controller TBD]*
* Connectivity:
	* PS/2 keyboard and mouse
	* 4 NES/SNES controllers
	* SD card
	* Commodore Serial Bus ("IEC")
	* several free GPIOs ("user port")

As a modern sibling of the line of Commodore home computers, the Commander X16 is reasonably compatible with computers of that line.

* Pure BASIC programs are fully backwards compatible with the VIC-20 and the C64.
* POKEs for video and audio are not compatible with any Commodore computer. (There are no VIC or SID controllers, for example.)
* Pure machine language programs ($FF81+ KERNAL API) are compatible with Commodore computers.

## BASIC Programming

### Commodore 64 Compatibility

The Commander X16 BASIC interpreter is 100% backwards-compatible with the Commodore 64 one. This includes the following features:

* All statements and functions
* Strings, arrays, integers, floats
* Max. 80 character BASIC lines
* Printing "quote mode" control characters like cursor control and color codes, e.g.:
	* `CHR$(147)`: clear screen
	* `CHR$(5)`: white text
	* `CHR$(18)`: reverse
	* `CHR$(14)`: switch to upper/lowercase font
	* `CHR$(142)`: switch to uppercase/graphics font

Because of the differences in hardware, the following functions and statements are incompatible between C64 and X16 BASIC programs.

* `POKE`: write to a memory address
* `PEEK`: read from a memory address
* `WAIT`: wait for memory contents
* `SYS`: execute machine language code

The BASIC interpreter also currently shares all problems of the C64 version, like the slow garbage collector.

### ISO Mode

In addition to PETSCII, the X16 also supports the ISO-8859-15 character encoding. In ISO-8859-15 mode ("ISO mode"):

* The character set is switched from Commodore-style (with PETSCII drawing characters) to a new ASCII/ISO-8859-15 compatible set, which covers most Western European writing systems.
* The encoding (`CHR$()` in BASIC and `BSOUT` in machine language) now complies with ASCII and ISO-8859-15.
* The keyboard driver will return ASCII/ISO-8859-15 codes.

This is the encoding:

	   0123456789ABCDEF
	0x|                |
	1x|                |
	2x| !"#$%&'()*+,-./|
	3x|0123456789:;<=>?|
	4x|@ABCDEFGHIJKLMNO|
	5x|PQRSTUVWXYZ[\]^_|
	6x|`abcdefghijklmno|
	7x|pqrstuvwxyz{|}~ |
	8x|                |
	9x|                |
	Ax| ¡¢£€¥Š§š©ª«¬ ®¯|
	Bx|°±²³Žµ¶·ž¹º»ŒœŸ¿|
	Cx|ÀÁÂÃÄÅÆÇÈÉÊËÌÍÎÏ|
	Dx|ÐÑÒÓÔÕÖ×ØÙÚÛÜÝÞß|
	Ex|àáâãäåæçèéêëìíîï|
	Fx|ðñòóôõö÷øùúûüýþÿ|

ISO mode can be enabled and disabled using two new control codes:

* `CHR$($0F)`: enable ISO mode
* `CHR$($8F)`: disable ISO mode (default)

You can also enable ISO mode in direct mode by pressing Ctrl+`O`.

**Important:** In ISO mode, BASIC keywords need to be written in upper case, that is, they have to be entered with the Shift key down, and abbreviating keywords is no longer possible.

### Background Color

In regular BASIC text mode, the video controller supports 16 foreground colors and 16 background colors for each character on the screen.

The new "swap fg/bg color" code is useful to change the background color of the cursor, like this:

	PRINT CHR$(1);   : REM SWAP FG/BG
	PRINT CHR$($1C); : REM SET FG COLOR TO RED
	PRINT CHR$(1);   : REM SWAP FG/BG

The new BASIC instruction `COLOR` makes this easier, but the trick above can also be used from machine code programs.

To set the background color of the complete screen, it just has to be cleared after setting the color:

      PRINT CHR$(147);

### New Control Characters

This is the set of all supported PETSCII control characters. Descriptions in bold indicate new codes compared to the C64:

| Code |                            |                           | Code |
|------|----------------------------|---------------------------|------|
| $00  | NULL                       | -                         | $80  |
| $01  | **SWAP COLORS**            | COLOR: ORANGE             | $81  |
| $02  <td colspan=2 align="center"> -                          | $82  |
| $03  <td colspan=2 align="center"> STOP/RUN                   | $83  |
| $04  | **ATTRIBUTES: UNDERLINE**  | **HELP**                  | $84  |
| $05  | COLOR: WHITE               | F1                        | $85  |
| $06  | **ATTRIBUTES: BOLD**       | F3                        | $86  |
| $07  | **BELL**                   | F5                        | $87  |
| $08  | **BACKSPACE**              | F7                        | $88  |
| $09  | **TAB**                    | F2                        | $89  |
| $0A  | **LF**                     | F4                        | $8A  |
| $0B  | **ATTRIBUTES: ITALICS**    | F6                        | $8B  |
| $0C  | **ATTRIBUTES: OUTLINE**    | F8                        | $8C  |
| $0D  <td colspan=2 align="center"> REGULAR/SHIFTED RETURN     | $8D  |
| $0E  <td colspan=2 align="center"> CHARSET: LOWER/UPPER CASE  | $8E  |
| $0F  <td colspan=2 align="center"> **CHARSET: ISO ON/OFF**    | $8F  |
| $10  | **F9**                     | COLOR: BLACK              | $90  |
| $11  <td colspan=2 align="center"> CURSOR: DOWN/UP            | $91  |
| $12  | ATTRIBUTES: REVERSE        | ATTRIBUTES: CLEAR ALL     | $92  |
| $13  <td colspan=2 align="center"> HOME/CLEAR                 | $93  |
| $14  <td colspan=2 align="center"> DEL/INSERT                 | $94  |
| $15  | **F10**                    | COLOR: BROWN              | $95  |
| $16  | **F11**                    | COLOR: LIGHT RED          | $96  |
| $17  | **F12**                    | COLOR: DARK GRAY          | $97  |
| $18  | **SHIFT+TAB**              | COLOR: MIDDLE GRAY        | $98  |
| $19  | -                          | COLOR: LIGHT GREEN        | $99  |
| $1A  | -                          | COLOR: LIGHT BLUE         | $9A  |
| $1B  | -                          | COLOR: LIGHT GRAY         | $9B  |
| $1C  | COLOR: RED                 | COLOR: PURPLE             | $9C  |
| $1D  | CURSOR: RIGHT              | CURSOR: LEFT              | $9D  |
| $1E  | COLOR: GREEN               | COLOR: YELLOW             | $9E  |
| $1F  | COLOR: BLUE                | COLOR: CYAN               | $9F  |

**Notes:**

* $01: SWAP COLORS swaps the foreground and background colors in text mode
* $04/$06/$0B/$0C: the new attribute change codes only have an effect in graphics mode
* $07/$08/$09/$0A/$18: have been added for ASCII compatibility *[NYI]*
* $08/$09: Charset switch enable/disable not supported
* F9-F12, HELP: these codes match the C65 additions

### Keyboard Layouts

Pressing the `F9` key cycles through the available keyboard layouts.

### New Statements and Functions

There are several new statement and functions. Note that all BASIC keywords (such as `FOR`) get converted into tokens (such as `$81`), and the tokens for the new keywords have not been finalized yet. Therefore, loading BASIC program saved from a different revision of BASIC may mix up keywords.


#### BIN$

**TYPE: String Function**
**FORMAT: BIN$(n)**

**Action:** Return a string representing the binary value of n. If n <= 255, 8 characters are returned and if 255 < n <= 65535, 16 characters are returned.

**EXAMPLE of BIN$ Function:**

	PRINT BIN$(200)   : REM PRINTS 11001000 AS BINARY REPRESENTATION OF 200
	PRINT BIN$(45231) : REM PRINTS 1011000010101111 TO REPRESENT 16 BITS

#### CHAR

**TYPE: Command**
**FORMAT: CHAR &lt;x&gt;,&lt;y&gt;,&lt;color&gt;,&lt;string&gt;**

**Action:** This command draws a text string on the graphics screen in a given color.

The string can contain printable ASCII characters (`CHR$($20)` to `CHR$($7E)`), as well most PETSCII control codes.

**EXAMPLE of CHAR Statement:**

	10 SCREEN$80
	20 A$="The quick brown fox jumps over the lazy dog."
	24 CHAR0,6,0,A$
	30 CHAR0,6+12,0,CHR$($04)+A$   :REM UNDERLINE
	40 CHAR0,6+12*2,0,CHR$($06)+A$ :REM BOLD
	50 CHAR0,6+12*3,0,CHR$($0B)+A$ :REM ITALICS
	60 CHAR0,6+12*4,0,CHR$($0C)+A$ :REM OUTLINE
	70 CHAR0,6+12*5,0,CHR$($12)+A$ :REM REVERSE

#### CLS

**TYPE: Command**
**FORMAT: CLS**

**Action:** Clears the screen. Same effect as `?CHR$(147);`.

**EXAMPLE of CLS Statement:**

	CLS

#### COLOR

**TYPE: Command**
**FORMAT: COLOR &lt;fgcol&gt;[,&lt;bgcol&gt;]**

**Action:** This command works sets the text mode foreground color, and optionally the background color.

**EXAMPLES of COLOR Statement:**

      COLOR 2   : SET FG COLOR TO RED, KEEP BG COLOR
      COLOR 2,0 : SET FG COLOR TO RED, BG COLOR TO BLACK

#### DOS

**TYPE: Command**
**FORMAT: DOS &lt;string&gt;**

**Action:** This command works with the command/status channel or the directory of a Commodore DOS device and has different functionality depending on the type of argument.

* Without an argument, `DOS` prints the status string of the current device.
* With a string argument of `"8"` or `"9"`, it switches the current device to the given number.
* With an argument starting with `"$"`, it shows the directory of the device.
* Any other argument will be sent as a DOS command.

**EXAMPLES of DOS Statement:**

      DOS"$"          : REM SHOWS DIRECTORY
      DOS"S:BAD_FILE" : REM DELETES "BAD_FILE"
      DOS             : REM PRINTS DOS STATUS, E.G. "01,FILES SCRATCHED,01,00"

#### FRAME

**TYPE: Command**
**FORMAT: FRAME &lt;x1&gt;,&lt;y1&gt;,&lt;x2&gt;,&lt;y2&gt;,&lt;color&gt;**

**Action:** This command draws a rectangle frame on the graphics screen in a given color.

**EXAMPLE of FRAME Statement:**

	10 SCREEN$80
	20 FORI=1TO20:FRAMERND(1)*320,RND(1)*200,RND(1)*320,RND(1)*200,RND(1)*128:NEXT
	30 GOTO20

#### GEOS

**TYPE: Command**
**FORMAT: GEOS**

**Action:** Enter the GEOS UI.

#### HEX$

**TYPE: String Function**
**FORMAT: HEX$(n)**

**Action:** Return a string representing the hexadecimal value of n. If n <= 255, 2 characters are returned and if 255 < n <= 65535, 4 characters are returned.

**EXAMPLE of HEX$ Function:**

	PRINT HEX$(200)   : REM PRINTS C8 AS HEXADECIMAL REPRESENTATION OF 200
	PRINT HEX$(45231) : REM PRINTS B0AF TO REPRESENT 16 BIT VALUE

#### JOY

**TYPE: Integer Function**
**FORMAT: JOY(n)**

**Action:** Return the state of a joystick.

`JOY(1)` through `JOY(4)` return the state of SNES controllers connected to the system, and `JOY(0)` returns the state of the "keyboard joystick", a set of keyboard keys that map to the SNES controller layout. See [`joystick_get`](#function-name-joystick_get) for details.

If no controller is connected to the SNES port (or no keyboard is connected), the function returns -1. Otherwise, the result is a bit field, with pressed buttons `OR`ed together:

| Value  | Button |
|--------|--------|
| $800   | A      |
| $400   | X      |
| $200   | L      |
| $100   | R      |
| $080   | B      |
| $040   | Y      |
| $020   | SELECT |
| $010   | START  |
| $008   | UP     |
| $004   | DOWN   |
| $002   | LEFT   |
| $001   | RIGHT  |

Note that this bitfield is different from the `joystick_get` KERNEL API one. Also note that the keyboard joystick will allow LEFT and RIGHT as well as UP and DOWN to be pressed at the same time, while controllers usually prevent this mechanically.

**EXAMPLE of JOY Function:**

	10 REM DETECT CONTROLLER, FALL BACK TO KEYBOARD
	20 J = 0: FOR I=1 TO 4: IF JOY(I) >= 0 THEN J = I: GOTO40
	30 NEXT
	40 :
	50 V=JOY(J)
	60 PRINT CHR$(147);V;": ";
	70 IF V = -1 THEN PRINT"DISCONNECTED ": GOTO50
	80 IF V AND 8 THEN PRINT"UP ";
	90 IF V AND 4 THEN PRINT"DOWN ";
	100 IF V AND 2 THEN PRINT"LEFT ";
	110 IF V AND 1 THEN PRINT"RIGHT ";
	120 GOTO50

#### LINE

**TYPE: Command**
**FORMAT: LINE &lt;x1&gt;,&lt;y1&gt;,&lt;x2&gt;,&lt;y2&gt;,&lt;color&gt;**

**Action:** This command draws a line on the graphics screen in a given color.

**EXAMPLE of LINE Statement:**

	10 SCREEN128
	20 FORA=0TO2*\XFFSTEP2*\XFF/200
	30 :  LINE100,100,100+SIN(A)*100,100+COS(A)*100
	40 NEXT

#### LOCATE

**TYPE: Command**
**FORMAT: LOCATE &lt;line&gt;[,&lt;column&gt;]**

**Action:** This command positions the text mode cursor at the given location. The values are 1-based. If no column is given, only the line is changed.

**EXAMPLE of LOCATE Statement:**

	100 REM DRAW CIRCLE ON TEXT SCREEN
	110 SCREEN0
	120 R=25
	130 X0=40
	140 Y0=30
	150 FORT=0TO360STEP1
	160 :  X=X0+R*COS(T)
	170 :  Y=Y0+R*SIN(T)
	180 :  LOCATEY,X:PRINTCHR$($12);" ";
	190 NEXT

#### MON

**TYPE: Command**
**FORMAT: MON (Alternative: MONITOR)**

**Action:** This command enters the machine language monitor. See the dedicated chapter for a  description.

**EXAMPLE of MON Statement:**

      MON
      MONITOR

#### MOUSE

**TYPE: Command**
**FORMAT: MOUSE &lt;mode&gt;**

**Action:** This command configures the mouse pointer.

| Mode | Description                              |
|------|------------------------------------------|
| 0    | Hide mouse                               |
| 1    | Show mouse, set default mouse pointer    |
| $FF  | Show mouse, don't configure mouse cursor |

`MOUSE 1` turns on the mouse pointer and `MOUSE 0` turns it off. If the BASIC program has its own mouse pointer sprite configured, it can use `MOUSE $FF`, which will turn the mouse pointer on, but not set the default pointer sprite.

The size of the mouse pointer's area will be configured according to the current screen mode. If the screen mode is changed, the MOUSE statement has to be repeated.

**EXAMPLES of MOUSE Statement:**

	MOUSE 1 : REM ENABLE MOUSE
	MOUSE 0 : REM DISABLE MOUSE

#### MX/MY/MB

**TYPE: Integer Function**
**FORMAT: MX**
**FORMAT: MY**
**FORMAT: MB**

**Action:** Return the horizontal (`MX`) or vertical (`MY`) position of the mouse pointer, or the mouse button state (`MB`).

`MB` returns the sum of the following values depending on the state of the buttons:

| Value | Button |
|-------|--------|
| 0     | none   |
| 1     | left   |
| 2     | right  |
| 4     | third  |

**EXAMPLE of MX/MY/MB Functions:**

	REM SIMPLE DRAWING PROGRAM
	10 SCREEN$80
	20 MOUSE1
	25 OB=0
	30 TX=MX:TY=MY:TB=MB
	35 IFTB=0GOTO25
	40 IFOBTHENLINEOX,OY,TX,TY,16
	50 IFOB=0THENPSETTX,TY,16
	60 OX=TX:OY=TY:OB=TB
	70 GOTO30

#### OLD

**TYPE: Command**
**FORMAT: OLD**

**Action:** This command recovers the BASIC program in RAM that has been previously deleted using the `NEW` command or through a RESET.

**EXAMPLE of OLD Statement:**

      OLD

#### PSET

**TYPE: Command**
**FORMAT: PSET &lt;x&gt;,&lt;y&gt;,&lt;color&gt;**

**Action:** This command sets a pixel on the graphics screen to a given color.

**EXAMPLE of PSET Statement:**

	10 SCREEN$80
	20 FORI=1TO20:PSETRND(1)*320,RND(1)*200,RND(1)*256:NEXT
	30 GOTO20

#### RECT

**TYPE: Command**
**FORMAT: RECT &lt;x1&gt;,&lt;y1&gt;,&lt;x2&gt;,&lt;y2&gt;,&lt;color&gt;**

**Action:** This command draws a solid rectangle on the graphics screen in a given color.

**EXAMPLE of RECT Statement:**

	10 SCREEN$80
	20 FORI=1TO20:RECTRND(1)*320,RND(1)*200,RND(1)*320,RND(1)*200,RND(1)*256:NEXT
	30 GOTO20

#### RESET

**TYPE: Command**
**FORMAT: RESET**

**Action:** Performs a software reset of the system.

**EXAMPLE of RESET Statement:**

	RESET

#### SCREEN

**TYPE: Command**
**FORMAT: SCREEN &lt;mode&gt;**

**Action:** This command switches the screen mode. Modes $80 (128) and above are graphics modes.

| Mode | Description |
|------|-------------|
| $00  | 80x60 text  |
| $01  | 80x30 text  |
| $02  | 40x60 text  |
| $03  | 40x30 text  |
| $04  | 40x15 text  |
| $05  | 20x30 text  |
| $06  | 20x15 text  |
| $80  | 320x200@256c<br/>40x25 text |
| $81  | 640x400@16c* |

* [currently unimplemented]

The value of $FF (255) toggles between modes $00 and $03.

Note that in text/graphics mode ($80), text color 0 is now translucent instead of black.

#### VPEEK

**TYPE: Integer Function**
**FORMAT: VPEEK (&lt;bank&gt;, &lt;address&gt;)**

**Action:** Return a byte from the video address space. The video address space has 20 bit addresses, which is exposed as 16 banks of 65536 addresses each.

**EXAMPLE of VPEEK Function:**

      PRINT VPEEK(1,$B000) : REM SCREEN CODE OF CHARACTER AT 0/0 ON SCREEN

#### VPOKE

**TYPE: Command**
**FORMAT: VPOKE &lt;bank&gt;, &lt;address&gt;, &lt;value&gt;**

**Action:** Set a byte in the video address space. The video address space has 20 bit addresses, which is exposed as 16 banks of 65536 addresses each.

**EXAMPLE of VPOKE Statement:**

      VPOKE 1,$B000+1,1 * 16 + 2 : REM SETS THE COLORS OF THE CHARACTER
                                   REM AT 0/0 TO RED ON WHITE

#### VLOAD

**TYPE: Command**
	**FORMAT: VLOAD &lt;filename&gt;, &lt;device&gt;, &lt;VERA_high_address&gt;, &lt;VERA_low_address&gt;**
	
**Action:** Loads a file directly into VERA RAM. 

**EXAMPLES of VLOAD:**
	
	VLOAD "MYFILE.BIN", 8, 0, $4000  :REM LOADS MYFILE.BIN FROM DEVICE 8 TO VRAM $4000.
	VLOAD "MYFONT.BIN", 8, 1, $F000  :REM LOAD A FONT INTO THE DEFAULT FONT LOCATION ($1F000).

### Other New Features

#### Hexadecimal and Binary Literals

The numeric constants parser supports both hex (`$`) and binary (`%`) literals, like this:

      PRINT $EA31 + %1010

The size of hex and binary values is only restricted by the range that can be represented by BASIC's internal floating point representation.

#### Different Text Modes

In BASIC, both an 80x60 and a 40x30 character text mode is supported. To switch modes, use the BASIC statement `SCREEN`:

      SCREEN 3 : REM SWITCH TO 40 CHARACTER MODE
      SCREEN 0 : REM SWITCH TO 80 CHARACTER MODE
      SCREEN 255 : REM SWITCH BETWEEN 40 and 80 CHARACTER MODE

#### LOAD into VRAM

In BASIC, the contents of files can be directly loaded into VRAM with the `LOAD` statement. When a secondary address greater than one is used, the KERNAL will now load the file into the VERA's VRAM address space. The first two bytes of the file are used as lower 16 bits of the address. The upper 4 bits are `(SA-2) & 0x0ff` where `SA` is the secondary address.

Examples:

	  10 REM LOAD VERA SETTINGS
	  20 LOAD"VERA.BIN",1,17 : REM SET ADDRESS TO $FXXXX
	  30 REM LOAD TILES
	  40 LOAD"TILES.BIN",1,3 : REM SET ADDRESS TO $1XXXX
	  50 REM LOAD MAP
      60 LOAD"MAP.BIN",1,2 : REM SET ADDRESS TO $0XXXX

#### Default Device Numbers

In BASIC, the LOAD, SAVE and OPEN statements default to the last-used IEEE device (device numbers 8 and above), or 8.

### Internal Representation

Like on the C64, BASIC keywords are tokenized.

* The C64 BASIC V2 keywords occupy the range of $80 (`END`) to $CB (`GO`).
* BASIC V3.5 also used $CE (`RGR`) to $FD (`WHILE`).
* BASIC V7 introduced the $CE escape code for function tokens $CE-$02 (`POT`) to $CE-$0A (`POINTER`), and the $FE escape code for statement tokens $FE-$02 (`BANK`) to $FE-$38 (`SLOW`).
* The unreleased BASIC V10 extended the escaped tokens up to $CE-$0D (`RPALETTE`) and $FE-$45 (`EDIT`).

The X16 BASIC aims to be as compatible as possible with this encoding. Keywords added to X16 BASIC that also exist in other versions of BASIC match the token, and new keywords are encoded in the ranges $CE-$80+ and $FE-$80+.

## KERNAL

The Commander X16 contains a version of KERNAL as its operating system in ROM. It contains

* a 40/80 character screen driver
* a PS/2 keyboard driver
* a PS/2 mouse driver
* an NES/SNES controller driver
* a Commodore Serial Bus ("IEC") driver *[not yet working]*
* "Channel I/O" for abstracting devices
* simple memory management
* timekeeping

### KERNAL Version

The KERNAL version can be read from location $FF80 in ROM. A value of $FF indicates a custom build. All other values encode the build number. Positive numbers are release versions ($02 = release version 2), two's complement negative numbers are prerelease versions ($FE = $100 - 2 = prerelease version 2).

### Compatibility Considerations

For applications to remain compatible between different versions of the ROM, they can rely upon:

* the KERNAL API

The following features must not be relied upon:

* the zero page and $0200+ memory layout
* direct function offsets in the ROM

### Commodore 64 API Compatibility

The KERNAL fully supports the C64 KERNAL API.

**Channel I/O:**
$FF90: `SETMSG` – set verbosity
$FFB7: `READST` – return status byte
$FFBA: `SETLFS` – set LA, FA and SA
$FFBD: `SETNAM` – set filename
$FFC0: `OPEN` – open a channel
$FFC3: `CLOSE` – close a channel
$FFC6: `CHKIN` – set channel for character input
$FFC9: `CHKOUT` – set channel for character output
$FFCC: `CLRCHN` – restore character I/O to screen/keyboard
$FFCF: `BASIN` – get character
$FFD2: `BSOUT` – write character
$FFD5: `LOAD` – load a file into memory
$FFD8: `SAVE` – save a file from memory
$FFE7: `CLALL` – close all channels

**Commodore Peripheral Bus:**
$FFB4: `TALK` – send TALK command
$FFB1: `LISTEN` – send LISTEN command
$FFAE: `UNLSN` – send UNLISTEN command
$FFAB: `UNTLK` – send UNTALK command
$FFA8: `CIOUT` – send byte to peripheral bus
$FFA5: `ACPTR` – read byte from peripheral bus
$FFA2: `SETTMO` – set timeout
$FF96: `TKSA` – send TALK secondary address
$FF93: `SECOND` – send LISTEN secondary address

**Memory:**
$FF9C: `MEMBOT` – read/write address of start of usable RAM
$FF99: `MEMTOP` – read/write address of end of usable RAM

**Time:**
$FFDE: `RDTIM` – read system clock
$FFDB: `SETTIM` – write system clock
$FFEA: `UDTIM` – advance clock

**Other:**
$FFE1: `STOP` – test for STOP key
$FFE4: `GETIN` – get character from keyboard
$FFED: `SCREEN` – get the screen resolution
$FFF0: `PLOT` – read/write cursor position
$FFF3: `IOBASE` – return start of I/O area

Some notes:

* For device #8, the Commodore Peripheral Bus calls first talk to the "Computer DOS" built into the ROM to detect an SD card, before falling back to the Commodore Serial Bus.
* The `IOBASE` call returns $9F60, the location of the first VIA controller.
* The `SETTMO` call has been a no-op since the Commodore VIC-20, and has no function on the X16 either.
* The `MEMTOP` call additionally returns the number of available RAM banks in the .A register.
* The layout of the zero page ($0000-$00FF) and the KERNAL/BASIC variable space ($0200+) are generally **not** compatible with the C64.
* The vectors ($0300-$0333) are fully compatible with the C64.

### Commodore 128 API Compatibility

In addition, the X16 supports a subset of the C128 API additions:

$FF4A: `CLOSE_ALL` – close all files on a device
$FF8D: `LKUPLA` – search tables for given LA
$FF8A: `LKUPSA` – search tables for given SA
$FF62: `DLCHR` - activate a text mode font in the video hardware *[not yet implemented]*
$FF65: `PFKEY` – program a function key *[not yet implemented]*
$FF74: `FETCH` – LDA (fetvec),Y from any bank
$FF77: `STASH` – STA (stavec),Y to any bank
$FF7A: `CMPARE` – CMP (cmpvec),Y to any bank
$FF7D: `PRIMM` – print string following the caller’s code

Some notes:

* `FETCH`, `STASH` and `CMPARE` require the caller to set the zero page location containing the address in memory beforehand. These are different than on the C128:

|Call    |Label   |Address |
|--------|--------|--------|
|`FETCH` |`FETVEC`|$03AF   |
|`STASH` |`STAVEC`|$XXXX   |
|`CMPARE`|`CMPVEC`|$XXXX   |

*[Note: `STASH` and `CMPARE` are currently non-functional.]*

### New API for the Commander X16

There are lots of new APIs. Please note that their addresses and their behavior is still prelimiary and can change between revisions.

Some new APIs use the "16 bit" ABI, which uses virtual 16 bit registers r0 through r15, which are located in zero page locations $02 through $21: r0 = r0L = $02, r0H = $03, r1 = r1L = $04 etc.

The 16 bit ABI generally follows the following conventions:

* arguments
    * word-sized arguments: passed in r0-r5
    * byte-sized arguments: if three or less, passed in .A, .X, .Y; otherwise in 16 bit registers
    * boolean arguments: .C, .N
* return values
	* basic rules as above
    * function takes no arguments: r0-r5, else indirect through passed-in pointer
    * arguments in r0-r5 can be "inout", i.e. they can be updated
* saved/scratch registers
    * r0-r5: arguments (saved)
    * r6-r10: saved
    * r11-r15: scratch
    * .A, .X, .Y, .C, .N: scratch (unless used otherwise)

#### Commodore Peripheral Bus

$FF44: `MACPTR` - read multiple bytes from peripheral bus

##### Function Name: MACPTR

Purpose: Read multiple bytes from the peripheral bus
Call address: $FF44
Communication registers: .A, .X, .Y
Preparatory routines: `FILNAM`, `FILPAR`, `OPEN`, `CHKIN`
Error returns: None
Stack requirements: ...
Registers affected: .A, .X, .Y

**Description:** The routine `MACPTR` is the multi-byte variant of the `ACPTR` KERNAL routine. Instead of returning a single byte in .A, it can read multiple bytes in one call and write them directly to memory.

The number of bytes to be read is passed in the .A register; a value of 0 indicates that it is up to the KERNAL to decide how many bytes to read. A pointer to where the data is supposed to be written is passed in the .X (lo) and .Y (hi) registers.

Upon return, a set .C flag indicates that the device does not support `MACPTR`, and the program needs to read the data byte-by-byte using the `ACPTR` call instead.

If `MACPTR` is supported, .C is clear and .X (lo) and .Y (hi) contain the number of bytes read.

Like with `ACPTR`, the status of the operation can be retrieved using the `READST` KERNAL call.

#### Clock

$FF4D: `clock_set_date_time` - set date and time
$FF50: `clock_get_date_time` - get date and time

##### Function Name: clock_set_date_time

Purpose: Set the date and time
Call address: $FF4D
Communication registers: r0, r1, r2, r3L
Preparatory routines: None
Error returns: None
Stack requirements: 0
Registers affected: .A, .X, .Y

**Description:** The routine `clock_set_date_time` sets the system's real-time-clock.

| Register | Contents          |
|----------|-------------------|
| r0L      | year (1900-based) |
| r0H      | month (1-12)	   |
| r1L      | day (1-31)		   |
| r1H      | hours (0-23)	   |
| r2L      | minutes (0-59)	   |
| r2H      | seconds (0-59)	   |
| r3L      | jiffies (0-59)    |

Jiffies are 1/60th seconds.

##### Function Name: clock_get_date_time

Purpose: Get the date and time
Call address: $FF50
Communication registers: r0, r1, r2, r3L
Preparatory routines: None
Error returns: None
Stack requirements: 0
Registers affected: .A, .X, .Y

**Description:** The routine `clock_get_date_time` returns the state of the system's real-time-clock. The register assignment is identical to `clock_set_date_time`.

On the Commander X16, the *jiffies* field is unsupported and will always read back as 0.

#### Keyboard

$FEBD: `kbdbuf_peek` - get first char in keyboard queue and queue length
$FEC0: `kbdbuf_get_modifiers` - get currently pressed modifiers
$FEC3: `kbdbuf_put` - append a char to the keyboard queue

##### Function Name: kbdbuf_peek

Purpose: Get next char and keyboard queue length
Call address: $FEBD
Communication registers: .A, .X
Preparatory routines: None
Error returns: None
Stack requirements: 0
Registers affected: -

**Description:** The routine `kbdbuf_peek` returns the next character in the keyboard queue in .A, without removing it from the queue, and the current length of the queue in .X. If .X is 0, the Z flag will be set, and the value of .A is undefined.

##### Function Name: kbdbuf_get_modifiers

Purpose: Get currently pressed modifiers
Call address: $FEC0
Communication registers: .A
Preparatory routines: None
Error returns: None
Stack requirements: 0
Registers affected: -

**Description:** The routine `kbdbuf_get_modifiers` returns a bitmask that represents the currently pressed modifier keys in .A:

| Bit | Value | Description  | Comment        |
|-----|-------|--------------|----------------|
| 0   | 1     | Shift        |                |
| 1   | 2     | Alt          | C64: Commodore |
| 2   | 4     | Control      |                |
| 3   | 8     | Logo/Windows | C128: Alt      |
| 4   | 16    | Caps         |                |

##### Function Name: kbdbuf_put

Purpose: Append a char to the keyboard queue
Call address: $FEC3
Communication registers: .A
Preparatory routines: None
Error returns: None
Stack requirements: 0
Registers affected: .X

**Description:** The routine `kbdbuf_put` appends the char in .A to the keyboard queue.

#### Mouse

$FF68: `mouse_config` - configure mouse pointer
$FF71: `mouse_scan` - query mouse
$FF6B: `mouse_get` - get state of mouse

##### Function Name: mouse_config

Purpose: Configure the mouse pointer
Call address: $FF68
Communication registers: .A, .X, .Y
Preparatory routines: None
Error returns: None
Stack requirements: 0
Registers affected: .A, .X, .Y

**Description:** The routine `mouse_config` configures the mouse pointer.

The argument in .A specifies whether the mouse pointer should be visible or not, and what shape it should have. For a list of possible values, see the basic statement `MOUSE`.

The arguments in .X and .Y specify the screen resolution in 8 pixel increments. The values .X = 0 and .Y = 0 keep the current resolution.

**EXAMPLE:**

	SEC
	JSR screen_mode ; get current screen size (in 8px) into .X and .Y
	LDA #1
	JSR mouse_config ; show the default mouse pointer

##### Function Name: mouse_scan

Purpose: Query the mouse and save its state
Call address: $FF71
Communication registers: None
Preparatory routines: None
Error returns: None
Stack requirements: ?
Registers affected: .A, .X, .Y

**Description:** The routine `mouse_scan` retrieves all state from the mouse and saves it. It can then be retrieved using `mouse_get`. The default interrupt handler already takes care of this, so this routine should only be called if the interrupt handler has been completely replaced.

##### Function Name: mouse_get

Purpose: Get the mouse state
Call address: $FF6B
Communication registers: .X
Preparatory routines: `mouse_config`
Error returns: None
Stack requirements: 0
Registers affected: .A

**Description:** The routine `mouse_get` returns the state of the mouse. The caller passes the offset of a zero-page location in .X, which the routine will populate with the mouse position in 4 consecutive bytes:

| Offset | Size | Description |
|--------|------|-------------|
| 0      | 2    | X Position  |
| 2      | 2    | Y Position  |

The state of the mouse buttons is returned in the .A register:

| Bit | Description   |
|-----|---------------|
| 0   | Left Button   |
| 1   | Right Button  |
| 2   | Middle Button |

If a button is pressed, the corresponding bit is set.

**EXAMPLE:**

	LDX #$70
	JSR mouse_get ; get mouse position in $70/$71 (X) and $72/$73 (Y)
	AND #1
	BNE BUTTON_PRESSED


#### Joystick

$FF53: `joystick_scan` - query joysticks
$FF56: `joystick_get` - get state of one joystick

##### Function Name: joystick_scan

Purpose: Query the joysticks and save their state
Call address: $FF53
Communication registers: None
Preparatory routines: None
Error returns: None
Stack requirements: 0
Registers affected: .A, .X, .Y

**Description:** The routine `joystick_scan` retrieves all state from the four joysticks and saves it. It can then be retrieved using `joystick_get`. The default interrupt handler already takes care of this, so this routine should only be called if the interrupt handler has been completely replaced.

##### Function Name: joystick_get

Purpose: Get the state of one of the joysticks
Call address: $FF56
Communication registers: .A
Preparatory routines: `joystick_scan`
Error returns: None
Stack requirements: 0
Registers affected: .A, .X, .Y

**Description:** The routine `joystick_get` retrieves all state from one of the joysticks. The number of the joystick is passed in .A (0 for the keyboard joystick and 1 through 4 for SNES controllers), and the state is returned in .A, .X and .Y.

      .A, byte 0:      | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
                  SNES | B | Y |SEL|STA|UP |DN |LT |RT |

      .X, byte 1:      | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
                  SNES | A | X | L | R | 1 | 1 | 1 | 1 |
      .Y, byte 2:
                  $00 = joystick present
                  $FF = joystick not present

If a button is pressed, the corresponding bit is zero.

(With a dedicated handler, the API can also be used for other devices with an SNES controller connector. The data returned in .A/.X/Y is just the raw 24 bits returned by the device.)

The keyboard joystick uses the standard SNES9X/ZSNES mapping:

| SNES Button    |Keyboard Key  | Alt. Keyboard Key |
|----------------|--------------|-------------------|
| A              | X            | Left Ctrl         |
| B              | Z            | Left Alt          |
| X              | S            |                   |
| Y              | A            |                   |
| L              | D            |                   |
| R              | C            |                   |
| START          | Enter        |                   |
| SELECT         | Left Shift   |                   |
| D-Pad          | Cursor Keys  |                   |

Note that the keyboard joystick will allow LEFT and RIGHT as well as UP and DOWN to be pressed at the same time, while controllers usually prevent this mechanically.

**How to Use:**

If the default interrupt handler is used:

1) Call this routine.

If the default interrupt handler is disabled or replaced:

1) Call `joystick_scan` to have the system query the joysticks.
2) Call this routine.

**EXAMPLE:**

      JSR joystick_scan
      LDA #0
      JSR joystick_get
      TXA
      AND #128
      BEQ A_PRESSED

#### I2C

$FEC6: `i2c_read_byte` - read a byte from an I2C device
$FEC9: `i2c_write_byte` - write a byte to an I2C device

##### Function Name: i2c_read_byte

Purpose: Read a byte at a given offset from a given I2C device
Call address: $FEC6
Communication registers: .A, .X, .Y
Preparatory routines: None
Error returns: .C = 1 in case of error
Stack requirements: [?]
Registers affected: .A

**Description:** The routine `i2c_read_byte` reads a single byte at offset .Y from I2C device .X and returns the result in .A. .C is 0 if the read was successful, and 1 if no such device exists.

**EXAMPLE:**

	LDX #$6F ; RTC device
	LDY #$20 ; start of NVRAM inside RTC
	JSR i2c_read_byte ; read first byte of NVRAM

##### Function Name: i2c_write_byte

Purpose: Write a byte at a given offset to a given I2C device
Call address: $FEC9
Communication registers: .A, .X, .Y
Preparatory routines: None
Error returns: .C = 1 in case of error
Stack requirements: [?]
Registers affected: .A

**Description:** The routine `i2c_write_byte` writes the byte in .A at offset .Y of I2C device .X. .C is 0 if the write was successful, and 1 if no such device exists.

**EXAMPLES:**

	LDX #$6F ; RTC device
	LDY #$20 ; start of NVRAM inside RTC
	LDA #'X'
	JSR i2c_write_byte ; write first byte of NVRAM

	LDX #$42 ; System Management Controller
	LDY #$01 ; magic location for system poweroff
	LDA #$00 ; magic value for system poweroff
	JSR i2c_write_byte ; power off the system

#### Sprites

$FEF0: `sprite_set_image` - set the image of a sprite
$FEF3: `sprite_set_position` - set the position of a sprite

##### Function Name: sprite_set_image

Purpose: Set the image of a sprite
Call address: $FEF0
Signature: bool sprite_set_image(byte number: .a, width: .x, height: .y, apply_mask: .c, word pixels: r0, word mask: r1, byte bpp: r2L);
Error returns: .C = 1 in case of error

**Description:** This function sets the image of a sprite. The number of the sprite is given in .A, The bits per pixel (bpp) in r2L, and the width and height in .X and .Y. The pixel data at r0 is interpreted accordingly and converted into the graphics hardware's native format. If the .C flag is set, the transparency mask pointed to by r1 is applied during the conversion. The function returns .C = 0 if converting the data was successful, and .C = 1 otherwise. Note that this does not change the visibility of the sprite.

**Note**: There are certain limitations on the possible values of width, height, bpp and apply_mask:

* width and height may not exceed the hardware's capabilities.
* Legal values for bpp are 1, 4 and 8. If the hardware only supports lower depths, the image data is converted down.
* apply_mask is only valid for 1 bpp data.

##### Function Name: sprite_set_position

Purpose: Set the position of a sprite or hide it.
Call address: $FEF3
Signature: void sprite_set_position(byte number: .a, word x: r0, word y: r1);
Error returns: None

**Description:** This function shows a given sprite (.A) at a certain position or hides it. The position is passed in r0 and r1. If the x position is negative (>$8000), the sprite will be hidden.

#### Framebuffer

The framebuffer API is a low-level graphics API that completely abstracts the framebuffer by exposing a minimal set of high-performance functions. It is useful as an abstraction and as a convenience library for applications that need high performance framebuffer access.

$FEF6: `FB_init` - enable graphics mode
$FEF9: `FB_get_info` - get screen size and color depth
$FEFC: `FB_set_palette` - set (parts of) the palette
$FEFF: `FB_cursor_position` - position the direct-access cursor
$FF02: `FB_cursor_next_line` - move direct-access cursor to next line
$FF05: `FB_get_pixel` - read one pixel, update cursor
$FF08: `FB_get_pixels` - copy pixels into RAM, update cursor
$FF0B: `FB_set_pixel` - set one pixel, update cursor
$FF0E: `FB_set_pixels` - copy pixels from RAM, update cursor
$FF11: `FB_set_8_pixels` - set 8 pixels from bit mask (transparent), update cursor
$FF14: `FB_set_8_pixels_opaque` - set 8 pixels from bit mask (opaque), update cursor
$FF17: `FB_fill_pixels` - fill pixels with constant color, update cursor
$FF1A: `FB_filter_pixels` - apply transform to pixels, update cursor
$FF1D: `FB_move_pixels` - copy horizontally consecutive pixels to a different position

All calls are vectored, which allows installing a replacement framebuffer driver.

$02E4: I_FB_init
$02E6: I_FB_get_info
$02E8: I_FB_set_palette
$02EA: I_FB_cursor_position
$02EC: I_FB_cursor_next_line
$02EE: I_FB_get_pixel
$02F0: I_FB_get_pixels
$02F2: I_FB_set_pixel
$02F4: I_FB_set_pixels
$02F6: I_FB_set_8_pixels
$02F8: I_FB_set_8_pixels_opaque
$02FA: I_FB_fill_pixels
$02FC: I_FB_filter_pixels
$02FE: I_FB_move_pixels

The model of this API is based on the direct-access cursor. In order to read and write pixels, the cursor has to be set to a specific x/y-location, and all subsequent calls will access consecutive pixels at the cursor position and update the cursor.

The default driver supports the VERA framebuffer at a resolution of 320x200 pixels and 256 colors. Using `screen_mode` to set mode $80 will enable this driver.

##### Function Name: FB_init

Signature: void FB_init();
Purpose: Enter graphics mode.

##### Function Name: FB_get_info

Signature: void FB_get_info(out word width: r0, out word height: r1, out byte color_depth: .a);
Purpose: Return the resolution and color depth

##### Function Name: FB_set_palette

Signature: void FB_set_palette(word pointer: r0, index: .a, byte count: .x);
Purpose: Set (parts of) the palette

[Note: This is not yet implemented.]

##### Function Name: FB_cursor_position

Signature: void FB_cursor_position(word x: r0, word y: r1);
Purpose: Position the direct-access cursor

**Description:** `FB_cursor_position` sets the direct-access cursor to the given screen coordinate. Future operations will access pixels at the cursor location and update the cursor.

##### Function Name: FB_cursor_next_line

Signature: void FB_cursor_next_line(word x: r0);
Purpose: Move the direct-access cursor to next line

**Description:** `FB_cursor_next_line` increments the y position of the direct-access cursor, and sets the x position to the same one that was passed to the previous `FB_cursor_position` call. This is useful for drawing rectangular shapes, and faster than explicitly positioning the cursor.

##### Function Name: FB_get_pixel

Signature: byte FB_get_pixel();
Purpose: Read one pixel, update cursor

##### Function Name: FB_get_pixels

Signature: void FB_get_pixels(word ptr: r0, word count: r1);
Purpose: Copy pixels into RAM, update cursor

**Description:** This function copies pixels into an array in RAM. The array consists of one byte per pixel.

##### Function Name: FB_set_pixel

Signature: void FB_set_pixel(byte color: .a);
Purpose: Set one pixel, update cursor

##### Function Name: FB_set_pixels

Signature: void FB_set_pixels(word ptr: r0, word count: r1);
Purpose: Copy pixels from RAM, update cursor

**Description:** This function sets pixels from an array of pixels in RAM. The array consists of one byte per pixel.

##### Function Name: FB_set_8_pixels

Signature: void FB_set_8_pixels(byte pattern: .a, byte color: .x);
Purpose: Set 8 pixels from bit mask (transparent), update cursor

**Description:** This function sets all 1-bits of the pattern to a given color and skips a pixel for every 0 bit. The order is MSB to LSB. The cursor will be moved by 8 pixels.

##### Function Name: FB_set_8_pixels_opaque

Signature: void FB_set_8_pixels_opaque(byte pattern: .a, byte mask: r0L, byte color1: .x, byte color2: .y);
Purpose: Set 8 pixels from bit mask (opaque), update cursor

**Description:** For every 1-bit in the mask, this function sets the pixel to color1 if the corresponding bit in the pattern is 1, and to color2 otherwise. For every 0-bit in the mask, it skips a pixel. The order is MSB to LSB. The cursor will be moved by 8 pixels.

##### Function Name: FB_fill_pixels

Signature: void FB_fill_pixels(word count: r0, word step: r1, byte color: .a);
Purpose: Fill pixels with constant color, update cursor

**Description:** `FB_fill_pixels` sets pixels with a constant color. The argument `step` specifies the increment between pixels. A value of 0 or 1 will cause consecutive pixels to be set. Passing a `step` value of the screen width will set vertically adjacent pixels going top down. Smaller values allow drawing dotted horizontal lines, and multiples of the screen width allow drawing dotted vertical lines.

*[Note: Only the values 0/1 and screen width are currently supported.]*

##### Function Name: FB_filter_pixels

Signature: void FB_filter_pixels(word ptr: r0, word count: r1);
Purpose: Apply transform to pixels, update cursor

**Description:** This function allows modifying consecutive pixels. The function pointer will be called for every pixel, with the color in .a, and it needs to return the new color in .a.

##### Function Name: FB_move_pixels

Signature: void FB_move_pixels(word sx: r0, word sy: r1, word tx: r2, word ty: r3, word count: r4);
Purpose: Copy horizontally consecutive pixels to a different position

*[Note: Overlapping regions are not yet supported.]*

#### Graphics

The high-level graphics API exposes a set of standard functions. It allows applications to easily perform some common high-level actions like drawing lines, rectangles and images, as well as moving parts of the screen. All commands are completely implemented on top of the framebuffer API, that is, they will continue working after replacing the framebuffer driver with one that supports a different resolution, color depth or even graphics device.

$FF20: `GRAPH_init` - initialize graphics
$FF23: `GRAPH_clear` - clear screen
$FF26: `GRAPH_set_window` - set clipping region
$FF29: `GRAPH_set_colors` - set stroke, fill and background colors
$FF2C: `GRAPH_draw_line` - draw a line
$FF2F: `GRAPH_draw_rect` - draw a rectangle (optionally filled)
$FF32: `GRAPH_move_rect` - move pixels
$FF35: `GRAPH_draw_oval` - draw an oval or circle
$FF38: `GRAPH_draw_image` - draw a rectangular image
$FF3B: `GRAPH_set_font` - set the current font
$FF3E: `GRAPH_get_char_size` - get size and baseline of a character
$FF41: `GRAPH_put_char` - print a character

##### Function Name: GRAPH_init

Signature: void GRAPH_init(word vectors: r0);
Purpose: Activate framebuffer driver, enter and initialize graphics mode

**Description**: This call activates the framebuffer driver whose vector table is passed in r0. If r0 is 0, the default driver is activated. It then switches the video hardware into graphics mode, sets the window to full screen, initializes the colors and activates the system font.

##### Function Name: GRAPH_clear

Signature: void GRAPH_clear();
Purpose: Clear the current window with the current background color.

##### Function Name: GRAPH_set_window

Signature: void GRAPH_set_window(word x: r0, word y: r1, word width: r2, word height: r3);
Purpose: Set the clipping region

**Description:** All graphics commands are clipped to the window. This function configures the origin and size of the window. All 0 arguments set the window to full screen.

*[Note: Only text output and GRAPH_clear currently respect the clipping region.]*

##### Function Name: GRAPH_set_colors

Signature: void GRAPH_set_colors(byte stroke: .a, byte fill: .x, byte background: .y);
Purpose: Set the three colors

**Description:** This function sets the three colors: The stroke color, the fill color and the background color.

##### Function Name: GRAPH_draw_line

Signature: void GRAPH_draw_line(word x1: r0, word y1: r1, word x2: r2, word y2: r3);
Purpose: Draw a line using the stroke color

##### Function Name: GRAPH_draw_rect

Signature: void GRAPH_draw_rect(word x: r0, word y: r1, word width: r2, word height: r3, word corner_radius: r4, bool fill: .c);
Purpose: Draw a rectangle.

**Description:** This function will draw the frame of a rectangle using the stroke color. If `fill` is `true`, it will also fill the area using the fill color. To only fill a rectangle, set the stroke color to the same value as the fill color.

*[Note: The border radius is currently unimplemented.]*

##### Function Name: GRAPH_move_rect

Signature: void GRAPH_move_rect(word sx: r0, word sy: r1, word tx: r2, word ty: r3, word width: r4, word height: r5);
Purpose: Copy a rectangular screen area to a different location

**Description:** `GRAPH_move_rect` coll copy a rectangular area of the screen to a different location. The two areas may overlap.

*[Note: Support for overlapping is not currently implemented.]*

##### Function Name: GRAPH_draw_oval

Signature: void GRAPH_draw_oval(word x: r0, word y: r1, word width: r2, word height: r3, bool fill: .c);
Purpose: Draw an oval or a circle

**Description:** This function draws an oval filling the given bounding box. If width equals height, the resulting shape is a circle. The oval will be outlined by the stroke color. If `fill` is `true`, it will be filled using the fill color. To only fill an oval, set the stroke color to the same value as the fill color.

##### Function Name: GRAPH_draw_image

Signature: void GRAPH_draw_image(word x: r0, word y: r1, word ptr: r2, word width: r3, word height: r4);
Purpose: Draw a rectangular image from data in memory

**Description:** This function copies pixel data from memory onto the screen. The representation of the data in memory has to have one byte per pixel, with the pixels organized line by line top to bottom, and within the line left to right.

##### Function Name: GRAPH_set_font

Signature: void GRAPH_set_font(void ptr: r0);
Purpose: Set the current font

**Description:** This function sets the current font to be used for the remaining font-related functions. The argument is a pointer to the font data structure in memory, which must be in the format of a single point size GEOS font (i.e. one GEOS font file VLIR chunk). An argument of 0 will activate the built-in system font.

##### Function Name: GRAPH_get_char_size

Signature: (byte baseline: .a, byte width: .x, byte height_or_style: .y, bool is_control: .c) GRAPH_get_char_size(byte c: .a, byte format: .x);
Purpose: Get the size and baseline of a character, or interpret a control code

**Description:** This functionality of `GRAPH_get_char_size` depends on the type of code that is passed in: For a printable character, this function returns the metrics of the character in a given format. For a control code, it returns the resulting format. In either case, the current format is passed in .x, and the character in .a.

* The format is an opaque byte value whose value should not be relied upon, except for `0`, which is plain text.
* The resulting values are measured in pixels.
* The baseline is measured from the top.

##### Function Name: GRAPH_put_char

Signature: void GRAPH_put_char(inout word x: r0, inout word y: r1, byte c: .a);
Purpose: Print a character onto the graphics screen

**Description:** This function prints a single character at a given location on the graphics screen. The location is then updated. The following control codes are supported:

* $01: SWAP COLORS
* $04: ATTRIBUTES: UNDERLINE
* $06: ATTRIBUTES: BOLD
* $07: BELL
* $08: BACKSPACE
* $09: TAB
* $0A: LF
* $0B: ATTRIBUTES: ITALICS
* $0C: ATTRIBUTES: OUTLINE
* $0D/$8D: REGULAR/SHIFTED RETURN
* $11/$91: CURSOR: DOWN/UP
* $12: ATTRIBUTES: REVERSE
* $13/$93: HOME/CLEAR
* $14 DEL
* $92: ATTRIBUTES: CLEAR ALL
* all color codes

Notes:

* CR ($0D) SHIFT+CR ($8D) and LF ($0A) all set the cursor to the beginning of the next line. The only difference is that CR and SHIFT+CR reset the attributes, and LF does not.
* BACKSPACE ($08) and DEL ($14) move the cursor to the beginning of the previous character but does not actually clear it. Multiple consecutive BACKSPACE/DEL characters are not supported.
* There is no way to individually disable attributes (underlined, bold, reversed, italics, outline). The only way to disable them is to reset the attributes using code $92, which switches to plain text.
* All 16 PETSCII color codes are supported. Code $01 to swap the colors will swap the stroke and fill colors.
* The stroke color is used to draw the characters, and the underline is drawn using the fill color. In reverse text mode, the text background is filled with the fill color.
* *[BELL ($07), TAB ($09) and SHIFT+TAB ($18) are not yet implemented.]*

#### Console

$FEDB: `console_init` - initialize console mode
$FEDE: `console_put_char` - print character to console
$FED8: `console_put_image` - draw image as if it was a character
$FEE1: `console_get_char` - get character from console
$FED5: `console_set_paging_message` - set paging message or disable paging

The console is a screen mode that allows text output and input in proportional fonts that support the usual styles. It is useful for rich text-based interfaces.

##### Function Name: console_init

Signature: void console_init(word x: r0, word y: r1, word width: r2, word height: r3);
Purpose: Initialize console mode.
Call address: $FEDB

**Description:** This function initializes console mode. It sets up the window (text clipping area) passed into it, clears the window and positions the cursor at the top left. All 0 arguments create a full screen console. You have to switch to graphics mode using `screen_mode` beforehand.

##### Function Name: console_put_char

Signature: void console_put_char(byte char: .a, bool wrapping: .c);
Purpose: Print a character to the console.
Call address: $FEDE

**Description:** This function prints a character to the console. The .C flag specifies whether text should be wrapped at character (.C=0) or word (.C=1) boundaries. In the latter case, characters will be buffered until a SPACE, CR or LF character is sent, so make sure the text that is printed always ends in one of these characters.

**Note**: If the bottom of the screen is reached, this function will scroll its contents up to make extra room.

##### Function Name: console_put_image

Signature: void console_put_image(word ptr: r0, word width: r1, word height: r2);
Purpose: Draw image as if it was a character.
Call address: $FEE1

**Description:** This function draws an image (in GRAPH_draw_image format) at the current cursor position and advances the cursor accordingly. This way, an image can be presented inline. A common example would be an emoji bitmap, but it is also possible to show full-width pictures if you print a newline before and after the image.

**Notes**:

* If the bottom of the screen is reached, this function will scroll its contents up to make extra room.
* Subsequent line breaks will take the image height into account, so that the new cursor position is below the image.

##### Function Name: console_get_char

Signature: (byte char: .a) console_get_char();
Purpose: Get a character from the console.
Call address: $FEE1

**Description:** This function gets a character to the console. It does this by collecting a whole line of character, i.e. until the user presses RETURN. Then, the line will be sent character by character.

This function allows editing the line using BACKSPACE/DEL, but does not allow moving the cursor within the line, write more than one line, or using control codes.

##### Function Name: console_set_paging_message

Signature: void console_set_paging_message(word message: r0);
Purpose: Set the paging message or disable paging.
Call address: $FED5

**Description:** The console can halt printing after a full screen height worth of text has been printed. It will then show a message, wait for any key, and continue printing. This function sets this message. A zero-terminated text is passed in r0. To turn off paging, call this function with r0 = 0 - this is the default.

**Note:** It is possible to use control codes to change the text style and color. Do not use codes that change the cursor position, like CR or LF. Also, the text must not overflow one line on the screen.

#### Other

$FEE4: `memory_fill` - fill memory region with a byte value
$FEE7: `memory_copy` - copy memory region
$FEEA: `memory_crc` - calculate CRC16 of memory region
$FEED: `memory_decompress` - decompress LZSA2 block
$FECF: `entropy_get` - get 24 random bits
$FF44: `monitor` - enter machine language monitor
$FF47: `enter_basic` - enter BASIC
$FF5F: `screen_mode` - get/set screen mode
$FF62: `screen_set_charset` - activate 8x8 text mode charset

##### Function Name: memory_fill

Signature: void memory_fill(word address: r0, word num_bytes: r1, byte value: .a);
Purpose: Fill a memory region with a byte value.
Call address: $FEE4

**Description:** This function fills the memory region specified by an address (r0) and a size in bytes (r1) with the constant byte value passed in .A.

##### Function Name: memory_copy

Signature: void memory_copy(word source: r0, word target: r1, word num_bytes: r2);
Purpose: Copy a memory region to a different region.
Call address: $FEE7

**Description:** This function copies one memory region specified by an address (r0) and a size in bytes (r2) to a different region specified by its start address (r1). The two regions may overlap.

##### Function Name: memory_crc

Signature: (word result: r2) memory_crc(word address: r0, word num_bytes: r1);
Purpose: Calculate the CRC16 of a memory region.
Call address: $FEEA

**Description:** This function calculates the CRC16 checksum of the memory region specified by an address (r0) and a size in bytes (r1). The result is returned in r2.

##### Function Name: memory_decompress

Signature: void memory_decompress(word input: r0, inout word output: r1);
Purpose: Decompress an LZSA2 block
Call address: $FEED

**Description:** This function decompresses an LZSA2-compressed data block from the location passed in r0 and outputs the decompressed data at the location passed in r1. After the call, r1 will be updated with the location of the last output byte plus one.

**Notes**:

* To create compressed data, use the `lzsa` tool[^4] like this:
`lzsa -r -f2 <original_file> <compressed_file>`
* This function cannot be used to decompress data in-place, as the output data would overwrite the input data before it is consumed. Therefore, make sure to load the input data to a different location.
* It is possible to have the input data stored in banked RAM, with the obvious 8 KB size restriction.

##### Function Name: entropy_get

Purpose: Get 24 random bits
Call address: $FECF
Communication registers: .A, .X, .Y
Preparatory routines: None
Error returns: None
Registers affected: .A, .X, .Y

**Description:** This routine returns 24 somewhat random bits in registers .A, .X, and .Y. In order to get higher-quality random numbers, this data should be fed into a pseudo-random number generator.

**How to Use:**
1) Call this routine.

**EXAMPLE:**

    ; throw a dice
    again:
      JSR entropy_get
      STX tmp   ; combine 24 bits
      EOR tmp   ; using exclusive-or
      STY tmp   ; to get a higher-quality
      EOR tmp   ; 8 bit random value
      STA tmp
      LSR
      LSR
      LSR
      LSR       ; combine resulting 8 bits
      EOR tmp   ; to get 4 bits
      AND #7    ; we're down to values 0-7
      CMP #0
      BEQ again ; 0 is illegal
      CMP #7
      BEQ again ; 7 is illegal
      ORA #$30  ; convert to ASCII
      JMP $FFD2 ; print character

##### Function Name: monitor

Purpose: Enter the machine language monitor
Call address: $FF44
Communication registers: None
Preparatory routines: None
Error returns: Does not return
Stack requirements: Does not return
Registers affected: Does not return

**Description:** This routine switches from BASIC to machine language monitor mode. It does not return to the caller. When the user quits the monitor, it will restart BASIC.

**How to Use:**
1) Call this routine.

**EXAMPLE:**

      JMP monitor

##### Function Name: enter_basic

Purpose: Enter BASIC
Call address: $FF47
Communication registers: .C
Preparatory routines: None
Error returns: Does not return

**Description:** Call this to enter BASIC mode, either through a cold start (.C=1) or a warm start (.C=0).

**EXAMPLE:**

	CLC
	JMP enter_basic ; returns to the "READY." prompt


##### Function Name: screen_mode

Purpose: Get/Set the screen mode
Call address: $FF5F
Communication registers: .A, .C
Preparatory routines: None
Error returns: .C = 1 in case of error
Stack requirements: [?]
Registers affected: .A, .X, .Y

**Description:** If .C is set, a call to this routine gets the current screen mode in .A. If .C is clear, it sets the current screen mode to the value in .A. For a list of possible values, see the basic statement `SCREEN`. If the mode is unsupported, .C will be set, otherwise cleared.

**EXAMPLE:**

	LDA #$80
	clc
	JSR screen_mode ; SET 320x200@256C MODE
	BCS FAILURE

##### Function Name: screen_set_charset

Purpose: Activate a 8x8 text mode charset
Call address: $FF62

Communication registers: .A, .X, .Y
Preparatory routines: None
Stack requirements: [?]
Registers affected: .A, .X, .Y

**Description:** A call to this routine uploads a character set to the video hardware and activates it. The value of .A decides what charset to upload:

| Value | Description          |
|-------|----------------------|
| 0     | use pointer in .X/.Y |
| 1     | ISO                  |
| 2     | PET upper/graph      |
| 3     | PET upper/lower      |

If .A is zero, .X (lo) and .Y (hi) contain a pointer to a 2 KB RAM area that gets uploaded as the new 8x8 character set. The data has to consist of 256 characters of 8 bytes each, top to bottom, with the MSB on the left and set bits representing the foreground color.

**EXAMPLE:**

	LDA #0
	LDX #<MY_CHARSET
	LDY #>MY_CHARSET
	JSR screen_set_charset ; UPLOAD CUSTOM CHARSET "MY_CHARSET"

##### Function Name: JSRFAR

Purpose: Execute a routine on another RAM or ROM bank
Call address: $FF6E
Communication registers: None
Preparatory routines: None
Error returns: None
Stack requirements: 4
Registers affected: None

**Description:** The routine `JSRFAR` enables code to execute some other code located on a specific RAM or ROM bank. This works independently of which RAM or ROM bank the currently executing code is residing in.
The 16 bit address and the 8 bit bank number have to follow the instruction stream. The `JSRFAR` routine will switch both the ROM and the RAM bank to the specified bank and restore it after the routine's `RTS`. Execution resumes after the 3 byte arguments.
**Note**: The C128 also has a `JSRFAR` function at $FF6E, but it is incompatible with the X16 version.

**How to Use:**
1) Call this routine.

**EXAMPLE:**

      JSR JSRFAR
      .WORD $C000 ; ADDRESS
      .BYTE 1     ; BANK


## Math Library

The Commander X16 contains a floating point Math library with a precision of 40 bits, which corresponds to 9 decimal digits. It is a stand-alone derivative of the library contained in Microsoft BASIC. Except for the different base address, it is compatible with the C128 and C65 libraries.

The following functions are available from machine language code after setting the ROM bank to 4.

### Format Conversions

| C128  | C65   | X16   | Symbol   | Description                            |
|-------|-------|-------|----------|----------------------------------------|
| $AF00 | $7F00 | $FE00 | `AYINT`  | convert floating point to integer      |
| $AF03 | $7F03 | $FE03 | `GIVAYF` | convert integer to floating point      |
| $AF06 | $7F06 | $FE06 | `FOUT`   | convert floating point to ASCII string |
| $AF09 | $7F09 | $FE09 | `VAL_1`  | convert ASCII string to floating point<br/>*[not yet implemented]*|
| $AF0C | $7F0C | $FE0C | `GETADR` | convert floating point to an address   |
| $AF0F | $7F0F | $FE0F | `FLOATC` | convert address to floating point      |

### Math Functions

| C128  | C65   | X16   | Symbol   | Description                            |
|-------|-------|-------|----------|----------------------------------------|
| $AF12 | $7F12 | $FE12 | `FSUB`   | MEM - FACC                             |
| $AF15 | $7F15 | $FE15 | `FSUBT`  | ARG - FACC                             |
| $AF18 | $7F18 | $FE18 | `FADD`   | MEM + FACC                             |
| $AF1B | $7F1B | $FE1B | `FADDT`  | ARG + FACC                             |
| $AF1E | $7F1E | $FE1E | `FMULT`  | MEM * FACC                             |
| $AF21 | $7F21 | $FE21 | `FMULTT` | ARG * FACC                             |
| $AF24 | $7F24 | $FE24 | `FDIV`   | MEM / FACC                             |
| $AF27 | $7F27 | $FE27 | `FDIVT`  | ARG / FACC                             |
| $AF2A | $7F2A | $FE2A | `LOG`    | compute natural log of FACC            |
| $AF2D | $7F2D | $FE2D | `INT`    | perform BASIC INT() on FACC            |
| $AF30 | $7F30 | $FE30 | `SQR`    | compute square root of FACC            |
| $AF33 | $7F33 | $FE33 | `NEGOP`  | negate FACC                            |
| $AF36 | $7F36 | $FE36 | `FPWR`   | raise ARG to the MEM power             |
| $AF39 | $7F39 | $FE39 | `FPWRT`  | raise ARG to the FACC power            |
| $AF3C | $7F3C | $FE3C | `EXP`    | compute EXP of FACC                    |
| $AF3F | $7F3F | $FE3F | `COS`    | compute COS of FACC                    |
| $AF42 | $7F42 | $FE42 | `SIN`    | compute SIN of FACC                    |
| $AF45 | $7F45 | $FE45 | `TAN`    | compute TAN of FACC                    |
| $AF48 | $7F48 | $FE48 | `ATN`    | compute ATN of FACC                    |
| $AF4B | $7F4B | $FE4B | `ROUND`  | round FACC                             |
| $AF4E | $7F4E | $FE4E | `ABS`    | absolute value of FACC                 |
| $AF51 | $7F51 | $FE51 | `SIGN`   | test sign of FACC                      |
| $AF54 | $7F54 | $FE54 | `FCOMP`  | compare FACC with MEM                  |
| $AF57 | $7F57 | $FE57 | `RND_0`  | generate random floating point number  |

### Movement

| C128  | C65   | X16   | Symbol   | Description                            |
|-------|-------|-------|----------|----------------------------------------|
| $AF5A | $7F5A | $FE5A | `CONUPK` | move RAM MEM to ARG                    |
| $AF5D | $7F5D | $FE5D | `ROMUPK` | move ROM MEM to ARG                    |
| $AF60 | $7F60 | $FE60 | `MOVFRM` | move RAM MEM to FACC                   |
| $AF63 | $7F63 | $FE63 | `MOVFM`  | move ROM MEM to FACC                   |
| $AF66 | $7F66 | $FE66 | `MOVMF`  | move FACC to MEM                       |
| $AF69 | $7F69 | $FE69 | `MOVFA`  | move ARG to FACC                       |
| $AF6C | $7F6C | $FE6C | `MOVAF`  | move FACC to ARG                       |

### X16 Additions

The following calls are not part of the C128/C65 API.

| X16   | Symbol   | Description                                     |
|-------|----------|-------------------------------------------------|
| $FE81 | FADDH    | FAC += .5                                       |
| $FE84 | ZEROFC   | FAC = 0                                         |
| $FE87 | NORMAL   | Normalize FAC                                   |
| $FE8A | NEGFAC   | FAC = -FAC                                      |
| $FE8D | MUL10    | FAC *= 10                                       |
| $FE90 | DIV10    | FAC /= 10                                       |
| $FE93 | MOVEF    | ARG = FAC                                       |
| $FE96 | SGN      | FAC = sgn(FAC)                                  |
| $FE99 | FLOAT    | FAC = (u8).A                                    |
| $FE9C | FLOATS   | FAC = (s16)facho+1:facho                        |
| $FE9F | QINT     | facho:facho+1:facho+2:facho+2 = u32(FAC)        |
| $FEA2 | FINLOG   | FAC += (s8).A                                   |
| $FEA5 | FOUTC    | Convert FAC to ASCIIZ string at fbuffr - 1 + .Y |

<!-- https://github.com/commanderx16/x16-rom/issues/245
| $FEA8 | POLYX    | Polynomial Evaluation 1 (SIN/COS/ATN/LOG)       |
| $FEAB | POLY     | Polynomial Evaluation 2 (EXP)                   |
-->

### Notes

* The full documentation of these functions can be found in the book [C128 Developers Package for Commodore 6502 Development](http://www.zimmers.net/anonftp/pub/cbm/schematics/computers/c128/servicemanuals/C128_Developers_Package_for_Commodore_6502_Development_(1987_Oct).pdf).
* `RND_0`: For .Z=1, the C128 and C65 versions get entropy from the CIA timers. The X16 version takes entropy from .A/.X/.Y instead. So in order to get a "real" random number, you would use code like this:

        LDA #$00
        PHP
        JSR entropy_get ; KERNAL call to get entropy into .A/.X/.Y
        PLP             ; restore .Z=1
        JSR RND_0
* The calls `FADDT`, `FMULTT`, `FDIVT` and `FPWRT` were broken on on the C128/C65. They are fixed on the X16.
* For more information on the additional calls, refer to [Mapping the Commodore 64](http://unusedino.de/ec64/technical/project64/mapping_c64.html) by Sheldon Leemon, ISBN 0-942386-23-X, but note these errata:
   * `FMULT` at $BA28 adds mem to FAC, not ARG to FAC
   * `NORMAL` at $B8D7 is incorrectly documented as being at $B8FE


## Machine Language Monitor

The built-in machine language monitor can be started with the `MON` BASIC command. It is based on the monitor of the Final Cartridge III and supports all its features. See the [Final Cartridge III Manual](https://rr.pokefinder.org/rrwiki/images/7/70/Final_Cartridge_III_english_Manual.pdf) more more information.

If you invoke the monitor by mistake, you can exit with by typing `X`, followed by the `RETURN` key.

Some features specific to this monitor are:
* The `I` command prints a CBM-ASCII-encoded memory dump.
* The `EC` command prints a binary memory dump. This is also useful for character sets.
* Scrolling the screen with the cursors or F3/F5 will continue memory dumps and disassemblies, and even disassemble backwards.

The following additions have been made:

* The instruction set extensions of the 65C02 are supported.
* The `O` command takes an 8 bit hex value as an argument and sets it as the ROM and RAM bank for reading and writing memory contents. The following example disassembles the beginning of the CBDOS ROM on bank 5:

      O05
      DC000 C015

* The `OV` command takes a 4 bit hex value as an argument and sets it as the bank in the video address space for reading and writing memory contents. The following example shows the character ROM in the video controller's address space:

      OV1
      ECF000 F00F

*[TODO: Full documentation]*

## Memory Map

The Commander X16 has 64 KB of ROM and 2,088 KB (2 MB[^1] + 40 KB) of RAM. Some of the ROM and RAM is always visible at certain address ranges, while the remaining ROM and RAM is banked into one of two address windows.

This is an overview of the X16 memory map:

|Addresses  |Description                                                       |
|-----------|------------------------------------------------------------------|
|$0000-$9EFF|Fixed RAM (40 KB minus 256 bytes)								   |
|$9F00-$9FFF|I/O Area (256 bytes)											   |
|$A000-$BFFF|Banked RAM (8 KB window into one of 256 banks for a total of 2 MB)|
|$C000-$FFFF|Banked ROM (16 KB window into one of 32 banks for a total of 512 KB) |

### Banked Memory

The currently enabled RAM and ROM banks can be configured by writing to zero page locations 0 and 1:

|Address  |Description              |
|---------|-------------------------|
|$0000    |Current RAM bank (0-255) |
|$0001    |Current ROM bank (0-31)  |

The currently set banks can also be read back from the respective memory locations. Both settings default to 0 on RESET. The upper three bits of location 1 are undefined.

### ROM Allocations

This is the allocation of the banks of banked ROM:

|Bank|Name   |Description                                            |
|----|-------|-------------------------------------------------------|
|0   |KERNAL |character sets (uploaded into VRAM), MONITOR, KERNAL   |
|1   |KEYBD  |Keyboard layout tables                                 |
|2   |CBDOS  |The computer-based CBM-DOS for FAT32 SD cards          |
|3   |GEOS   |GEOS KERNAL                                            |
|4   |BASIC  |BASIC interpreter                                      |
|5   |MONITOR|Machine Language Monitor                               |
|6   |CHARSET|PETSCII and ISO character sets (uploaded into VRAM)    |
|7   |CODEX  |CodeX16 Interactive Assembly Environment / Monitor     |
|6-31|–      |*[Currently unused]*                                   |

**Important**: The layout of the banks is still constantly changing.

### RAM Contents

This is the allocation of fixed RAM in the KERNAL/BASIC environment.

|Addresses  |Description                                                     |
|-----------|----------------------------------------------------------------|
|$0000-$00FF|Zero page                                                       |
|$0100-$01FF|CPU stack                                                       |
|$0200-$03FF|KERNAL and BASIC variables, vectors                             |
|$0400-$07FF|Available for machine code programs or custom data storage      |
|$0800-$9EFF|BASIC program/variables; available to the user                  |

The $0400-$07FF can be seen as the equivalent of $C000-$CFFF on a C64. A typical use would be for helper machine code called by BASIC.

#### Zero Page

|Addresses  |Description                            |
|-----------|---------------------------------------|
|$0000-$0001|Banking registers                      |
|$0002-$0021|16 bit registers r0-r15 for KERNAL API |
|$0022-$007F|Available to the user                  |
|$0080-$009C|Used by KERNAL and DOS                 |
|$009D-$00A8|Reserved for DOS/BASIC                 |
|$00A9-$00D3|Used by the Math library (and BASIC)   |
|$00D4-$00FF|Used by BASIC                          |

Machine code applications are free to reuse the BASIC area, and if they don't use the Math library, also that area.

#### Banking

This is the allocation of banked RAM in the KERNAL/BASIC environment.

|Bank |Description                                 |
|-----|--------------------------------------------|
|0    |Used for KERNAL/CBDOS variables and buffers |
|1-255|Available to the user                       |

(On systems with only 512 KB RAM, banks 64-255 are unavailable.)

During startup, the KERNAL activates RAM bank 1 as the default for the user.

### I/O Area

This is the memory map of the I/O Area:

|Addresses  |Description                  |
|-----------|-----------------------------|
|$9F00-$9F0F|VIA I/O controller #1        |
|$9F10-$9F1F|VIA I/O controller #2        |
|$9F20-$9F3F|VERA video controller        |
|$9F40-$9F41|YM2151 audio controller      |
|$9F42-$9F5F|Reserved                     |
|$9F60-$9FFF|External devices             |

## Video Programming

The VERA video chip supports resolutions up to 640x480 with up to 256 colors from a palette of 4096, two layers of either a bitmap or tiles, 128 sprites of up to 64x64 pixels in size. It can output VGA as well as a 525 line interlaced signal, either as NTSC or as RGB (Amiga-style).

See the [VERA Programmer's Reference](VERA%20Programmer's%20Reference.md) for the complete reference.

**IMPORTANT**: The VERA register layout has changed between 0.7 and 0.8. Here is the old documentation: [vera-module v0.7.pdf](https://github.com/commanderx16/x16-docs/blob/master/old/vera-module%20v0.7.pdf)

The X16 KERNAL uses the following video memory layout:

|Addresses    |Description                                   |
|-------------|----------------------------------------------|
|$00000-$12BFF|320x240@256c Bitmap                           |
|$12C00-$12FFF|*unused*                                      |
|$13000-$1AFFF|Sprites ($1000 per sprite)                    |
|$1B000-$1EBFF|Text Mode                                     |
|$1EC00-$1EFFF|*unused*                                      |
|$1F000-$1F7FF|Charset                                       |
|$1F800-$1F9BF|*unused*                                      |
|$1F9C0-$1FFFF|VERA internal (PSG, Palette, Sprite Registers)|

Application software is free to use any part of video RAM if it does not use the corresponding KERNAL functionality. To restore text mode, it just hast to call `CINT` ($FF81).

## Sound Programming

*[TODO]*

## I/O Programming

There are two 65C22 "Versatile Interface Adapter" (VIA) I/O controllers in the system, VIA#1 at address $9F60 and VIA#2 at address $9F70. The IRQ out lines of VIA#1 is connected to the CPU's NMI line, while the IRQ out line of VIA#2 is connected to the CPU's IRQ line.

The following tables describe the connections of the I/O pins:

**VIA#1**


|Pin  |Name      | Description                     |
|-----|----------|---------------------------------|
| PA0 | PS2KDAT  | PS/2 DATA keyboard              |
| PA1 | PS2KCLK  | PS/2 CLK  keyboard              |
| PA2 | NESLATCH | NES LATCH (for all controllers) |
| PA3 | NESCLK   | NES CLK   (for all controllers) |
| PA4 | NESDAT3  | NES DATA  (controller 3)        |
| PA5 | NESDAT2  | NES DATA  (controller 2)        |
| PA6 | NESDAT1  | NES DATA  (controller 1)        |
| PA7 | NESDAT0  | NES DATA  (controller 0)        |
| PB0 | PS2MDAT  | PS/2 DATA mouse                 |
| PB1 | PS2MCLK  | PS/2 CLK  mouse                 |
| PB2 | I2CDATA  | I2C DATA                        |
| PB3 | IECATTO  | Serial ATN  out                 |
| PB4 | IECCLKO  | Serial CLK  out                 |
| PB5 | IECDATAO | Serial DATA out                 |
| PB6 | IECCLKI  | Serial CLK  in                  |
| PB7 | IECDATAI | Serial DATA in                  |
| CB2 | I2CCLK   | I2C CLK                         |

**VIA#2**

The second VIA is completely unused by the system. All its 16 GPIOs and 4 handshake I/Os can be freely used.

### Custom keyboard scan code handler

On receiving a keyboard scan code, the KERNAL jumps to the address stored in $032E-032F. This makes
it possible to implement custom scan code handlers that extend or override the default behavior of the KERNAL.

Input set by the KERNAL: .X = PS/2 prefix, .A = PS/2 scan code, carry clear if key down and set if key up event.

Return from a custom handler with RTS. The KERNAL will continue handling the scan code according to the values of .X, .A and carry.  The KERNAL will, however, ignore the scan code if the zero flag is set.

```
;EXAMPLE: A custom handler that prints "A" on Alt key down

setup:
    sei
    lda #<keyhandler
    sta $032e
    lda #>keyhandler
    sta $032f
    cli
    rts

keyhandler:
    php         ;Save input on stack
    pha
    phx

    bcs exit    ;C=1 is key up

    cmp #$11    ;Alt key scan code
    bne exit    

    lda #'a'
    jsr $ffd2

exit:
    plx		;Restore input
    pla
    plp
    rts		;Return control to Kernal
```

### I2C Bus

The Commander X16 contains an I2C bus, which is implemented through two pins of VIA#1. The system management controller (SMC) and the real-time clock (RTC) are connected through this bus. The KERNAL APIs `i2c_read_byte` and `i2c_write_byte` allow talking to these devices.

#### System Management Controller

The system management controller (SMC) controls the power and activity LEDs, and an be used to power down the system or inject RESET or NMI signals.

| Register | Value      | Description             |
|----------|------------|-------------------------|
| 0x01     | 0x00       | Power off               |
| 0x01     | 0x01       | Hard reboot             |
| 0x02     | 0x00       | Inject RESET            |
| 0x03     | 0x00       | Inject NMI              |
| 0x04     | 0x00..0xFF | Power LED brightness    |
| 0x05     | 0x00..0xFF | Activity LED brightness |

#### Real-Time-Clock

The Commander X16 contains a battery-backed Microchip MCP7940N real-time-clock (RTC) chip. It provide a real-time clock/calendar, two alarms and 64 bytes of RAM.

For more information, please refer to this device's datasheet.

<hr>

[^1]: Current development systems have 2 MB of bankable RAM. Actual hardware is currently planned to have an option of either 512 KB or 2 MB of RAM.

[^3]: The pin assignment of the NES/SNES controller is likely to change.

[^4]: [https://github.com/emmanuel-marty/lzsa](https://github.com/emmanuel-marty/lzsa)
