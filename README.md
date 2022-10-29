
# uncrx

Simple command-line tool to extract a zip file from a chrome extension file.


## About

This is standalone program with zero dependencies, and its purpose is to extract
CRX files (Chrome Extensions, Chrome Web Apps) from the Chrome Web Store back
into ZIP files.

Users that don't want to use Google Chrome and want to use the local `Developer Mode`
and `Unpacked Extensions` in order to not be tracked by Google will have to extract
the Extensions somewhere, and load it manually via `chrome://extensions`.

This can only be done once the 
, so that users of an Ungoogled Chromium Browser can also use the
official source of Extensions without having to build them from scratch all the
time :)

Note that Google changed their "Cr24" file format already twice, and all three
versions differ heavily.


## Example Usage

This example demonstrates how to download and extract [uBlock Origin](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm?hl=de)
from the Chrome Web Store, so that the ZIP file can be unpacked and the extension
can be loaded as an "Unpacked Extension" in Chromium and Ungoogled Chromium.

```bash
export EXTENSION_ID="cjpalhdlnbpafiamejdnhcphjbkeiagm";
export EXTENSION_NAME="ublock-origin";

wget -O "$EXTENSION_NAME.crx" "https://clients2.google.com/service/update2/crx?response=redirect&acceptformat=crx2,crx3&prodversion=100&x=id%3D$EXTENSION_ID%26uc";

uncrx "$EXTENSION_NAME.crx":                        # creates the $EXTENSION_NAME.zip file in the same folder
unzip "$EXTENSION_NAME.zip" -d "./$EXTENSION_NAME"; # unpack the extension, so that it can be loaded in Developer Mode
```

## File Format Support

This tool supports the following file formats:

- `CRX3` or "Cr24 / version 3" is currently in use by Chromium 100 or newer, and the Chrome Web Store.
- `CRX2` or "Cr24 / version 2" was previously used by Chromium 24 until around Chromium 100.
- `CRX1` was used until Chromium 23, and is a zip file without any signature headers.


## Similar Tools

- [crx-unpack](https://pypi.org/project/crx-unpack/), but only supports `Cr24 / version 2` encoded files.


## License

GPLv3

