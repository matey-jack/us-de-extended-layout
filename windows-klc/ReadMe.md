Main files in this folder:
 - [usintl48](usintl48) -- this folder contains the compiled layout (described in main ReadMe) that you can install in Windows.
 - [US extended international for 48 keys.klc](US%20extended%20international%20for%2048%20keys.klc) -- source code for the layout.
   You can load it into MS Keyboard Layout Creator and compile it yourself to the installable layout.
 - TODO: base layout for Iris Split keyboard

Some additional files in this folder:
 - [US extended international.klc](US%20extended%20international.klc) -- layout saved from the Windows onboard "US extended international".
  This is the basis for the custom layout, and you diff the files to see what exactly I modified.
 - [DE ext 1.klc](DE%20ext%201.klc) -- layout saved from the Windows onboard "Deutsch (erweitert 1)". 
   Only here for reference to check how things are done in this layout.
 - [US ANSI German.klc](US%20ANSI%20German.klc) -- experiment trying to get to a similar layout as the intl48, 
   but putting German Umlauts on the base layer instead leaving them on their existing AltGr positions.
   This layout looks more like the total result that I want to get (when combined with keyboard firmware layout),
   but it has the drawback that the firmware is harder to program, as we can't use standard key labels as a reference.

Changes that Iris needs:
 - ;: swap with <>   actually swap both ways, so that the firmware will have a fallback when only US standard layout is active.
 - Shift+690 becomes +=?
 - ^() move to AltGr layer of their original keys
 - Shift+/ becomes \
 - add n-dash on - key
 - '" become live characters and the corresponding dead accents move to AltGr layers
 - add a live ` and ~ in some convenient place on AltGr layer
 - OEM_PLUS keycode mapped to '" to be on base layer and that's the only key with no significant keycode assigned already.

In "fallback mode" keys will be available as follows:
 - ;: and <> simply swap layers
 - ()? directly in their US position Shift+90/
 - = in our alternate mapping AltGr+M, and + on same with additional Shift.
 - \ needs an alternate mapping defined in Firmware
 - '" will need additional 'space' to be pressed in US int'l layout, but will just work in US ANSI layout.

Note that for alternate mappings to work in both modified and standard layouts, 
the characters += \| need to stay on their original keys in addition to being mapped onto new Shift-layer positions.
For characters that swap with other mapped characters, we don't need to do that.
