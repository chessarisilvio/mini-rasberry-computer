mini-raspberry-computer
A simple adapter PCB for connecting a 4" touchscreen to a Raspberry Pi

i was tired of dealing with messy jumper wires when i connected my raspberry with my screen, this is just a small PCB that sits between your Raspberry Pi 3B+ and a 4-inch touchscreen. Plug and play, basically.

What you need
Raspberry Pi 3B+ (I already have one)

4" TFT display (ILI9488 chip, around $18 on AliExpress)

This custom PCB (about $5 from JLCPCB for 5 boards)

The display is 480x320 resolution with resistive touch. Good enough for dashboards or simple control panels.

Building it
Order the PCB from JLCPCB using the Gerber files in the repo. Standard 2-layer board, nothing fancy. When it arrives, just stack everything together - Pi goes on the bottom, PCB in the middle, display on top. Takes like 10 minutes.

Software
Enable SPI in raspi-config, then install the fbcp-ili9341 driver. It's all in the repo. The board uses GPIO 24 and 25 for display control. Boot it up and you're done.

If the screen's black, check if SPI is enabled. If touch isn't working, run dmesg | grep touch to see what's wrong.

Files
Everything's MIT licensed. KiCad files are included if you want to modify it. Made in KiCad 9 with FreeRouting. Pull requests welcome if you improve anything.
