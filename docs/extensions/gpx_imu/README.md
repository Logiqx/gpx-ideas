## GPX Extensions

### Inertial Measurement Unit  - gpx_imu

#### Overview

Data derived from inertial measurement units (IMUs) can be added to `<wpt>`, `<rtept>` and `<trkpt>`  elements via GPX extensions.


| Name      | Values       | Description                                                  |
| --------- | ------------ | ------------------------------------------------------------ |
| `<head>`  | 0 to 360     | Heading is the direction in which an object is pointed, relative to true north in degrees (°)<br />Sailors and pilots refer to yaw as "heading"<br />See THS, [HDT](https://gpsd.gitlab.io/gpsd/NMEA.html#_hdt_heading_true), [HDG](https://gpsd.gitlab.io/gpsd/NMEA.html#_hdg_heading_deviation_variation) and [VHW](https://gpsd.gitlab.io/gpsd/NMEA.html#_vhw_water_speed_and_heading) in NMEA 0183 |
| `<rot>`   |              | Rate of turn (ROT) is the rate of change of heading, measured in degrees per minute (°/min)<br />Positive = clockwise, negative = counter-clockwise<br />See [ROT](https://gpsd.gitlab.io/gpsd/NMEA.html#_rot_rate_of_turn) in NMEA 0183 |
| `<roll>`  | -180 to +180 | Roll is the side-to-side rotation of an object about its longitudinal / x axis in degrees (°)<br />Sailors refer to roll as "heel", pilots refer to it as "bank" |
| `<pitch>` | -90 to +90   | Pitch is the up / down rotation of an object about its transverse / y axis in degrees (°)<br />Sailors often refer to pitch as "trim" |
| `<stat>`  | 0 or 1       | INS status flag. 0 = SPAN pre-alignment INS status, 1 = SPAN post-alignment INS status<br />TBC |

Accuracy estimates for heading, roll and pitch can be provided using the "acc" attribute.

| Name              | Values   | Description                                                  |
| ----------------- | -------- | ------------------------------------------------------------ |
| `<head acc="n">`  | 0 to 180 | Heading accuracy / error estimate in degrees, such that the difference between the true yaw and the reported yaw is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<roll acc="n">`  | 0 to 180 | Roll accuracy / error estimate in degrees, such that the difference between the true roll and the reported roll is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<pitch acc="n">` | 0 to 90  | Pitch accuracy / error estimate in degrees, such that the difference between the true pitch and the reported pitch is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |



#### Example Usage

Sea / Nautical

- [Dinghy Racing](../examples/sea/dinghy.md)
- [Yachting](../examples/sea/yacht.md)

Air / Aviation

- [Skydiver](../examples/air/skydiver.md)
- [Microlight](../examples/air/microlight.md)
- [Light Aircraft](../examples/air/aircraft.md) 

Meteorology

- [Weather Station](../examples/met/weather.md)
