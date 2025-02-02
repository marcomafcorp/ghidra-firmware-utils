Ghidra Firmware Utilities
=========================

Various modules for [Ghidra][1] to assist with PC firmware reverse-engineering.
This was accepted as a [coreboot project][2] for GSoC 2019.

## Features (very much WIP)
### PCI option ROM loader
 - Implements a FS loader for PCI option ROMs (handles hybrid ROMs,
   e.g. legacy x86 + UEFI)
 - Loads UEFI executables from PCI option ROMs (including compressed images)
 - Calculates entry point address for legacy x86 option ROMs (still needs to be
   manually loaded as a raw real-mode binary)
 - TODO: Write loader for legacy x86 option ROMs (automatically select
   real-mode x86)

## Planned functionality / TODO
### Firmware image loader
 - Implement FS loader for firmware images
 - Write parsers for Intel IFD (BIOS region), coreboot CBFS/FMAP, and UEFI
   firmware volumes

### UEFI loader
 - Write helper script to import GUIDs/etc (similar to [ida-efitools][3])

## Building & Installation

Ghidra's standard Gradle build system is used. Set the `GHIDRA_INSTALL_DIR`
environment variable before building:

```bash
$ export GHIDRA_INSTALL_DIR="/path/to/ghidra"
$ gradle
```

The module ZIP will be output to `dist/`. Use **File > Install Extensions** and
select the green plus to browse to the extension. Restart Ghidra when prompted.

## Usage
### PCI option ROM loader
Add a PCI option ROM to a Ghidra project. When prompted to select an import
mode, select **File system**. The images contained within the option ROM will
be displayed, and can be imported for analysis. Information for each image can
be displayed by selecting **Get Info** in the right-click menu for an image.

## License
Apache 2.0, with some exceptions:

 - `src/efidecompress/c/efidecompress.c`: BSD

## Credits
`src/efidecompress/c/efidecompress.c` is a lightly modified version of
[Decompress.c][4] from uefi-firmware-parser (which itself is derived from
[the original in EDK2 BaseTools][5]).

[1]: https://ghidra-sre.org/
[2]: https://summerofcode.withgoogle.com/projects/#6413737605464064
[3]: https://github.com/danse-macabre/ida-efitools
[4]: https://github.com/theopolis/uefi-firmware-parser/blob/21106baf019db9dcd046a3c01ee7b32212de45a5/uefi_firmware/compression/Tiano/Decompress.c
[5]: https://github.com/tianocore/edk2/blob/2e351cbe8e190271b3716284fc1076551d005472/BaseTools/Source/C/Common/Decompress.c
