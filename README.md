# nabu-ftdi-serial
A serial interposer board for NABU PCs with a FTDI USB-serial adapter and
hardware flow control

This is a simple serial interposer board for NABU PCs that intercepts
the Tx and Rx signals from the TR1863 UART and routes them to an FTDI
USB-serial adapter rather than to the RS422 line drivers on the NABU
main board.

In addition to intercepting the Tx and Rx signals, it also provides two
enhancements:

* The option to use a 1.8432MHz oscillator to generate a 115.2K baud
  rate on the UART, rather than the stock 111.8K baud that the NABU's
  clock generates.  Two different oscillator footprints are provided,
  for your convenience.  A jumper is provided to select the clock source.

* The option to enable hardware flow control.  This is done by connecting
  the TR1863's _DR_ signal (Data Received) to the _CTS_ input on the FTDI.
  Because _DR_ is active-high and _CTS_ is active-low, a pending receive
  interrupt effectively de-asserts _CTS_, which will cause the sender to
  pause transmitting until the interrupt has been serviced.

To build this board you're oging to need an FTDI USB -> serial interface
chip mounted on some sort of break-out board.  The board provides 2
footprints to provide some flexibility.

The first footprint is for a 6-pin right-angle pin header that is meant
for an Adafruit 6-pin female FTDI connector.  Such a connector can be
found on the [Adafruit FTDI Friend](https://www.adafruit.com/product/284),
the [Adafruit FTDI Serial TTL-232 Cable](https://www.adafruit.com/product/70),
or the [Adafruit FTDI Serial TTL-232 USB Type C 5V Cable](https://www.adafruit.com/product/4364).
There are other cables out there with a compatible 6-pin connector,
but I specifically referenced the pin configuration of the Adafruit
products.

The other option is one of the FTDI FT232RL boards that are all over
Ali Express.  I ordered [this one](https://www.aliexpress.us/item/2251832463833524.html),
but there are lots of identical boards floating around.

This board is 99.9% the work of Kris Sekula (MyGeekyHobby.com).  All I did
was add the hardware flow control modification.  Kudos to Kris for publishing
his idea [here](https://github.com/Kris-Sekula/NABU/tree/main/RS422Alternative).

