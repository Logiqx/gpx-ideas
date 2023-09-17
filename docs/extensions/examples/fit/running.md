## GPX Extensions

### Running

#### Overview

Example of a runner with a sports watch, chest strap and pod.

- gpx_pvt - sog + dist
- gpx_fit - hr (watch or chest strap) + cad (watch or pod) + steps (watch or pod) + elegain



#### Trackpoint

Individual trackpoints do not need to specify the source(s) for sensor metrics:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>103.92</ele>
  <time>2022-04-11T10:16:01Z</time>
  <extensions>
    <pvt:ext>
      <pvt:sog>4.542</pvt:sog>
      <pvt:dist>1234.567</pvt:dist>
    </pvt:ext>
    <fit:ext>
      <fit:hr>145.17</fit:hr>
      <fit:cad>180.83</fit:cad>
      <fit:elegain>15.27</fit:elegain>
      <fit:steps>1500</fit:steps>
    </fit:ext>
  </extensions>
</trkpt>
```



#### Sensors

Sources for the sensor metrics are optional, but if provided would be in `<gpx>`, `<trk>` or `<trkseg>`.

```xml
<trk>
  ...
  <extensions>
    <fit:metrics>
      <fit:metric name="hr" sensor="abc" />
      <fit:metric name="cad" sensor="def" />
      <fit:metric name="steps" sensor="def" />
    </fit:metrics>
    <fit:sensors>
      <fit:sensor name="abc" type="chest">
        <fit:brand>Brand A</fit:brand>
        <fit:product>Product B</fit:product>
        <fit:model>Model C</fit:model>
      </fit:sensor>
      <fit:sensor name="def" type="pod">
        <fit:brand>Brand D</fit:brand>
        <fit:product>Product E</fit:product>
        <fit:model>Model F</fit:model>
      </fit:sensor>
    </fit:sensors>
  </extensions>
  <trkseg>
    ...
  </trkseg>
</trk>
```

n.b. The metric names and sensor types can be validated.