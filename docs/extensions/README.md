## GPX Extensions

### Basic Concepts

- Adhere to the existing GPX [standards](../standards.md)
- Identify different data categories and group all related data items into the same schema(s)
  - Use three letter abbreviations - e.g. "gpx_met.xsd" and `<met:xyz>` for meteorological data

- Avoid duplication so that a specific data item can only be stored in one way within a GPX file
  - Speed over ground (SOG) is ground speed (GS) in aviation, but they are synonymous so there should be only one way to store them in GPX
  
  - Likewise for yaw / heading, pitch / trim, and roll / bank / heel from an IMU which are just synonyms of each other
  
  - Subtle examples exist such as outside air temperature (OAT) and static air temperature (SAT) which are essentially air temperature
  
- Ensure 100% compatibility with existing GPX readers, including Garmin software such as Connect, MapSource, etc
  - See [notes](../proposal/garmin.md) from previous GPX 1.1.1 proposal describing the behaviors of Garmin products




### Diving In

There are a huge number of [activities](../landscape/activities.md) that can benefit from the use of GPS / GNSS receivers, many of which will be interested in similar sources of data.

Feel free to take a look at some simple [examples](examples/README.md) prior to looking at the extensions in more detail.

| Schema                       | Description                |
| ---------------------------- | -------------------------- |
| [gpx_pvt](gpx_pvt/README.md) | Position / velocity / time |
| [gpx_imu](gpx_imu/README.md) | Inertial measurement unit  |
| [gpx_met](gpx_met/README.md) | Meteorological             |
| [gpx_fit](gpx_fit/README.md) | Fitness                    |
| [gpx_sea](gpx_sea/README.md) | Sea / nautical             |
| [gpx_air](gpx_air/README.md) | Air / aviation             |
| [gpx_eng](gpx_eng/README.md) | Engine                     |
| [gpx_gen](gpx_gen/README.md) | Generic                    |
| [gpx_nav](gpx_nav/README.md) | Navigation - TODO          |

Don't forget to look at the [examples](examples/README.md) that have been provided for various activities; land, sea, and air. :)



### Additional Concepts

- Use of an optional "acc" attribute for elements that can provide accuracy estimates
- Use of an optional "id" attribute for elements that have multiple concurrent readings
  - Multiple tachometers; e.g. boats with two motors, helicopters, etc
  - The "id" attribute can also be used to record the same readings from multiple sensors, if required
    - Speed(s) from both a GPS / GNSS receiver and from a bike wheel
    - Heart rates from both a sports watch and a chest strap
- Sources for the sensor metrics are optional, but if provided can be in elements such as `<gpx>`, `<trk>` or `<trkseg>`
  - See [running](examples/fit/running.md) and [cycling](examples/fit/cycling.md) examples for an illustration of how that could work
- Use of file compression ("gpz" files) will significantly reduce any file storage overheads when using extensions
