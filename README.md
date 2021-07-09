# Dead key-less ISO keyboard layouts for Windows

Windows does not provide dead key-less variants for keyboard layouts that
feature dead keys. This can make typing characters like `` ` `` and `~`
irritating, especially in languages that rarely need the diacritics.

If you have administrator rights, you can make and install your own keyboard
layouts using [Microsoft Keyboard Layout Creator][url-msklc].

Here are some indiscriminately dead key-less regional keyboard layout variants.
All of them are...

- ISO physical layouts (11 keys between _Shift_ keys)...
- ... based on the regional input methods built into Windows...
- ... with every single dead key turned into a regular key.

If your desired region is not here, you're welcome to provide or request it,
but it must follow the rules above. If you want only some of the dead keys in
your input method disabled your use case is a bad fit. If you're looking for
even more sophisticated functionality than provided here, look into
[EPKL][url-epkl].

## Instructions

Whether you want to use one of these layouts or make your own layout you have
to first install and run Microsoft Keyboard Layout Creator ("MSKLC").

### Use an existing layout

1. In MSKLC, open the `.klc` file representing the layout you want to use
2. Choose _Project_ > _Build DLL and Setup Package_.
3. Choose _Yes_ to open the output directory.
4. Run `setup.exe` located in the output directory to install the layout.
5. Open Windows' _Language settings_ and select the _Keyboard_ section.
6. Select the new layout from the drop-down.

### Create a new layout

1. In MSKLC, choose _Load Existing Keyboard..._ from the _File_ menu item.
2. Locate the desired base layout.
3. Right-click every light grey key in every shift state and remove the
   checkmark next to _Set as dead key_.
4. Choose _Properties_ in the _Project_ menu item and fill out the information.
5. Choose _Save Source File As..._ in the _File_ menu item and save the file..
6. Reencode the `.klc` file from UTF-16LE to UTF-8.

MSKLC writes the `.klc` file as UTF-16LE with BOM and mixed line endings. It
should be normalized to UTF-8 without BOM and CRLF (not LF); this can be
accomplished with

```sh
for f in mylayout.klc
do
    iconv -f UTF-16 -t UTF-8 $f > x && mv x $f
done
```

## Notes

- Uninstallation works somewhere between poorly and not.
- The output directory is placed in the current user's _Documents_ directory by
  default.

## See also

- https://msklc-guide.github.io/
- https://zauner.nllk.net/post/0014-windows-no-dead-keys/

[url-dead-key]: https://en.wikipedia.org/wiki/Dead_key "Wikipedia: dead key"
[url-epkl]: https://github.com/DreymaR/BigBagKbdTrixPKL "DreymaR's Big Bag of Keyboard Tricks for EPKL"
[url-msklc]: https://www.microsoft.com/en-us/download/details.aspx?id=102134 "Download MSKLC"
