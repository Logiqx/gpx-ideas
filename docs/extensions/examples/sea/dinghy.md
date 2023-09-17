## GPX Extensions

### Dinghy Racing

#### Overview

Example of a sailing dinghy with a custom GNSS training / racing instrument.

- gpx_pvt - cog + sog, plus accuracy estimates
- gpx_imu - head, trim (pitch), heel (roll)

See short [video](https://www.youtube.com/watch?v=hpqvp6MbXAQ) with data overlay at 1:28



#### Trackpoint

GPX 1.1 example:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>1.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <sats>29</sats>
  <extensions>
    <pvt:ext>
      <pvt:cog acc="10.0">157.19</pvt:cog>
      <pvt:sog acc="0.542">3.542</pvt:sog>
    </pvt:ext>
    <imu:ext>
      <imu:head>275.23</imu:head>
      <imu:roll>15.25</imu:roll>
      <imu:pitch>10.15</imu:pitch>
    </imu:ext>
  </extensions>
</trkpt>
```

GPX 1.2 will allow for horizontal and vertical accuracy estimates:

```xml
<trkpt lat="50.5710623" lon="-2.4563484" acc="1.937">
  <ele acc="2.754">1.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <sats>29</sats>
  <extensions>
    <pvt:ext>
      <pvt:cog acc="10.0">157.19</pvt:cog>
      <pvt:sog acc="0.542">3.542</pvt:sog>
    </pvt:ext>
    <imu:ext>
      <imu:head>275.23</imu:head>
      <imu:roll>15.25</imu:roll>
      <imu:pitch>10.15</imu:pitch>
    </imu:ext>
  </extensions>
</trkpt>
```



#### Sailmon

The Sailmon Max currently outputs the following data to CSV files:

- Time + latitude + longitude
- HDT + SOG + COG
- TWA + TWD (both require an airspeed sensor)
- Heel + Trim
- Satellites + hAcc

