## GPX Extensions

### Position / Velocity / Time - gpx_pvt

#### Overview

Position / velocity / time (PVT) elements are outputs of GPS / GNSS chipsets and location APIs - see [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) and [VTG](https://gpsd.gitlab.io/gpsd/NMEA.html#_vtg_track_made_good_and_ground_speed) sentences of NMEA 0183.

The following components can be added to `<wpt>`, `<rtept>` and `<trkpt>` elements via GPX extensions.

| Name     | Values   | Description                                                  |
| -------- | -------- | ------------------------------------------------------------ |
| `<cog>`  | 0 to 360 | Course over ground (COG) in degrees is the actual direction of travel relative to true north. COG is an independent measurement from position, so it is possible (and not an error) for the difference between two successive positions to be inconsistent with the COG values.<br />See [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) and [VTG](https://gpsd.gitlab.io/gpsd/NMEA.html#_vtg_track_made_good_and_ground_speed) in NMEA 0183 |
| `<sog>`  | >= 0     | Speed over ground (SOG) / ground speed (GS) in m/s is the horizontal speed calculated by the GPS / GNSS chipset. SOG is an independent measurement from position, so it is possible (and not an error) for the difference between two successive positions to be inconsistent with the SOG values.<br />See [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) and [VTG](https://gpsd.gitlab.io/gpsd/NMEA.html#_vtg_track_made_good_and_ground_speed) in NMEA 0183 - units are knots or km/h, but recommend converting from knots to m/s |
| `<roc>`  |          | Rate of climb (ROC) / rate of descent (ROD) / vertical speed / in m/s calculated by the GPS / GNSS chipset. ROC is an independent measurement from position, so it is possible (and not an error) for the difference between two successive positions to be inconsistent with the ROC values. |
| `<dist>` | >= 0     | Cumulative distance over ground for the trip / activity in meters (m)<br />Sometimes measured by a wheel odometer, thus can be independent of the GPS / GNSS receiver<br />See [VLW](https://gpsd.gitlab.io/gpsd/NMEA.html#_vlw_distance_traveled_through_water) (ground distance since reset) - units are nautical miles so need to convert to meters |

Accuracy estimates for COG, SOG and ROC can be provided using the "acc" attribute.

| Name             | Values   | Description                                                  |
| ---------------- | -------- | ------------------------------------------------------------ |
| `<cog acc="n">`  | 0 to 180 | Course over ground (COG) accuracy / error estimate in degrees, such that the difference between the true COG and the reported COG is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<sog  acc="n">` | >= 0     | Speed over ground (SOG) accuracy / error estimate in m/s, such that the difference between the true SOG and the reported SOG is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<roc  acc="n">` | >= 0     | Vertical speed accuracy / error estimate in m/s, such that the difference between the true ROC and the reported ROC is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |

GPX 1.2 can also support position and time accuracy estimates using the "acc" attribute.

| Name              | Values | Description                                                  |
| ----------------- | ------ | ------------------------------------------------------------ |
| `<trkpt acc="n">` | >= 0   | Horizontal accuracy / error estimate in meters, such that the difference between the true horizontal position and the reported horizontal position is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed.<br />TODO - list NMEA sentences |
| `<ele acc="n">`   | >= 0   | Vertical accuracy / error estimate in meters, such that the difference between the true vertical position and the reported vertical position is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed.<br />TODO - list NMEA sentences |
| `<time acc="n">`  |        | Time accuracy / error estimate in seconds (including milliseconds), such that the difference between the true time and the reported time is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |



#### Example Usage

Land / Fitness

- [Hiking](../examples/fit/hiking.md)
- [Running](../examples/fit/running.md)
- [Cycling](../examples/fit/cycling.md)

Sea / Nautical

- [GPS Speedsailing](../examples/sea/gpsss.md)
- [Dinghy Racing](../examples/sea/dinghy.md)
- [Yachting](../examples/sea/yacht.md)

Air / Aviation

- [Skydiver](../examples/air/skydiver.md)
- [Microlight](../examples/air/microlight.md)
- [Light Aircraft](../examples/air/aircraft.md) 

Meteorology

- [Weather Station](../examples/met/weather.md)

