# us-de-extended-layout
A keyboard layout that mixes the best of US extended international layout with to make it more usable for German language. 
It's particularly designed for split ergo keyboards that have fewer keys for all the punctuation characters available.

Since almost all mappings from the original US int'l layout are kept in place, this layout can be used for many different languages,
including English and German.

## Motivation 

A full traditional PC keyboard has 11 keys for punctuation,
while a 4×6 split keyboard (two hands, four rows, six columns per hand, giving 48 keys plus thumb keys) has around 5 keys for punctuation,
depending on how Escape, Tab, Enter, Backspace, Shift and other modifiers are mapped.
The usual solution is to make those punctuation keys accessible using an extra layer that is mapped in keyboard firmware,
instead of the software layout. 
Since the Firmware programming in the keyboard usually doesn't change the behavior of the Shift key, 
it is limited to just mapping pairs of characters (base character and shift character of each key).

This layout makes some sensible adjustment to the Shift layer (see below)
while at the same time making sure that all characters of the extended layout are still accessible to be mapped.
 
So this layout is not optimized to be used directly with a standard non-programmable keyboard, 
but it's optimized to give more programming freedom to the programmable keyboards.

Long explanation here: https://docs.google.com/document/d/1OiI-ya_XjVfk-rus44CFxOqT6734LNw9ImftXiJKImw/edit?usp=sharing

In case where the word "layout" is ambiguous, I am using the following terms:
 - Software layout -- the layout defined in the operating system, 
   defined using KLC for Windows, xkb for Linux, and something similar for macOS.
   This maps the standardized key "scan" codes to characters.
 - Firmware layout -- this tells the keyboard which key code to send to the operating system.
   Programmable keyboards can send different key codes from the same key, depending on their internal keyboard layers.
   Crucially, the operating system doesn't know about the keyboard layers, 
   and the keyboard can't know which characters will actually be produced by the key codes it sends.
 - Total Layout -- this is my own term for the result of all the other layouts: 
   which character you actually get out of a key.

To make this all more confusing, the scan codes will also be transformed according to different mappings.
It seems that Windows and Linux keyboard mappings are defined in terms of scan codes 
which more or less number the keys by their physical position on the old typewriter keyboard, 
where codes where standardized for the IBM PC AT, or least they are quoted as such in the USB standard.
USB in turn, numbers the keys semantically by their US querty layout meaning.

Here is a list of USB keycodes mapped to the old IBM ones: https://www.toomanyatoms.com/computer/usb_keyboard_codes.html

So if you are ever making a custom firmware that works together with a custom software layout, 
debugging can be very confusing as keys get mapped to letter codes, then scan codes, then letters again.
This layout try to make it easier to have most of the letter mapping logic in the keyboard firmware, 
by leaving most of the mappings as they are in the standard.
This allows you to map any language or layouts like Colemak, qwerty-flip, or my [Gemütliches Layout] 
in your (hopefully) comfortable firmware mapping tool.

[Gemütliches Layout]: https://github.com/matey-jack/gemuetliche-tastatur


## Solution

The main differences to US ext int'l are:
 - Since many split ergo layouts collect all types of brackets/parentheses/braces onto a separate layer (called AltGr, symbols, raise, lower or similar),
   we remove () and <> from the Shift layer to use the room for other punctuation that is used in typing of English texts:
   - Shift , and . become ; and : as in the German layout, so that the US ;: key can be omitted from the base layer.
   - Shift 9 and 0 become + and ? so that both the =+ and /? keys can be omitted from the base layer. 
     In my layouts I map = on a layer and key close to < and >, so that it is easy to type <= and >= .
     I also map / to this layer.
 - US ext int'l has apostrophe and quotation marks as dead keys, needing to type an extra space key to get the base character. 
   Since especially the apostrophe is used so often in English, I moved the dead key functionality and make it behave like ordinary US ANSI.
   The dead-key mapping tables are preserved in the AltGr and Shift+AltGr layer of the same key.
   The can be used directly or mapped in keyboard firmware to any other key. 
 - Finally, since my own 4×6 layout omits the =+ key from the base layer, I also changed the '" key to produced the VK_PLUS keycode.
   This allows Ctrl+' to stand in for Ctrl++, avoiding any interference with mappings of Ctrl+9 or Shift+Ctrl+9 that any application might have.

Example (total) layout for Iris CE and Ergodox keyboards which uses this (software) layout is described here:
https://docs.google.com/spreadsheets/d/1JkIiKLAgzVKIijrSS0zbML-NLrd7E52zQ_xwXzjz3oQ/edit?usp=sharing

And implemented here: https://configure.zsa.io/ergodox-ez-st/layouts/MWA4J/7avvp/0

## Usage

To ease programming the keyboard firmware this layout changes as little character positions from the original US ext int'l layout.
This allows the keyboard tools like Oryx and VIA to map keys using the standardized key labels. 
For example, in Oryx, go to settings (gear icon on the right), then choose "international", 
then scroll to the bottom and enable "US - international keycodes". That's it!
Now when you click on a key to edit it, you will have characters like öäüß, æøå, and more available.

For the characters that have changed mapping in this layout, you can access them in the following way:
 - for < and > select , and . and click on "right Alt" as additional modifier in the mapping.
 - for ( and ) same process, but with 9 and 0
 - additionally ;: and /? and += are still available for mapping normally, despite having new positions on the Shift layer,
   since they are positioned on keys which many split-ergo layouts don't map to the base layer.
   They are basically in spare parts bin. :-)


