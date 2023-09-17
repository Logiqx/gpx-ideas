## GPX Extensions

### Sea / Nautical - gpx_sea

#### Random Notes - UNEDITED

- Everything is covered by [IEC 61162](https://en.wikipedia.org/wiki/IEC_61162) part 1 (single talker and multiple listeners) which is [NMEA 0183](https://en.wikipedia.org/wiki/NMEA_0183)
- Elsewhere:
  - Engine revolutions per minute (RPM) - use tachometer which is in the generic extension (gpx_gen)
- Unnecessary:
  - No need for velocity made good (VMG), directly upwind or downwind - short [video](https://www.youtube.com/watch?v=14TYwonISH0)
    - VMG using [VPW](https://gpsd.gitlab.io/gpsd/NMEA.html#_vpw_speed_measured_parallel_to_wind)
    - VMG can be calculated from STW + heading and TWD - long [video](https://www.youtube.com/watch?v=KdeVIgqN8Ec)
    - It is also possible to calculate VMG using SOG + COG and TWD
  - No need for opposite tacking heading
    - It provides the navigator with the Heading the Boat will be sailing on if it is sailed to the same wind angle on the opposite Tack
    - It is very simple to calculate opposite tack heading from the current heading and TWD
- Links
  - See page about [wind](https://raymarine.custhelp.com/app/answers/detail/a_id/3794/~/apparent-wind%2C-true-wind-and-ground-wind%2C-and-data-required-to-calculate-them#:~:text=Apparent%20Wind%20will%20vary%20depending,(wind%20on%20the%20bow.)) for details about apparent wind, true wind, etc.
  - See page about [distance](https://forum.raymarine.com/showthread.php?tid=123) logs

