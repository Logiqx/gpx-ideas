## GPX Extensions

### Yacht Sailing

#### Overview

Example of a sailing yacht with a chartplotter / fish finder with external sensors - e.g. boat / water speed, temperature, depth.

- gpx_pvt - cog + sog
- gpx_imu - hdg, trim (pitch), heel (roll)
- gpx_sea - awa, aws, twa, tws, stw, 
- gpx_met - gwd, gws, atemp, wtemp

See short [video](https://www.youtube.com/watch?v=14TYwonISH0) with data overlays.



#### Trackpoint

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>1.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <sats>29</sats>
  <extensions>
    <pvt:ext>
      <pvt:cog>157.19</pvt:cog>
      <pvt:sog>8.542</pvt:sog>
    </pvt:ext>
    <imu:ext>
      <imu:hdg>275.23</imu:hdg>
      <imu:roll>15.25</imu:roll>
      <imu:pitch>10.15</imu:pitch>
    </imu:ext>
    <sea:ext>
      <sea:stw>9.176</sea:stw>
      <sea:dist>1234.567</sea:dist>
      <sea:awa>20.15</sea:awa>
      <sea:aws>4.23</sea:aws>
      <sea:twa>30.15</sea:twa>
      <sea:tws>3.43</sea:tws>
    </sea:ext>
    <met:ext>
      <met:atemp>20.15</met:atemp>
      <met:wtemp>6.89</met:wtemp>
      <met:gwd>25.46</met:gwd>
      <met:gws>5.23</met:gws>
    </met:ext>
  </extensions>
</trkpt>
```

