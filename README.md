This is a simple Open Hardware peripheral for the OLPC XO-1/1.5/1.75/4.

The files are created using Eagle 6.2.0 on Linux and the SparkFun
footprint libraries.

Some details about the design:

1. Supporting using either the ATtiny85 (lowest cost) or the ATtiny861
   (14 I/Os, slightly more expensive).
2. Based on the Sparkfun AVR Stick
    http://www.sparkfun.com/products/9147
   and thus software will be based on
    http://www.obdev.at/vusb/
   Note that the USB port has been moved to PB3/4 so software for the
   SparkFun AVR Stick will not work without modification.
3. The PCB we're working with is 0.8mm (0.031"); a USB plug "is supposed to be
   2.4mm (0.093") but you can get away with 1.6mm (0.062")" (thanks, djgpp)
   Our solution is to put two breakaway tabs on the back of the board.  You
   can break them off and glue them below the USB fingers to make it stay in
   the port better/at all.  One gotcha is that break away PCBs tend to stress
   nearby traces; I've tried to give them adequate clearance.  We're also
   putting copper fills on the PCBs to make them thicker (thanks again, djgpp).
   The PCB we have also has 4 layers, but I've routed this board with only
   the top and bottom so that 2 layer reproductions will work just fine as
   well.  The inner two layers are ground and power planes, which don't
   need to be present to connect the ground and power nets.
4. I'm attempting to bring BOM below $1/student and part count down as low as
   possible as well.  As a result, we're skimping a bit on ferrites and
   bypass caps.
5. There are pads for populating a mini USB B connector, so you can
   put this on a cable (and avoid the glue-the-PCBs-together dance).
6. The XO Stick has a standard arduino shield pinout.  This lets it be
   piggybacked on another XO Stick for programming, or piggy backed on
   an XOrduino to control a turtle robot.  Standard arduino shields will
   probably *not* work, since not all pins are connected -- but they might!
7. To program one XO Stick from an XOrduino, the RST header on the
   target should be put in the "PROG" position so that the programmer
   can drive it via arduino pin 0.  To program an XO Stick from another
   XO Stick, both RST headers should be in the "NORM" position, and
   the programmer needs to have the RSTDISBL fuse programmed, so that it
   can use PB5 ('85) or PB7 ('861) as an output.  Note that once RSTDISBL
   is programmed, the device can't be programmed using the ICSP port
   until RSTDISBL is unprogrammed using the high-voltage programming method.
8. The XO Stick currently needs an external programmer.
   Can we write a USB DFU bootloader using v-usb?
   Something like:

        http://www.obdev.at/products/vusb/usbasploader.html
        http://embedded-creations.com/projects/attiny85-usb-bootloader-overview/
        https://github.com/embedded-creations/USBaspLoader-tiny85

  -- C. Scott Ananian, 2012-06-09; revised 2012-07-30, 2012-08-08
