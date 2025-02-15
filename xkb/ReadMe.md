
This is just a modified /usr/share/X11/xkb/symbols/us from Ubuntu 24-04.

You can see the changes I made on it in the Git history or diff it with the same file installed on your computer. 
Since the changes are very small and work well with all keyboards, I just overrode the packaged US ext intl layout, instead of creating a separate layout as in Windows.

To use, just do

    diff -ub symbols_us /usr/share/X11/xkb/symbols/us
    # and if you approve of the changes:
    sudo cp symbols_us /usr/share/X11/xkb/symbols/us
