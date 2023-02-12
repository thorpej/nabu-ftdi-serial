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

This board is 99.9% the work of Kris Sekula (MyGeekyHobby.com).  All I did
was add the hardware flow control modification.  Kudos to Kris for publishing
his idea [here](https://github.com/Kris-Sekula/NABU/tree/main/RS422Alternative).
