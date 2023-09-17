## GPX Extensions

### Meteorological - gpx_met

#### Overview

Meteorological data is straightforward to understand and is relevant to many activities; land, sea and air.

All of the meteorological elements listed below are available in the [MDA](https://gpsd.gitlab.io/gpsd/NMEA.html#_mda_meteorological_composite) sentence of NMEA 0183.

| Name      | Values   | Description                                                  |
| --------- | -------- | ------------------------------------------------------------ |
| `<atemp>` |          | Air temperature in degrees centigrade (° C).  See [MDA](https://gpsd.gitlab.io/gpsd/NMEA.html#_mda_meteorological_composite) in NMEA 0183 |
| `<wtemp>` |          | Water temperature in degrees centigrade (° C). See [MDA](https://gpsd.gitlab.io/gpsd/NMEA.html#_mda_meteorological_composite) and [MTW](https://gpsd.gitlab.io/gpsd/NMEA.html#_mtw_mean_temperature_of_water) in NMEA 0183 |
| `<gwd>`   | 0 to 360 | Ground wind direction (GWD), relative to true north in degrees (°). See [MDA](https://gpsd.gitlab.io/gpsd/NMEA.html#_mda_meteorological_composite) in NMEA 0183 |
| `<gws>`   | >= 0     | Ground wind speed (GWS) in metres per second (m/s). See [MDA](https://gpsd.gitlab.io/gpsd/NMEA.html#_mda_meteorological_composite) in NMEA 0183 |
| `<baro>`  | > 0      | Barometric pressure in hectopascals (hPa) / millibars (mb). See [MDA](https://gpsd.gitlab.io/gpsd/NMEA.html#_mda_meteorological_composite) in NMEA 0183 |
| `<hum>`   | 0 to 100 | Relative humidity in percent (%). See [MDA](https://gpsd.gitlab.io/gpsd/NMEA.html#_mda_meteorological_composite) in NMEA 0183 |
| `<dew>`   |          | Dew point in degrees centigrade (° C). See [MDA](https://gpsd.gitlab.io/gpsd/NMEA.html#_mda_meteorological_composite) in NMEA 0183 |



#### Notes

- Wind direction + speed use their nautical names, signifying "wind over ground" or "ground wind" (GWD + GWS)
- Dew point is included because it can be directly measured, not just calculated from air temperature and relative humidity
- Wind chill is not included because it is calculated from the air temperature and wind speed
- Heat index is not included because it is calculated from air temperature and relative humidity



#### Example Usage

Land / Fitness

- [Cycling](../examples/fit/cycling.md)

Sea / Nautical

- [Yachting](../examples/sea/yacht.md)

Air / Aviation

- [Light Aircraft](../examples/air/aircraft.md) 

Meteorology

- [Weather Station](../examples/met/weather.md)

