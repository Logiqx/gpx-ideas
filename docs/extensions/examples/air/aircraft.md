## GPX Extensions

### Light Aircraft

#### Overview

Example of a light aircraft with a GNSS receiver and standard cockpit indicators; traditional "steam engine" indicators or glass cockpit.

- gpx_pvt - cog + sog + roc
- gpx_imu - head, rot, pitch, bank (roll)
- gpx_air - ias, tas, alt, agl, slip
- gpx_met - atemp, baro



 #### Trackpoint

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