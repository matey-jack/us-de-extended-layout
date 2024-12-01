æ	ø# us-de-extended-layout
A keyboard layout that mixes the best of US extended international layout with to make it more usable for German language. 
It´s particularly designed for split ergo keyboards that have less keys for all the punctuation characters.

Since almost all mappings from the original US int´l layout are kept in place, this layout can be used for many different languages,
including English and German.

## Motivation 

A full traditional PC keyboard has 11 keys for punctuation,
while a 4×6 split keyboard (two hands, four rows, six columns per hand, giving 48 keys plus thumb keys) has around 5 keys for punctuation,
depending on how Escape, Tab, Enter, Backspace, Shift and other modifiers are mapped.
The usual solution is to make those punctuation keys accessible using an extra layer that is mapped in keyboard firmware,
instead of the software layout. 
Since the Firmware programming in the keyboard usually doesn´t change the behavior of the Shift key, 
it is limited to just mapping pairs of characters (base character and shift character of each key).

This layout makes some sensible adjustment to the Shift layer (see below)
while at the same time making sure that all characters of the extended layout are still accessible to be mapped.
 
So this layout is not optimized to be used directly with a standard non-programmable keyboard, 
but it´s optimized to give more programming freedom to the programmable keyboards.


## Solution

The main differences to US ext int´l are:
 - Since many split ergo layouts collect all types of brackets/parentheses/braces onto a separate layer (called AltGr, symbols, raise, lower or similar),
   we remove () and <> from the Shift layer to use the room for other punctuation that is used in typing of English texts:
   - Shift , and . become ; and : as in the German layout, so that the US ;: key can be omitted from the base layer.
   - Shift 9 and 0 become + and ? so that both the =+ and /? keys can be omitted from the base layer. 
     In my layouts I map = on a layer and key close to < and >, so that it is easy to type <= and >= .
     I also map / to this layer.
 - US ext int´l has apostrophe and quotation marks as dead keys, needing to type an extra space key to get the base character. 
   Since especially the apostrophe is used so often in English, I removed the dead key functionality and make it behave like ordinary US ANSI.
   Currently, the dead-key mapping tables are removed from the layout, but they can be brought back in a later version if anyone needs them. 
 - Finally, since my own 4×6 layout omits the =+ key from the base layer, I also changed the ´¨ key to produced the VK_PLUS keycode.
   This should allow Ctrl+´ to stand in for Ctrl++ which probably wouldn´t work when pressing Ctrl+Shift+9.


## Usage

To ease programming the keyboard firmware this layout changes as little character positions from the original US ext int´l layout.
This allows the keyboard tools like Oryx and VIA to map keys using the standardized key labels. 
For example, in Oryx, go to settings (gear icon on the right), then choose ¨international¨, 
then scroll to the bottom and enable ¨US - international keycodes¨. That´s it!
Now when you click on a key to edit it, you will have characters like öäüß, æøå, and more available.

For the characters that have changed mapping in this layout, you can access them in the following way:
 - for < and > select , and . and click on ¨right Alt¨ as additional modifier in the mapping.
 - for ( and ) same process, but with 9 and 0
 - additionally ;: and /? and += are still available for mapping normally, despite having new positions on the Shift layer,
   since they are positioned on keys which many split-ergo layouts don´t map to the base layer.
   They are basically in spare parts bin. :-)


