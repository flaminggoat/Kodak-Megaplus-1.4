# Kodak Megaplus 1.4

## Architecture

* CCD - Kodak KAF-1400 1.4MP
* MCU - Motorola

## Pinout

Pinout has been reverse engineered from probing the Megaplus 1.4 PCBs, it may be inaccurate.

| Row A | Function            | Row B | Function        | Row C | Function                |
| ----- | ------------------- | ----- | --------------- | ----- | ----------------------- |
| 1     | RX+ A               | 13    | RX- A           | 25    | DOUT                    |
| 2     | COUT                | 14    | ~COUT           | 26    | ~DOUT                   |
| 3     | RX+ B               | 15    | RX- B           | 27    | NC                      |
| 4     | TX+ B               | 16    | TX- B           | 28    | NC                      |
| 5     | V+ to Cap A         | 17    | V- to Cap A & B | 29    | GAL GND                 |
| 6     | V+ to Cap B         | 18    | V- to Cap A & B | 30    | +5V                     |
| 7     | +5V                 | 19    | GND B           | 31    | GAL GND                 |
| 8     | -5.2V to MECL       | 20    | GND B           | 32    | +5V                     |
| 9     | ECL pulldown -2V?   down -2V?   | 21    | GND B           | 33    | NC                      |
| 10    | GND                 | 22    | GND             | 34    | GND                     |
| 11    | GND                 | 23    | GND             | 35    | GND                     |
| 12    | Power? to CCD board | 24    | NC              | 36    | -5V to AL1210           |
|       |                     |       |                 | 37    | +5V to AL1210 & MAX9687 |
|       |                     |       |                 | 38    | NC                      |
| COAX  | output              |       |                 | 39    | V+ to LT317 & CCD board |
|       |                     |       |                 | 40    | GND                     |
|       |                     |       |                 | 41    | GND                     |

## RX and TX pins

These connect to RS422 transceivers. 

RX and TX B connects through to the MCU, it is not connected to the UART pins of the MCU, it seems to accept a pulse and send a pulse on the tx lines in response.

RX A has unknown function.


## COUT and DOUT

These are differential MECL outputs.

* COUT - 10MHz clock
* DOUT - seems to be SOF or SOL pulse

## Pin 12
Connects to the collector of a 2N3906 PNP transistor on the CCD board. I think it should be an unknown negative voltage.

## Pin 39
Connects to LT317. Also passes through to the CCD board where it connects directly with the CCD. 15V seems to work...

### LT317

* R1 = 191
* R2 = 1500

Vout = 1.25*(1+1500/191)+50e-6*1500 = 11.14V