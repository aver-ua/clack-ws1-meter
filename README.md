# Clack WS1 Control Valve Meter
This project forked from https://github.com/fonske/clack-reader 

ESPHome config to monitor Clack WS1 Control Valve used in water softeners and purification systems. 
In my case it is a purification system from Ecosoft (Ukraine). 

## Set up Clack WS1 "RELAY 1 / RLY 1", "RELAY 2 / RLY 2"

You need to configure Clack WS1 Valve relays: 
- Relay 1 (RELAY 1 / rLY1) activates after a set number of water liters have been used 
- Relay 2 (RELAY 2 / rLY2) activates at the beginning of a regeneration cycle 

[EN Manual 1](/docs/Clack%20WS1%20manual.pdf) pages 13-14 
[EN Manual 2](/docs/Clack%20WS1%20manual2.pdf) pages 12-13 

Buttons: `NEXT` - next step | `REGEN` - previous step | `ARROWS` - change value 

1.	Press `NEXT` + `ARROW DOWN` and hold 5 seconds
2.	Press `NEXT` until `RELAY 1` / `rLY1` is visible
    a.	Use arrows to change value. Set it on: `VOLUME` / `Softening On L` 
    b.	Press `NEXT` again
    c.	Set it on 10 L (Watermeter pulse. ID `clack_pulse_liters` settings in `clack-ws1-meter.yaml`. This is default value, you can change it to desired)
    d.	Press `NEXT` again
    e.	Set time: 0.01 min
3.	Press `NEXT` until `RELAY 2` / `rLY2` is visible
    a.	Use arrows to change value. Set it on: `REGEN TIME` / `Time to On`
    b.	Press NEXT again
    c.	Set time: 0.01 min

## Schematic
[Clack WS1 PCB Relay terminal block](/images/ws1-pcb.png) has 3 outs (GND is central). Output voltage 15-17V, so, a step-down DC-DC modules is required. Then you must use also two 12V or 5V relay modules connected to each DC-DC module out. Relays connected to GPIO19 (watermeter pulse), GPIO18 (regeneration pulse) of ESP32. 
Ultrasonic sensor HC-SR04 (to measure the salt level) connected to GPIO25 (trigger) and GPIO26 (echo). The sensor is [placed under the lid of the salt tank](/images/board_example.jpg). 
[Schematic diagram of connections](/images/Schematic_clack-ws1-meter.png) 
[Board Example](/images/board_example.jpg) 

## Installation
1. Create new device in ESPHome
2. Copy the contents of the file `clack-ws1-meter.yaml`
3. Edit substitutions & customize
4. Flash firmware to your ESP32

## References
- https://github.com/fonske/clack-reader