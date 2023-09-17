## GPX Extensions

### Sea / Nautical - gpx_sea

#### Random Notes - UNEDITED

- Everything is covered by [IEC 61162](https://en.wikipedia.org/wiki/IEC_61162) part 1 (single talker and multiple listeners) which is [NMEA 0183](https://en.wikipedia.org/wiki/NMEA_0183)
- Unnecessary:
  - No need for velocity made good (VMG), directly upwind or downwind - short [video](https://www.youtube.com/watch?v=14TYwonISH0)
    - VMG using [VPW](https://gpsd.gitlab.io/gpsd/NMEA.html#_vpw_speed_measured_parallel_to_wind)
    - VMG can be calculated from STW + heading and TWD - long [video](https://www.youtube.com/watch?v=KdeVIgqN8Ec)
  - No need for opposite tacking heading
    - It provides the navigator with the Heading the Boat will be sailing on if it is sailed to the same wind angle on the opposite Tack
    - It is very simple to calculate opposite tack heading from the current heading and TWD
- Links
  - See page about [distance](https://forum.raymarine.com/showthread.php?tid=123) logs

