## GPX Extensions

### Basic Concepts

- Adhere to existing GPX [standards](../standards.md)
- Identify general categories and group similar items together in separate schemas
  - Use three letter abbreviations - e.g. "gpx_met.xsd" and `<met:xyz>` for meteorological extensions

- Maintain 100% compatibility with existing GPX readers, including Garmin software such as Connect, MapSource, etc



### Diving In

Feel free to look at some of the [examples](examples/README.md) first, prior to looking at the extensions in more detail.

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

Don't forget to look at the [examples](examples/README.md) that have been provided for various activities; land, sea, and air. :)



### Additional Concepts

- Use of an optional "id" attribute for elements have multiple concurrent readings
  - Multiple tachometers; e.g. boats with two motors, helicopters, etc
  - The "id" attribute can also be used to record the same readings from multiple sensors, if required
    - Speed(s) from both a GPS / GNSS receiver and from a bike wheel
    - Heart rates from both a sports watch and a chest strap
- Use of an optional "acc" attribute for elements that can provide accuracy estimates
- Use of file compression ("gpz" files) will significantly reduce any file storage overheads when using extensions
