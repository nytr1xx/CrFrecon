# CrFrecon

I ported chromeOS frecon to standard Linux. It's only been tested on Ubuntu 26.04 x86_64, so expect issues on other distros. I'll do more testing as time goes on

# What IS CrFrecon?

First off, FRECON (Freon Console) is Google's answer to virtual terminals (VTs) on chromeOS . Ever noticed on old chromebooks how on the "dead battery" screen, that you can type pixelated text in the top left corner despite the device being dead? Well, thats Frecon doing its job. (Skip the next paragraph if you don't care about chromeOS rendering)

When chromebooks die, they have a LITTLE bit of juice left in them. Just enough to boot into chromeOS's kernel. chromeOS realizes it has low battery, and changes the chromeOS boot logo to the low battery screen, before powering back off. See, Frecon renders images directly to the framebuffer, but its text input (at least on older versions of chromeOS) still remains as an artifact of Frecon, so you can type some text at a painfully slow speed before powers off again. 

CrFrecon directly ports Frecon to generic Linux, at least, Ubuntu. It most likely works on other distros but should be tested with caution.

# Build

Add the universe repository:

`sudo add-apt-repository universe`

Update your package lists:

`sudo apt update`

Install dependencies:

`sudo apt install build-essential pkg-config libdrm-dev libpng-dev libtsm-dev python3`

Clone the repository (no duh):  
  
`git clone https://github.com/nytr1xx/CrFrecon/`

Go into the directory (duh):  
  
`cd CrFrecon/frecon/ # or whatever path CrFrecon was copied into`

Generate the font headers:

`python3 font_to_c.py ter-u16n.bdf glyphs.h`

Build it!:  
  
`gcc -std=c99 -D_GNU_SOURCE=1 -DFRECON_LITE=1 -I. main.c dev_lite.c dbus_lite.c drm.c fb.c font.c image.c input.c shl_pty.c splash.c term.c util.c $(pkg-config --cflags --libs libdrm libpng libtsm) -o frecon-lite`

# Running Frecon

Switch to any unoccupied virtual terminal (eg. tty3) and run:

```cd CrFrecon/frecon/ # or wherever you cloned CrFrecon```   
```sudo ./frecon-lite --flags-go-here```

# Opening my test images :D

Keep in mind the commands here assume you are in CrFrecon/frecon/
Switch to your unoccupied virtual terminal and run:

`sudo ./frecon-lite --enable-vt1 --enable-osc --clear=0xFFFFFFFF --image=img/BootLogoOld.png # for the old chromeOS boot logo`
`sudo ./frecon-lite --enable-vt1 --enable-osc --clear=0x00000000 --image=img/BatteryDeadRecreation.png # for the dead battery screen`
`sudo ./frecon-lite --enable-vt1 --enable-osc --clear=0x000000FF --image=img/Surprise.png # you can find out`
