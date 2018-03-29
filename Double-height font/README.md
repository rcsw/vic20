# VIC-20 double-height font

The file vic20-largefont is a binary image of a font with 8x16 chraracters, to be used in double-height character mode. To use in VICE:

1. Be sure you have expansion memory attached, as most of the built-in memory is required for the imported characters. The instructions below assume a 3K expanded VIC; you can alter the memory addresses accordingly for other memory settings. (If you know how to switch to 8x16 characters, you probably know what needs done!)

1. Mount the file as an image. In WinVICE, the easiest way is to use File > Attach cartridge image > Add to generic cartridge > 4/8/16KB cartridge at $2000.

1. Move the start-of-basic or limit-of-basic location to take BASIC completely out of the VIC-20 onboard memory. On a 3K expanded VIC, you can lower the limit of BASIC with the command **poke 56,16**.

1. Copy the contents from the ROM image to the built-in memory. Be sure to not copy the full 4K of the cartridge, or you'll overwrite your current video memory. This BASIC program works on a 3K-expanded VIC:

```
10 FOR I=0 TO 3071
20 POKE 4096+I,PEEK(8192+I)
30 NEXT I
```

5. Switch the location of the character table (byte 36869), while also changing the row number (byte 36867). You must do both of these and clear the screen in a single command, or you won't be able to see to type! The command is:

```
POKE 36867,23:POKE 36869,252:PRINT CHR$(147)
```

You should now be seeing the double-height characters.

As of the writing of this, only part of the character page has been created, meaning only capital letters, numbers, and some punctuation work, and there is no cursor. These will be added later. Note that the Shift+Commodore-key key combination no longer works properly, because the character table is now doubled in size- you will end up shifting halfway through the character table instead. Since the arrangement of the character tables is standard-lowercase-inverse standard-inverse lowercase, switching to inverse will give you the lowercase character table.

All of these characters are HAND-CODED, using a spreadsheet program, and thus are an original work. No data from the factory 8x8 font was used.
