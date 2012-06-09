This is a simple Open Hardware peripheral for the OLPC XO-1/1.5/1.75.

The files are created using Eagle 5.10.0 on Linux, and the SparkFun
footprint libraries.

Some details about the design:

1) Supporting using either the ATtiny85 (lowest cost) or the ATtiny261
   (14 I/Os, $0.12 more expensive).
2) Based on the Sparkfun AVR Stick
    http://www.sparkfun.com/products/9147
   and thus software will be based on
    http://www.obdev.at/vusb/
3) The PCB we're working with is 0.8mm (0.031"); a USB plug "is supposed to be
   2.4mm (0.093") but you can get away with 1.6mm (0.062")" (thanks, djgpp)
   Our solution is to put two breakaway tabs on the back of the board.  You
   can break them off and glue them below the USB fingers to make it stay in
   the port better/at all.  One gotcha is that break away PCBs tend to stress
   nearly traces; I've tried to give them adequate clearance.  We're also
   putting copper fills on the PCBs to make them thicker (thanks again, djgpp).
4) Attempting to bring BOM below $1/student and part count down as low as
   possible as well.  As a result, we're skimping a bit on ferrites and
   bypass caps.
5) There are pads for populating a full-size USB-B connector, so you can
   put this on a cable (and avoid the glue-the-PCBs-together dance).
   Full size USB-B through hole connectors seem to be the sweet spot for
   cost, but this means you need a different cable for the XO Stick and the
   XOrduino (which needs to use a mini or micro connector to save PCB space).
   Also, the USB signals will be exposed on the tabs when the connector
   is populated.  Maybe some different trade-offs need to be made here.
6) The XO Stick needs an external programmer.
   a) Can we write a USB DFU bootloader using v-usb?  The chip has the
      hardware for self-programming, dunno about code space.
   b) Using one XO Stick to program another is a Simple Matter Of Software.
      We should define a standard for the hardware hookup.
   c) The XOrduino should be able to program XO Sticks as well.
   d) Maybe a little bit of extra PCB space to support (b) and/or (c) is
      called for?  Pads for a male ICSP programming cable, for example?

  -- C. Scott Ananian, 2012-06-09
