
## Summary

This project is an SOC (System on a Chip) coded in VHDL and implemented for the Lattice iCE40-hx8k dev board. The SOC contains the following components: PDP-8 CPU + RAM + UART + Timer + I/O Ports

## Required Hardware

* Lattice iCE40-hx8k dev board (can be ordered online at www.latticesemi.com)
* USB-to-Serial 3.3V adapter (can be ordered from eBay)
* misc USB cables and wires for connecting the USB-to-Serial adapter

NOTE: Make sure the USB-to-serial adapter is a 3.3V version. Some adapters have 5V interface signals which could damage your iCE40-hx8k dev board.

## Tools

* IceCube2 (from Lattice Semiconductor) was used for synthesis and FPGA Routing.
* Icestorm (https:/github.com/cliffordwolf/icestorm) was used for programming.


## Build Flow

I used the Lattice IceCube2 software to generate the SOC_bitmap.bin programming file and then I used this command line "iceprog SOC_bitmap.bin" the program the iCE40-hx8k dev board over the USB cable (iceprog is part of the icestorm tool suite).

## Console Interface

I used the minicom program (on Ubuntu Linux) as a console to communicate with the SOC over the USB-to-Serial connection. Configure minicom using the command line "minicom -s" to configure the serial port for ttyUSB0 and turn of the hardware handshaking. There are probably other alternatives to minicom. Any ANSI terminal-emulator program should work for this application.

## Pinout

The iCE40 pins are defined as follows:
```
UART_RXD   G1 -pullup yes
UART_TXD   G2
PORTA[0]   B5
PORTA[1]   B4
PORTA[2]   A2
PORTA[3]   A1
PORTA[4]   C5
PORTA[5]   C4
PORTA[6]   B3
PORTA[7]   C3
RESET      N3 -pullup yes
CLK        J3 -pullup yes
```

## Memory Map

The memory map of this SOC is as follows:
```
$000 -> $FFF  4k RAM
```

## I/O Map

The I/O map of this SOC is as follows:
```
03            UART read  (keyboard)
04            UART write (teleprint)
30 -> 33      Timer registers
34            Output Register
```

## PDP-8 CPU Background Info

The PDP-8 was a 12-bit computer introduced by Digital Equipment Corporation (DEC) on March 22, 1965. The chief designer of the PDP-8 was Edson de Castro, who later founded Data General. The PDP-8 became a highly successful product line for DEC due to its relatively low price and good support for a wide range of peripherals. The PDP-8 was an improvement on the earlier DEC PDP-5 and the PDP-5 in turn was influenced by the MIT LINC and the CDC 160 minicomputers. Architecturally it was very simple with only a single 12-bit accumulator (on the base model) and very simple addressing modes. The base PDP-8 could only address 4096 12-bit words although later models added a user-managed memory-paging system to expand memory to 32K 12-bit words.

## Contributors

* Scott L Baker - SOC design

## License

See the **LICENSE** file in this repository
