# us-de-extended-layout

This repository contains several modifications of the "US extended international" keyboard layout that serve as 
"support" layouts for programmable keyboards.

The main advantages of such a "support" layout are:
 - includes characters like '–' (n-dash) which otherwise wouldn't be available at all
 - smooth out differences in Windows and Linux implementation of the US ext int'l layout (which is not standardized)
 - make it easier to type standard ' and " (especially on Windows)
 - modify the Shift layer characters to optimize for split ergonomic keyboards with less than 72 keys. 

The Shift-layer mapping uses a mix of standard US and DE (German) keyboards. 
Anyone not used to a German keyboard will probably not use this layout directly, but rather use it as an inspiration to create their own.
But since all characters can be typed and all letters and most basic punctuation is compatible with the US layout,
you could try this out with your custom keyboard Firmware before deciding if you want to spend the time 
for creating your own "support" layout for your "bespoke" keyboard firmware.

To clarify: 
 - a "support" keyboard layout is a software layout meant to be used with a programmable keyboard. 
   The layout doesn't need to map all the keys in all the right places, but it needs to make sure that all needed characters are available,
   and the Shift-layer mappings make sense.
 - a "bespoke" keyboard firmware is one that works best in combination with such a support layout.
 - (When making the above layouts, we can do it in way that minimizes changes, so that our keyboards (and computers) are
   still usable when the support layout (or the bespoke firmware) is not present. But the main use-case is for both together.)

## Motivation 

A full traditional PC keyboard has 11 keys for punctuation characters (in addition to 10 punctuation characters on shift+number).
A 4×6 split keyboard (two hands, four rows, six columns per hand, giving 48 keys plus thumb keys) has around 5 keys for punctuation,
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
where codes were standardized for the IBM PC AT, or least they are quoted as such in the USB standard.
USB in turn, numbers the keys semantically by their US qwerty layout meaning.
(Which in turn becomes meaningless when attaching a non-qwerty keyboard.)

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

(I am not using those exact same any more, but very similar evolutions of them.)

## Shift layer mapping for number row

On a "traditional" (IBM compatible) keyboard, there are 13 keys in the number row.
Split keyboards (like the MS Ergonomic keyboard line) usually split the number row between the digits 6 and 7.
(And so does the Colemak Wide mod and also my own "split layout" for traditional keyboards).

With a US layout it looks like this (using Colemak Wide mod):

    ´~  1!  2@  3#  4$  5%  6^      =+  7&  8*  9(  0)  -_  (⌫)

And the DE (German) layout is like this (using my Gemütliches Layout wide mod):

    ^°  1!  2"  3§  4$  5%  6&      ´`  7/  8(  9)  0=  ß?  (⌫)

On the US standard layout '/' is available on the main (letters) area of the keyboard,
while on the DE standard layout '-' takes its place.
On my split keyboard layouts, I have mapped the letter 'e' to a thumb key, thus liberating a spot in the main letter area,
so both important punctuation keys / and - can be placed there.

On my Ergodox the number row is mapped like this:

    ESC  1!  2@  3#  4$  5%  6^      ´`  7&  8*  9+  0=  ß?  (⌫)

As you can see, it preserves some muscle memory from both traditional layouts!
Accents ^° are mapped on a higher layer, all on the strong fingers of the left hand,
memorably those are the same fingers that type <> on the standard US layout and () on the DE layout.

For the Iris, we have two keys less and map like this:

        ESC  1!  2@  3#  4$  5%      6+  7&  8*  9=  0?  (⌫)

Now, also ^ß´` move to a higher layer, but their keys are close to their original position, preserving that part of muscle memory.

All the layouts in this repository have the shift mapping for this last (Iris) variant,
because a width of 6 keys is much more common with custom ergo split keyboards.
All the layouts also have the standard German shift pairing of .; and ,; keys, so that the US ;: key doesn't need to be mapped.
(And <> are to be mapped with all the other parenthesis.)

While my firmware layouts all have a layer called AltGr, this historically contained a lot of key mappings from the DE layout AltGr layer,
this is still a completely mapped-in-firmware layer and the AltGr layer of the software layouts in this repository serve merely as the "support"
to make characters available for mapping.


## Usage

To ease programming the keyboard firmware this layout changes as little character positions from the original US ext int'l layout.
This allows the keyboard tools like Oryx and VIA to map keys using the standardized key labels. 
For example, in Oryx, go to settings (gear icon on the right), then choose "international", 
then scroll to the bottom and enable "US - international keycodes". That's it!
Now when you click on a key to edit it, you will have characters like öäüß, æøå, and more available.

The same works when adding a layout in the QMK sources directly. 
You can `#include "keymap_us_international_linux.h"` to get mappable keycodes that haven't changed from US ext int'l.
For ease of mapping, the redundant ;: and =+ keys are still present in the layout, so that no extra keycodes need to be defined for them.

For the ones that were overwritten in the layout, you can use some custom keycodes 
[following my example](https://github.com/matey-jack/qmk_firmware/blob/7ce8ea04d924c7919d17bef57e1b883b8af39c9e/keyboards/keebio/iris_ce/keymaps/asdr_nilt/us-ext-intl-mod.h).

TODO: link to full QMK example, once that is published.

## Variants

 - [US ext intl Iris full compatible.klc](windows-klc/US%20ext%20intl%20Iris%20full%20compatible.klc) is the one that I am currently using and that I'd recommend.
 - [US extended international more live keys.klc](windows-klc/US%20extended%20international%20more%20live%20keys.klc) is one that makes as little changes as possible.
   It's meant to be used together with [some additional logic in the firmware](https://github.com/matey-jack/qmk_firmware/commit/b4ac5ef75c565e3c6342b59f3c3731975a44f1ae)
   to swap some keys in the shift layer around.
   This has the advantage of making the layout usable even with a standard keyboard and also making the keyboard firmware useable with a standard computer.
   But since some keys have to be input in different ways, this is not worth it in most cases.
 - [US extended international for 48 keys.klc](windows-klc/US%20extended%20international%20for%2048%20keys.klc) old version, stays for historic reasons.
 - Note that there is no layout here, which has the shift-layer mapping for the Ergodox shown above. 
   I instead implemented that purely as a firmware layer.

The minimal variant (name "more live" keys) is the only one that I also made for Linux. 
As you can see in the diff/history of [symbols_us](xkb/symbols_us), this change is really minimal.
That's possible because the Windows variant contains a change to make the apostrophe behavior the same as Linux
the firmware layout relies on that.
