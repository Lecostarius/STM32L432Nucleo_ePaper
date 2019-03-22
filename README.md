# STM32L432Nucleo_ePaper
Code to attach the Waveshare 1.5'' ePaper (SKU12955) to a STM32L432 Nucleo board

This is a working example of how to control a ePaper display using a STM32 microcontroller.
I used a Waveshare 1.5 inch ePaper module. Waveshare offers on their website implementations
of a control library for it, for three platforms (Arduino, Raspberry and STM32). The example
for STM32 is designed for a STM32F1.

I wanted to have it for a STM32L432 Nucleo board (which should become an environment sensor
platform at some later time). 

Also, I wanted to use a free platform - so it uses gcc and a Makefile. I used VSCode as Editor,
so the VSCode configuration directory is also part of the repository. It is not needed if another
editor is used.

What needed to be done is:

1) using the STM32Cube, setting Pins for SPI and some GPIO (3 outputs, one for Chip Select of
SPI, one for RST and one for DC; plus one GPIO Input for BUSY) and naming them just they were
named in the Waveshare code (BUSY, RST, DC).
2) create code using STM32Cube
3) copy the User/ directory from the Waveshare example code for STM32F1 into the new directory
4) adapt the Makefile (manually adding the library)
5) copy-paste the example code into main.c
6) change three (or so) references to F1 HAL libraries to the corresponding L4 libraries
7) connect the ePaper electrically:

ePaper  Nucleo
VCC     3V3
GND     GND
DIN     A6  (PA7, this is SPI1_MOSI)
CLK     A1  (PA1, this is SPI1_SCK)
CS      D6  (PB1, SPI_CS)
DC      D3  (PB0)
RST     A4  (PA5)
BUSY    A2  (PA3)

8) compile, flash. If you flash from a .bin file, the Prog. addr. is 0x08000000. I was using
the SEGGER J-Flash Lite 6.44b, after changing the standard ST-LINKV2 interface of the Nucleo
board to Segger J-Link. But I verified that flashing with ST-LINKV2 directly works just the same.
