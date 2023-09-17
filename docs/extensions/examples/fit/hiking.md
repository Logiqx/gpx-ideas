## GPX Extensions

### Hiking

#### Overview

Example of a hiker with a handheld GNSS receiver.

- gpx_pvt - sog + dist



#### Trackpoint

A simple trackpoint including GNSS-derived speed and total distance:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>103.92</ele>
  <time>2022-04-11T10:16:01Z</time>
  <extensions>
    <pvt:ext>
      <pvt:sog>1.842</pvt:sog>
      <pvt:dist>1234.567</pvt:dist>
    </pvt:ext>
  </extensions>
</trkpt>
```

