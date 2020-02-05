# do your own keyboard layout

**loadkb.sh** is a script that will create and load a keyboard layout based on **XKB** symbols definition. If no path to such a definition is passed, it will default to `symbols/budkb` in this directory. The symbols definition must be located in a directory called "**symols**" for this to work.  

## budkb - the default layout

Included in this repo is the layout budkb, a combination of symbols already installed on the system, and two custom ones. The base layout is **se(us)**, which is US layout with added Swedish (`åäö`) characters on the **Third Layer**. This is the layout I personally use, probably not what (you) want, but I leave it here for reference.

*symbols/budkb*  
```
default alphanumeric_keys modifier_keys
xkb_symbols "base" {

    include "typo"
    include "se(us)"
    include "eurosign(e)"
    include "level3(lsgt_switch)"
    include "caps_esc_ctrl"
    include "hjkl-like-vi"
};
```

The `include` statements works like this: FILE(TYPE) . Where FILE is a file either in: `/usr/share/X11/xkb/symbols/` or in `symbols/` in this directory or the same directory as the file you passed as an argument. Some files have multiple types declared, so the word in parenthesis specifies which to include. If no type is specified the default one or the one with the same name as the file will get chosen.

*/usr/share/X11/xkb/symbols/eurosign*
```
// Most keyboards have the EuroSign engraved on the E key
partial
xkb_symbols "e" {
    key <AD03>    { [  NoSymbol,   NoSymbol,   EuroSign,    NoSymbol ]    };
};

// Many Apple keyboards have the EuroSign engraved on the 2 key
partial
xkb_symbols "2" {
    key <AE02>    { [  NoSymbol,   NoSymbol,   EuroSign,    NoSymbol ]    };
};
...
```

*symbols/caps_esc_ctrl*
```
hidden partial modifier_keys
xkb_symbols "caps_esc_ctrl" {
    replace key <CAPS> {
        type[Group1] = "ONE_LEVEL",
        symbols[Group1] = [ Escape ],
        actions[Group1] = [ SetMods(modifiers=Control) ]
    };
    modifier_map Control { <CAPS> };
};
```

## links

https://www.charvolant.org/doug/xkb/html/xkb.html  
https://unix.stackexchange.com/a/506185  
https://askubuntu.com/q/1044474  
https://github.com/sebastiw/keyboard-layout  
