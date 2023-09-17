## GPX Extensions

### Sea / Nautical - gpx_sea

#### Random Notes - UNEDITED

- "Ground distance since reset" (VLW sentence) should go in `<pvt:dist>`
- Everything is covered by [IEC 61162](https://en.wikipedia.org/wiki/IEC_61162) part 1 (single talker and multiple listeners) which is [NMEA 0183](https://en.wikipedia.org/wiki/NMEA_0183)
- Boat speed / speed through the water (STW) is typically measured using a paddlewheel or ultrasonic transducer
- Distance through water is included to avoid possible accumulated errors when deriving from speed every second.
- True wind is typically wind-over-water (using heading and water speed sensor) but can be wind-over-ground (using heading, COG + SOG)
  - Strictly speaking you do not need to record TWA and TWS.
    - However, recording the true wind will help to maintain precision
- Tidal elements "drift" and "set" can be calculated from other elements but have been included to maintain precision
  - See page about [set and drift][http://www.sailfastllc.com/AppNoteCurrentSetAndDrift] which explains how they are determined using a vector triangle, hence their exclusion.
- Rate of turn (ROT):
  - ROT represents the rate of change of heading, typically measured by external rate of turn turn indicator ([ROTI](https://en.wikipedia.org/wiki/Rate_of_turn_indicator))
  - ROT should <u>not</u> be derived from COG information - [link](https://www.navcen.uscg.gov/ais-class-a-reports)
- Elsewhere:
  - Engine revolutions per minute (RPM) - use tachometer which is in the generic extension (gpx_gen)
- Unnecessary:
  - No need for true wind direction (TWD) which represents wind-over-water, relative to true north in degrees (°)
    - It can easily be calculated from TWA and heading
      - TWD = (TWA + heading)  % 360
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

