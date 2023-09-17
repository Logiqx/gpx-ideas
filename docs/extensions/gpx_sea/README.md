## GPX Extensions

### Sea / Nautical - gpx_sea

#### Overview

Sea / nautical elements can be added to `<wpt>`, `<rtept>` and `<trkpt>`  elements via GPX extensions.

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



#### Example Usage

Sea / Nautical

- [Yachting](../examples/sea/yacht.md)

Meteorology

- [Weather Station](../examples/met/weather.md)

