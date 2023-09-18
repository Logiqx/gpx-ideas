## GPX Extensions

### Inertial Measurement Unit  - gpx_imu

#### Overview

Heading (yaw) and attitude (pitch and roll) from inertial measurement units (IMUs) is relevant to a huge number of activities; land, sea and air.


| Name      | Values       | Description                                                  |
| --------- | ------------ | ------------------------------------------------------------ |
| `<hdg>`   | 0 to 360     | Heading (HDG) is the direction in which an object is pointed, relative to true north in degrees (°). Heading and yaw are synonymous but sailors and pilots will always refer to yaw as heading. See THS, [HDT](https://gpsd.gitlab.io/gpsd/NMEA.html#_hdt_heading_true), [HDG](https://gpsd.gitlab.io/gpsd/NMEA.html#_hdg_heading_deviation_variation) and [VHW](https://gpsd.gitlab.io/gpsd/NMEA.html#_vhw_water_speed_and_heading) in NMEA 0183 |
| `<pitch>` | -90 to +90   | Pitch is the up / down rotation of an object about its transverse / y axis in degrees (°).  Sailors will sometimes refer to pitch as "trim" |
| `<roll>`  | -180 to +180 | Roll is the side-to-side rotation of an object about its longitudinal / x axis in degrees (°). Sailors refer to roll as "heel", whereas pilots refer to it as "bank". A value greater than 90 degrees indicates an inversion of the vessel / aircraft. |
| `<stat>`  | 0 or 1       | INS status flag. 0 = SPAN pre-alignment INS status, 1 = SPAN post-alignment INS status |
| `<rot>`   |              | Rate of turn (ROT) is the rate of change of heading, measured in degrees per minute (°/min). A positive number means turning clockwise and negative number means turning counter-clockwise. ROT is most relevant to ships and aircraft where it is a measure of how fast the vessel / aircraft is turning. See [ROT](https://gpsd.gitlab.io/gpsd/NMEA.html#_rot_rate_of_turn) in NMEA 0183 |

Accuracy estimates for heading, roll and pitch can be provided using the "acc" attribute.

| Name              | Values   | Description                                                  |
| ----------------- | -------- | ------------------------------------------------------------ |
| `<hdg acc="n">`   | 0 to 180 | Heading accuracy / error estimate in degrees, such that the difference between the true yaw and the reported yaw is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<roll acc="n">`  | 0 to 180 | Roll accuracy / error estimate in degrees, such that the difference between the true roll and the reported roll is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<pitch acc="n">` | 0 to 90  | Pitch accuracy / error estimate in degrees, such that the difference between the true pitch and the reported pitch is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |



#### Notes

- The standard abbreviation for heading is HDG in nautical and aviation environments, hence the naming of `<hdg>` in this schema
  - The words heading and yaw are synonymous. However, yaw values are sometimes -180 to 180, so heading = (yaw + 360) % 360
  - The aviation industry (worldwide) is currently preparing to switch from magnetic north to true north - [Mag2True](https://www.aerosociety.com/news/time-for-a-change-of-direction)
- The availability of accuracy / error estimates is largely due to the use of a Kalman filter within the IMU



#### Exclusions

- Instantaneous heave (up / down), sway (left / right) and surge (front / back)
  - Instantaneous heave is sometimes calculated in GNSS + INS solutions, but not sway or surge?



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

