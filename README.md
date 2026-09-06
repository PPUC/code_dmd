# Read pinball DMD data

This project allows to read the contents of a pinball DMD using the Raspberry Pi Pico. Both the RP2040 and RP2350 are supported.

## Officially supported pinball hardware systems

* WPC95 & WPC -> 128x32
* Data East -> 128x32 & 128x16
* Sega -> 128x32 & 192x64
* Stern Whitestar -> 128x32
* Stern SAM -> 128x32
* Stern SPIKE 1 -> 128x32
* Capcom -> 128x32 & 256x64
* Gottlieb/Premier -> 128x32
* Alvin G. & Co -> 128x32
* Homepin -> 128x32
* Spinball -> 128x32
* Sleic/Petaco -> 128x32
* Dotmation -> 192x64

## Pico hardware setup

The Pico is directly connected to all DMD data lines. Communication between the Pico and the consumer is implemented via SPI with an additional IRQ line. On this IRQ line, the Pico signals that a new frame is available, notifying the consumer to start the data transfer as soon as possible. This architecture accommodates consumers (especially Linux hosts like the Raspberry Pi) that are not real-time systems.

## Reading data

When reading data, we assume the data is sent correctly.
DMDreader sends complete frames only, containing a predefined amount of bits per pixel.

The process is as follows:
 - Wait for a frame to start (DMD frame detect PIO program)
 - Read frame (DMD dotloop PIO program)
 - Construct frame based on captured data (dmd_dma_handler IRQ)

## Project credits

DMDreader would not exist without the foundational work done by [Daniel Matuschek](https://github.com/pinballpower). Since then, the project has grown significantly due to extensive contributions from [Markus Kalkbrenner](https://github.com/mkalkbrenner) and [Jan Vos](https://github.com/pastorl69), who have delivered numerous bug fixes, performance optimizations, and support for additional manufacturers. Today, DMDreader is an integral part of [PPUC/DMD](https://ppuc.github.io/docs/ppuc_dmd/).

## License

This project has been forked from https://github.com/pinballpower/code_dmd. Since the original project changed its license from MIT to GPL v3 on 2022-05-02, the license of this fork is now also GPL v3.