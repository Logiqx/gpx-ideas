## GPX Extensions

### GPS Speedsailing

#### Overview

Example of a windsurfer with a custom GNSS logger featuring a u-blox chipset.

- gpx_pvt - cog + sog, plus accuracy estimates

See short [video](https://www.youtube.com/watch?v=f-60_YiGBXg) with simple data overlay.



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
      <pvt:sog acc="0.542">23.542</pvt:sog>
    </pvt:ext>
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
      <pvt:sog acc="0.542">23.542</pvt:sog>
    </pvt:ext>
  </extensions>
</trkpt>
```

