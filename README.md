# CrFrecon
I ported chromeOS frecon to linux (standard linux, that is)

# Build

Clone the repository (no duh)
`git clone https://github.com/nytr1xx/CrFrecon/`

Go into the directory (duh)
`cd CrFrecon # or whatever path CrFrecon was copied into`

Build it!
'gcc -std=c99 -D_GNU_SOURCE=1 -DFRECON_LITE=1 -I. main.c dev_lite.c dbus_lite.c drm.c fb.c font.c image.c input.c shl_pty.c splash.c term.c util.c $(pkg-config --cflags --libs libdrm libpng libtsm) -o frecon-lite'
