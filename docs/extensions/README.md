## GPX Ideas

### GPX Extensions

#### Basic Concepts

- Adhere to existing GPX [standards](../standards.md)
- Identify general categories and group similar items together in separate schemas
- Use three letter abbreviations - e.g. "gpx_met.xsd" and `<met:xyz>` for meteorological extensions
- 100% compatible with existing GPX readers, including Garmin software such as Connect, MapSource, etc



#### Diving In

Feel free to look at some of the [examples](examples/README.md) first, prior to looking at the finer details of the extensions.

| Schema                       | Description                |
| ---------------------------- | -------------------------- |
| [gpx_pvt](gpx_pvt/README.md) | Position / velocity / time |
| [gpx_imu](gpx_imu/README.md) | Inertial measurement unit  |
| [gpx_met](gpx_met/README.md) | Meteorological             |
| [gpx_fit](gpx_fit/README.md) | Fitness                    |
| [gpx_air](gpx_air/README.md) | Air / aviation             |
| [gpx_sea](gpx_sea/README.md) | Sea / nautical             |
| [gpx_nav](gpx_nav/README.md) | Navigation                 |
| [gpx_eng](gpx_eng/README.md) | Engine                     |
| [gpx_gen](gpx_gen/README.md) | Generic                    |

Don't forget to look at the [examples](examples/README.md) for various activities; land, sea, and air. :)



#### Additional Concepts

- Use of optional "id" attribute for elements that can repeat multiple times (e.g. fuel gauges, tachometers, etc)
- Use of optional "acc" attribute for elements that sometimes have accuracy estimates.
