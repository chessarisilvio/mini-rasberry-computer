mini-raspberry-computer
Building a compact Raspberry Pi computer with a touchscreen display

Ever wanted to hook up a touchscreen to your Raspberry Pi but ended up with a bird's nest of jumper wires? Yeah, me too. It works, but it's ugly and falls apart if you look at it wrong. This adapter is basically just a small PCB that sits between your Raspberry Pi and a 4-inch touchscreen, The board is about credit card sized and plugs directly into the Pi's GPIO header. On the other side, there's a connector for the display.

What You're Getting Into
you need a Raspberry Pi 3B+ kit (the one with the power supply and SD card), a 4-inch display with the ILI9488 chip, and this custom PCB. The whole thing runs about a hundred bucks if you shop on AliExpress. The display is resistive touch, which means stylus or finger both work fine. Resolution is 480x320—not amazing but good enough for dashboards, small games, or control panels.

I use this setup for a home automation controller in my kitchen. It's running 24/7 and hasn't given me problems. Screen size is perfect when you just need to tap a few buttons or check some sensors.

Making the PCB
Order the boards from JLCPCB or wherever. They'll want the Gerber files (they're in the repo), and you pick standard options—2 layers, 1.6mm thick, green solder mask unless you want to pay extra for black or whatever. Minimum order is 5 boards for like two bucks, so you'll have spares. Takes about two weeks to show up.

When the package arrives, the connectors should already be soldered on if you ordered assembly, Push the Pi onto the board, screw in some standoffs, plug the display on top. Ten minutes and you're done. The mounting holes line up with the Pi's holes, so everything stays put.

Software Side
Getting it working is the usual Raspberry Pi stuff. Boot it up, enable SPI in raspi-config (it's under Interface Options), reboot. Then you compile the display driver, which sounds scarier than it is. The fbcp-ili9341 driver is what you want—it mirrors whatever's on your normal screen to the little display.

Configuration is mostly just telling it which GPIO pins to use. This board uses GPIO 25 and 24 for the display control lines. SPI clock divisor starts at 6 but you can tweak it if things look weird. Driver takes maybe 5 minutes to compile on the Pi.

Touch calibration is optional. If you're just tapping buttons it doesn't matter much. For drawing or precise stuff, run xinput-calibrator and follow the dots.

When Things Go Wrong
Black screen after boot usually means SPI isn't enabled or the driver crashed. Check systemctl status fbcp to see what's up.
Touch not working is either a driver problem. Run dmesg | grep touch and see if there are errors. Usually it's just a typo in the config file.

The Files
Everything's MIT licensed—do whatever you want with it. KiCad project files are there if you want to modify the board. All the Gerbers are ready to upload. There's a bill of materials with AliExpress links that were current when I made this (prices probably changed by now).

If you improve something or make it work with a different display, send a pull request. I'd especially like to see someone design a 3D-printed case for this thing. I've been using it bare-board and it's fine, but a case would be nice.

Built this in KiCad 9 and used FreeRouting because I'm lazy and didn't want to route all those traces by hand. Passed all the design rule checks before ordering, so the boards came out good.

Total cost about $100. Assembly takes 10 minutes. Works great for small displays and control panels.
