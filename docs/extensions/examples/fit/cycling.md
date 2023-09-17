## GPX Extensions

### Cycling

#### Overview

Example of a cyclist with a sports watch and bike computer.

- gpx_pvt - sog (gnss or wheel) + dist (gnss or wheel)
- gpx_fit - hr (watch or chest strap) + cad + power + elegain
- gpx_met - atemp



 #### Trackpoint

Individual trackpoints do not need to specify the source(s) for sensor metrics:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>103.92</ele>
  <time>2022-04-11T10:16:01Z</time>
  <extensions>
    <pvt:ext>
      <pvt:sog>13.542</pvt:sog>
      <pvt:dist>1234.567</pvt:dist>
    </pvt:ext>
    <fit:ext>
      <fit:hr>145.17</fit:hr>
      <fit:cad>90.57</fit:cad>
      <fit:power>250.86</fit:power>
      <fit:elegain>15.27</fit:elegain>
    </fit:ext>
    <met:ext>
      <met:atemp>20.15</met:atemp>
    </met:ext>
  </extensions>
</trkpt>
```



#### Sensors

Sources for the sensor metrics are optional, but if provided would be in `<gpx>`, `<trk>` or `<trkseg>`.

```xml
<trk>
  ...
  <extensions>
    <pvt:metrics>
      <pvt:metric name="sog" sensor="xyz" />
      <pvt:metric name="dist" sensor="xyz" />
    </pvt:metrics>
    <pvt:sensors>
      <pvt:sensor name="xyz" type="wheel">
        <pvt:brand>Brand X</pvt:brand>
        <pvt:product>Product Y</pvt:product>
        <pvt:model>Model Z</pvt:model>
      </pvt:sensor>
    </pvt:sensors>
    <fit:metrics>
      <fit:metric name="hr" sensor="abc" />
      <fit:metric name="cad" sensor="def" />
      <fit:metric name="power" sensor="def" />
    </fit:metrics>
    <fit:sensors>
      <fit:sensor name="abc" type="chest">
        <fit:brand>Brand A</fit:brand>
        <fit:product>Product B</fit:product>
        <fit:model>Model C</fit:model>
      </fit:sensor>
      <fit:sensor name="def" type="crank">
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
