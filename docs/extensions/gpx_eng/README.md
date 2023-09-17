## GPX Extensions

### Engine - gpx_eng

#### Overview

The engine elements listed below are important to motor boats, planes, and helicopters.

| Name            | Values   | Description                                                  |
| --------------- | -------- | ------------------------------------------------------------ |
| tach id="n"     | >= 0     | Tachometer for engine / rotor / propeller for revolutions per minute (RPM)<br />See [RPM](https://gpsd.gitlab.io/gpsd/NMEA.html#_rpm_revolutions) in NMEA 0183 - only record when status "A" |
| trim id="n"     | 0 to 100 | Propeller pitch as a percentage of the maximum (%) - boats<br />See [RPM](https://gpsd.gitlab.io/gpsd/NMEA.html#_rpm_revolutions) in NMEA 0183 - only record when status "A" |
| torq id="n"     | >= 0     | Engine torque in Newton metres (Nm)<br />e.g. helicopters    |
| temp id="n"     |          | cylinder head, exhaust gas, carburetor, oil, coolant         |
| pressure id="n" | >= 0     | Boost, vacuum, oil, coolant, fuel                            |
| level id="n"    | >= 0     | Fuel / oil quantity in litres (L)                            |
| volts id="n"    | >= 0     | Battery level in volts (V)                                   |
| amps id="n"     | >= 0     | Battery current - negative (charging) or positive (discharging) in amps (A) |

