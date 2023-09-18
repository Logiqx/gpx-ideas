## GPX Extensions

### Microlight

#### Overview

Example of a microlight with a custom GNSS receiver + INS device, air speed indicator and altitude indicator.

- gpx_pvt - cog + sog + roc, plus accuracy estimates
- gpx_imu - hdg, pitch, bank (roll)
- gpx_air - ias, alt



#### Trackpoint

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
      <imu:hdg>275.23</imu:hdg>
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
      <imu:hdg>275.23</imu:hdg>
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
