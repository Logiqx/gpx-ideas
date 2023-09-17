## GPX Extensions

The examples below are simply to illustrate how different activities might use different extensions.

It may be worth considering whether some (or all) of the PVT elements should be in the GPX 1.2 schema because they are so common:

e.g. cog + sog could be added to GPX 1.2, making them available to existing software that recognises them in GPX 1.0 files



### Fitness Examples

#### Hiking

Example of a hiker with a handheld GNSS receiver and GPX 1.1:

- gpx_pvt - sog + dist

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



#### Running

Example of a runner with a sports watch, chest strap and pod.

- gpx_pvt - sog + dist
- gpx_fit - hr (watch or chest strap) + cad (watch or pod) + steps (watch or pod) + elegain

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

Sources for the sensor metrics would be in the `<gpx>`, `<trk>` or `<trkseg>`:

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



#### Cycling

Example of a cyclist with a sports watch and bike computer.

- gpx_pvt - sog (gnss or wheel) + dist (gnss or wheel)
  
- gpx_fit - hr (watch or chest strap) + cad + power + elegain
- gpx_met - atemp

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

Sources for the sensor metrics would be specified in the `<gpx>`, `<trk>` or `<trkseg>`:

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



### Nautical Examples

#### GPS Speedsailing

Example of a windsurfer with a custom GNSS receiver.

- gpx_pvt - cog + sog

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

Short [video](https://www.youtube.com/watch?v=f-60_YiGBXg) with simple data overlay.



#### Dinghy Racing

Example of a sailing dinghy with a custom GNSS training / racing instrument.

- gpx_pvt - cog + sog
- gpx_imu - head, trim (pitch), heel (roll)

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

Current Sailmon outputs (CSV):

- Time + latitude + longitude
- HDT + SOG + COG
- TWA + TWD (both require an airspeed sensor)
- Heel + Trim
- Satellites + hAcc

See short [video](https://www.youtube.com/watch?v=hpqvp6MbXAQ) with data overlay at 1:28



#### Yachting

Example of a sailing yacht with a chartplotter / fish finder with external sensors - e.g. boat / water speed, temperature, depth.

- gpx_pvt - cog + sog
- gpx_imu - head, trim (pitch), heel (roll)
- gpx_sea - awa, aws, twa, tws, stw, 
- gpx_met - gwd, gws, atemp, wtemp

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
      <imu:head>275.23</imu:head>
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

Short [video](https://www.youtube.com/watch?v=14TYwonISH0) with data overlays.



### Aviation Examples

#### Skydiver

Example of a skydiver with a custom GNSS receiver + INS device (optional).

- gpx_pvt - cog + sog + roc
- gpx_imu (optional) - head, pitch, roll

GPX 1.1 example:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>1007.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <sats>29</sats>
  <extensions>
    <pvt:ext>
      <pvt:cog acc="10.0">157.19</pvt:cog>
      <pvt:sog acc="0.542">30.542</pvt:sog>
      <pvt:roc acc="0.781">50.678</pvt:roc>
    </pvt:ext>
    <imu:ext>
      <imu:head>275.23</imu:head>
      <imu:roll>5.25</imu:roll>
      <imu:pitch>-10.15</imu:pitch>
    </imu:ext>
  </extensions>
</trkpt>
```

GPX 1.2 will allow for horizontal and vertical accuracy estimates:

```xml
<trkpt lat="50.5710623" lon="-2.4563484" acc="1.937">
  <ele acc="2.754">1007.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <sats>29</sats>
  <extensions>
    <pvt:ext>
      <pvt:cog acc="10.0">157.19</pvt:cog>
      <pvt:sog acc="0.542">30.542</pvt:sog>
      <pvt:roc acc="0.781">50.678</pvt:roc>
    </pvt:ext>
    <imu:ext>
      <imu:head>275.23</imu:head>
      <imu:roll>5.25</imu:roll>
      <imu:pitch>-10.15</imu:pitch>
    </imu:ext>
  </extensions>
</trkpt>
```

Short [video](https://www.youtube.com/watch?v=KBQXuzfNWjE) with custom GPS providing audio feedback.



#### Microlight

Example of a microlight with a custom GNSS receiver + INS device, air speed indicator and altitude indicator.

- gpx_pvt - cog + sog + roc
- gpx_imu - head, pitch, bank (roll)
- gpx_air - ias, alt

GPX 1.1 example:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>507.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <sats>29</sats>
  <extensions>
    <pvt:ext>
      <pvt:cog acc="10.0">157.19</pvt:cog>
      <pvt:sog acc="0.542">30.542</pvt:sog>
      <pvt:roc acc="0.781">5.678</pvt:roc>
    </pvt:ext>
    <imu:ext>
      <imu:head>275.23</imu:head>
      <imu:roll>15.25</imu:roll>
      <imu:pitch>10.15</imu:pitch>
    </imu:ext>
    <air:ext>
      <avt:ias>50.678</avt:ias>
      <air:ialt set="1023.85" ref="qnh">518.271</air:ialt>
    </air:ext>
  </extensions>
</trkpt>
```

GPX 1.2 will allow for horizontal and vertical accuracy estimates:

```xml
<trkpt lat="50.5710623" lon="-2.4563484" acc="1.937">
  <ele acc="2.754">507.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <sats>29</sats>
  <extensions>
    <pvt:ext>
      <pvt:cog acc="10.0">157.19</pvt:cog>
      <pvt:sog acc="0.542">30.542</pvt:sog>
      <pvt:roc acc="0.781">5.678</pvt:roc>
    </pvt:ext>
    <imu:ext>
      <imu:head>275.23</imu:head>
      <imu:roll>15.25</imu:roll>
      <imu:pitch>10.15</imu:pitch>
    </imu:ext>
    <air:ext>
      <avt:ias>50.678</avt:ias>
      <air:ialt set="1023.85" ref="qnh">518.271</air:ialt>
    </air:ext>
  </extensions>
</trkpt>
```



#### Light Aircraft

Example of a light aircraft with a GNSS receiver and standard cockpit indicators; traditional steam engine or glass cockpit.

- gpx_pvt - cog + sog + roc
- gpx_imu - head, rot, pitch, bank (roll)
- gpx_air - ias, tas, alt, agl, slip
- gpx_met - atemp, baro

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>10007.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <sats>29</sats>
  <extensions>
    <pvt:ext>
      <pvt:cog>157.19</pvt:cog>
      <pvt:sog>230.542</pvt:sog>
      <pvt:roc>5.678</pvt:roc>
    </pvt:ext>
    <imu:ext>
      <imu:head>275.23</imu:head>
      <imu:rot>183.98</imu:rot>
      <imu:roll>15.25</imu:roll>
      <imu:pitch>10.15</imu:pitch>
    </imu:ext>
    <air:ext>
      <air:ias>80.678</air:ias>
      <air:tas>87.456</air:tas>
      <air:ialt set="1013.25" ref="std">5038.271</air:ialt>
      <air:agl>4912.372</air:agl>
      <air:slip>1.27</air:slip>
    </air:ext>
    <met:ext>
      <met:atemp>-17.47</met:atemp>
      <met:baro>500.38</met:baro>
    </met:ext>
  </extensions>
</trkpt>
```



### Miscellaneous Examples

#### Weather Station

Example of a weather station.

- gpx_pvt - cog + sog
- gpx_imu - head, rot, pitch, roll
- gpx_sea - awa, aws
- gpx_met - gwd, gws, atemp, wtemp, baro, hum

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>1.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <sats>29</sats>
  <extensions>
    <pvt:ext>
      <pvt:cog>157.19</pvt:cog>
      <pvt:sog>0.542</pvt:sog>
    </pvt:ext>
    <imu:ext>
      <imu:head>275.23</imu:head>
      <imu:rot>3.98</imu:rot>
      <imu:roll>1.25</imu:roll>
      <imu:pitch>1.15</imu:pitch>
    </imu:ext>
    <sea:ext>
      <sea:awa>20.15</sea:awa>
      <sea:aws>4.23</sea:aws>
    </sea:ext>
    <met:ext>
      <met:atemp>15.37</met:atemp>
      <met:wtemp>6.89</met:wtemp>
      <met:gwd>20.46</met:gwd>
      <met:gws>4.67</met:gws>
      <met:baro>1013.89</met:baro>
      <met:hum>89.23</met:hum>
    </met:ext>
  </extensions>
</trkpt>
```
