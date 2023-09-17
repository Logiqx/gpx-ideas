## GPX Extensions

### Inertial Measurement Unit  - gpx_imu

#### Random Notes - UNEDITED

TODO - might add heave, surge, sway?

Separate accuracy estimates are an old idea:

| Name     | Values   | Description                                                  |
| -------- | -------- | ------------------------------------------------------------ |
| `<hacc>` | 0 to 180 | Heading accuracy / error estimate in degrees, such that the difference between the true yaw and the reported yaw is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<racc>` | 0 to 180 | Roll accuracy / error estimate in degrees, such that the difference between the true roll and the reported roll is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<pacc>` | 0 to 90  | Pitch accuracy / error estimate in degrees, such that the difference between the true pitch and the reported pitch is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |

u-blox

- https://www.u-blox.com/en/product/zed-f9r-module?legacy=Current#Documentation-&-resources
- https://content.u-blox.com/sites/default/files/documents/ZED-F9R-03B_DataSheet_UBX-22024085.pdf
- https://content.u-blox.com/sites/default/files/documents/u-blox-F9-HPS-1.30_InterfaceDescription_UBX-22010984.pdf



Notes

- Heading is relative to true north, rather than magnetic north
  - Gyrocompasses are widely used on boats and ships
  - The aviation industry is currently preparing to move from the use of magnetic north to true north - [link](https://www.aerosociety.com/news/time-for-a-change-of-direction)
- Background
  - 6 degrees of freedom - [link](https://www.roadtovr.com/introduction-positional-tracking-degrees-freedom-dof/) - [wiki](https://en.wikipedia.org/wiki/Degrees_of_freedom_(mechanics))
  - See Wikipedia about [IMU](https://en.wikipedia.org/wiki/Inertial_measurement_unit) devices
  - See Wiki about [INS](https://en.wikipedia.org/wiki/Inertial_navigation_system#Inertial_navigation_systems_in_detail) and page about [ship motion](https://nautiluslive.org/video/2020/12/09/beyond-wow-six-types-ship-motion)
  - See Novatel [PASHR](https://docs.novatel.com/OEM7/Content/SPAN_Logs/PASHR.htm) and gpsd [PASHR](https://gpsd.gitlab.io/gpsd/NMEA.html#_pashr_rt300_proprietary_roll_and_pitch_sentence)
- TBC - Heave, sway and surge
  - Typically describe motion of boats
    - surge - Movement forward and backward in meters (m/s)
    - sway - Movement left and right in meters (m/s)
    - heave - Movement upwards and downward in meters (m/s)
  - Aircraft may also have the concept - [link](https://ntrs.nasa.gov/api/citations/20160013217/downloads/20160013217.pdf)
- Reference for value ranges
  - Option 1 - yaw = 0 to 360, pitch = -90 to 90, roll = -90 to 90 - [link](https://www.skylineglobe.com/Legacy/TerraExplorer/v6.6.0/APIReferenceGuide/Yaw_Pitch_and_Roll_Angles.htm)
  - Option 2 - yaw = -18 0to 180, pitch = -90 to 90, roll = -90 to 90 - [link](https://stackoverflow.com/questions/9143161/max-and-min-values-of-roll-pitch-and-yaw-of-the-capture-motion-of-iphone)
- Errors
  - overview of error estimates - [link](https://www.canalgeomatics.com/knowledgebase/imu-accuracy-error-definitions/)
- Aviation refers to pitch and roll as "attitude" - see [artificial horizon](https://en.wikipedia.org/wiki/Attitude_indicator) and [stack exchange](https://aviation.stackexchange.com/questions/35933/what-is-the-exact-meaning-of-attitude-does-it-include-translational-movement)
  - boats and aircraft both use the word "pitch"
  - boats and aircraft use the word "heading" instead of "yaw"
- Pitch, roll and yaw also can be determined using two high-precision GNSS receivers - e.g. Novatel [Attitude](https://novatel.com/solutions/attitude)
  - Should not assume they are INS, they might also be gyroscopic such as on a plane
- Excluded for now
  - Instantaneous heave (up / down), sway (left / right) and surge (front / back)
    - I've seen instantaneous heave in GNSS + INS solutions, but not sway or surge

