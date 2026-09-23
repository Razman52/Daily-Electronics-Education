## Multiplexer

digital electrical components that selects one of several input signals and outputs a single line. Think multi-position rotary switch.

- Digital mux: logic gates or transmission gates to switch binary data
- Analog mux: routes analogue voltages/currents using MOSFETS/switches

## I2C

communication protocol. short-distance, with two wires. used for connecting microcontrollers to chips like sensors and displays.

- Wire 1 = SDA (serial data) for information, wire 2 = SCK (serial clock) synchronise timing.
- Address system: every device on the line has a specific address (can be hexadecimal or binary), the microcontroller calls the address and only that device responds.
- Shared bus: multiple components can be attached to the same two wires. **identical sensors often-times share same addresses making this not possible.**

## I2C Multiplexer

hardware switch enabling the connection of multiple devices with exact same address to a single controller.

- takes one main I2C input line, splits into multiple output channels, one-by-one the channels open up to enable communcation between MC and the sensors without crosstalk.
- only adds ~50us latency from switching between channels. latency from software manually turning more GPIO pins on/off is greater.

## Communication Protocols
#### I2C - Inter-Integrated Circuit

- Wires required: 2 (SDA - Serial Data, SCK - Serial Clock)
- Topology: Bus (multiple devices share 2 wires)
- Addressing: sofware-based (unique ID sent over data line)
- Speed: 100 kbps - 1 Mbps
- Duplex: half-duplex (cannot send and receive simultaneosly)
- Use cases: connecting multiple simple sensors on board to save pins

#### SPI - Serial Peripheral Interface

- Wires required: 4+ (MOSI - master out / slave in, MISO - master in / slave out, SCK - serial clock, CS - chip select)
- Topology: Bus (shared data/clock lines, separate CS lines)
- Addressing: hardware-based (dedicated CS pin per slave)
- Speed: 10 Mbps - 50+ Mbps
- Duplex: full-duplex (send & receive signals simultaneously)
- Use cases: high-speed data like SD cards, LCD screens or fast ADCs

#### UART - Universal Asynchronous Receiver-Transmitter
- Wires Reqruied: 2 (TX - transmitter, RX - receiver)
- Topology: Point-to-point (1-to-1)
- Addressing: N/A, direct connections
- Speed: Medium (9600 bps - 1 Mbps)
- Full-duplex
- Use cases: connecting two devices, GPS modules, or PC serial debugging

## Why devices are limited to certain protocols
Peripheral controller dependency - the dedicated hardware blocks that handle the I2C/SPI work
- peripheral controller blocks hardwired to pins in traditional microcontrollers
- can perform bit-banging but results in slower, more unstable commmunication
  - manually toggling the standard digital pins fast enough to mimic communication protocols in software

## ESP32 GPIO Matrix
ESP32 has flexibility of GPIO matrix: arbitrary pin mapping with hardware acceleration, and multiple hardware buses 
- arbitrary pin mapping: can control via software which pins SDA/SCK for I2C, or TX/RX for UART
- hardware acceleration: even after mapping, communication still processed with dedicated hardware controllers. **flexibility of bit-banging with speed and zero-CPU overhead of hardware peripherals**
- multiple hardware buses: 4 SPIs, 3 UARTs, 2 I2Cs
- limitations include some pins being input only (**lack pull-up resistor**)