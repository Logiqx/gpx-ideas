## GPX Extensions

### Engine - gpx_eng

#### Overview

The engine elements listed below are important to motor vehicles, yachts, boats, planes, and helicopters. When combined with other extensions such as [gpx_pvt](../gpx_pvt/README.md) / [gpx_imu](../gpx_imu/README.md) / [gpx_met](../gpx_met/README.md) / [gpx_air](../gpx_air/README.md) / [gpx_sea](../gpx_sea/README.md), every common gauge and indicator on yachts, boats, planes and helicopters can be represented by GPX.

| Name                | Values   | Description                                                  |
| ------------------- | -------- | ------------------------------------------------------------ |
| `<ach id="n">`      | >= 0     | Tachometer for engine / rotor / propeller for revolutions per minute (RPM). See [RPM](https://gpsd.gitlab.io/gpsd/NMEA.html#_rpm_revolutions) in NMEA 0183 - only record when status "A" |
| `<trim id="n">`     | 0 to 100 | Propeller pitch as a percentage of the maximum (%). See [RPM](https://gpsd.gitlab.io/gpsd/NMEA.html#_rpm_revolutions) in NMEA 0183 - only record when status "A" |
| `<torq id="n">`     | >= 0     | Torque from engine in Newton metres (Nm)                     |
| `<temp id="n">`     |          | Temperature of cylinder head / exhaust gas / carburetor / oil / coolant in degrees centigrade (° C) |
| `<pressure id="n">` | >= 0     | Pressure for boost / vacuum / oil / coolant / fuel in kilopascals (kPa) |
| `<level id="n">`    | >= 0     | Amount of fuel / oil in litres (L)                           |
| `<volts id="n">`    | >= 0     | Battery level in volts (V)                                   |
| `<amps id="n">`     | >= 0     | Battery current which may be negative (charging) or positive (discharging) in amps (A) |

n.b. The "id" attribute could be useful in all of the other [extensions](../README.md) where multiple sensors are quite possible (and likely).



#### Notes

All of these engine measurements may result in multiple values for a single moment in time, which is why elements have an "id" attribute.

- `<tach>` might be required for boats with twin outboard motors
- `<temp>` might be required for oil temperature and coolant temperature
- `<level>` might be required for port and starboard fuel tanks

Sources for each "id" are optional, but if provided would be in elements such as `<gpx>`, `<trk>` or `<trkseg>`, much like in the [gpx_fit](../gpx_fit/README.md) examples.
