# Transmitter Setup
# Table of Contents
1. [DX18](#DX18)
  * [Assign Channels](#Assign Channels)
  * [Reverse Servos](#Reverse Servos)
  * [Trim Servos](#Trim Servos)
  * [Mix Channels](#Mix Channels)
 

## Allows 6 flight modes. (Mission Planner: FLTMODE_CH = 7)

<div id='DX18'/>
### DX18

<div id='Assign Channels'/>

* Assign Channels  
   System Setup (start) -> Channel Assign (click) -> Next (click) -> Channel Input Config (stay)
  * THRO: N/A
  * AILE: N/A
  * ELEV: N/A
  * RUDD: N/A
  * GEAR: C
  * AUX1: F
  * AUX2: E

<div id='Reverse Servos'/>

* Reverse Servos  
   Function List (start) -> Servo Setup (click) -> Travel (scroll) -> Reverse (stay)
  * AX1: reversed
  * AX2: reversed

<div id='Trim Servos'/>

* Trim Servos  
   Function List (start) -> Servo Setup (click) -> Travel (stay)

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| 100 | 100 | 100 | 100 | 100 |
| 100 | 100 | 100 | 100 | 100 |
| THR | AIL | ELE | RUD | GER |
|     |     |     |     |     |
| 100 | 100 | 100 | 100 | 100 |
| 100 | 70  | 100 | 100 | 100 |
| AX1 | AX2 | AX3 | AX4 | AX5 |

<div id='Mix Channels'/>

* Mix Channels  
   Function List (start) -> Mixing (click) -> P-Mi x 1:   INH > INH    On (click) -> Normal (click)
  * AX1>AX2
  * Rate: 0% 33%
  * Offset: 100%
  * Trim Inh
  * Switch: On
