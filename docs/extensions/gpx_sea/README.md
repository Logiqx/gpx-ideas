## GPX Extensions - Sea / Nautical

### Overview

Sea / nautical elements include speed through the water (STW), wind measurements, tidal measurements and water depth.

| Name      | Values      | Description                                                  |
| --------- | ----------- | ------------------------------------------------------------ |
| `<stw>`   |             | Speed through the water (STW) / boat speed in meters per second (m/s)<br />See [VHW](https://gpsd.gitlab.io/gpsd/NMEA.html#_vhw_water_speed_and_heading) in NMEA 0183 - units are knots or km/h, but recommend converting from knots to m/s<br />n.b. different to `<sog>` in gpx_pvt which is speed over ground |
| `<dist>`  | >= 0        | Cumulative distance for the trip / distance through the water since last reset in meters (m)<br />See [VLW](https://gpsd.gitlab.io/gpsd/NMEA.html#_vlw_distance_traveled_through_water) (water distance since reset) in NMEA 0183 - units are nautical miles so need to convert to meters<br />n.b. different to `<dist>` in gpx_pvt which is trip distance over ground |
| `<awa>`   | -180 to 180 | Apparent wind angle (AWA), relative to the bow in degrees (°)<br />See [MWV](https://gpsd.gitlab.io/gpsd/NMEA.html#_mwv_wind_speed_and_angle) (reference = R) and [VWR](https://gpsd.gitlab.io/gpsd/NMEA.html#_vwr_relative_wind_speed_and_angle) in NMEA 0183 |
| `<aws>`   | >= 0        | Apparent wind speed (AWS) in metres per second (m/s)<br />See [MWV](https://gpsd.gitlab.io/gpsd/NMEA.html#_mwv_wind_speed_and_angle) (reference = R) and [VWR](https://gpsd.gitlab.io/gpsd/NMEA.html#_vwr_relative_wind_speed_and_angle) in NMEA 0183 |
| `<twa>`   | -180 to 180 | True wind angle (TWA) representing wind-over-water, relative to the bow in degrees (°)<br />See [MWV](https://gpsd.gitlab.io/gpsd/NMEA.html#_mwv_wind_speed_and_angle) (reference = T) in NMEA 0183 |
| `<tws>`   | >= 0        | True wind speed (TWS) representing wind-over-water in metres per second (m/s)<br />See [MWV](https://gpsd.gitlab.io/gpsd/NMEA.html#_mwv_wind_speed_and_angle) (reference = T) in NMEA 0183 |
| `<set>`   | 0 to 360    | Direction of the water / current, relative to true north in degrees (°)<br />See [VDR](https://gpsd.gitlab.io/gpsd/NMEA.html#_vdr_set_and_drift) in NMEA 0183 |
| `<drift>` | >= 0        | Speed of the water / current in meters per second (m/s)<br />See [VDR](https://gpsd.gitlab.io/gpsd/NMEA.html#_vdr_set_and_drift) in NMEA 0183 - units are knots so need to convert to m/s |
| `<depth>` | >= 0        | Depth of the water below the surface in meters (m)<br />See [DBS](https://gpsd.gitlab.io/gpsd/NMEA.html#_dbs_depth_below_surface) (not DBK or DBT) in NMEA 0183 - often determined by chartplotter or fishfinder |



### Background

- Non-sailors can read a page written by [Raymarine](https://raymarine.custhelp.com/app/answers/detail/a_id/3794/~/apparent-wind%2C-true-wind-and-ground-wind%2C-and-data-required-to-calculate-them#:~:text=Apparent%20Wind%20will%20vary%20depending,(wind%20on%20the%20bow.)) to understand the difference between apparent wind, true wind, and ground wind.



### Notes

- Boat speed / speed through the water (STW) is typically measured using a paddlewheel or ultrasonic transducer
- Distance through water is included to avoid possible accumulated errors when deriving from speed every second
- True wind is typically wind-over-water (using heading and water speed sensor) but can be wind-over-ground (using heading, COG + SOG)
  - Strictly speaking you do not need to record TWA and TWS.
    - However, recording the true wind (TWA and TWS) will help to maintain precision
  - There is no need to record true wind direction (TWD) which is relative to true north in degrees (°)
    - It can easily be calculated from TWA and the heading
      - TWD = (TWA + heading)  % 360
- Tidal elements "drift" and "set" can be calculated from other elements but have been included to maintain precision
  - See page about [set and drift](http://www.sailfastllc.com/AppNoteCurrentSetAndDrift) which explains how they are determined using a vector triangle
- Rate of turn (ROT) is supported by the [gpx_imu](../gpx_imu/README.md) extension
  - ROT represents the rate of change of heading, typically measured by external rate of turn turn indicator ([ROTI](https://en.wikipedia.org/wiki/Rate_of_turn_indicator))
  - ROT should <u>not</u> be derived from COG information - [link](https://www.navcen.uscg.gov/ais-class-a-reports)
- "Ground distance since reset" (VLW sentence) should go in `<pvt:dist>` - see [gpx_pvt](../gpx_pvt/README.md)



### Exclusions

- IMU data such as heading, pitch and roll are handled by the [gpx_imu](../gpx_imu/README.md) extension
- Meteorological data is handled by the [gpx_met](../gpx_met/README.md) extension
  - `<atemp>` and `<wtemp>` should be used for air temperature and water temperature
  - `<gwd>` and `<gws>` should be used for ground wind direction and speed, not to be confused with TWD and TWS
- Engine data is handled by the [gpx_eng](../gpx_eng/README.md) extension
  - e.g. tachometers, temperatures, pressures, fuel, batteries, etc

- VMG relative to the wind is not included at this time because it can be calculated from SOG + COG and TWD



### Example Usage

Sea / Nautical

- [Yachting](../examples/sea/yacht.md)

Meteorology

- [Weather Station](../examples/met/weather.md)

