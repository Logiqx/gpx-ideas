## GPX Extensions

### Background

Ever since the release of GPX 1.1 there have been requests for specific types of sensor data to be included in the official GPX specification. Common requests have included things like course + speed, IMU data (e.g. heading / pitch / roll), meteorological data (e.g. air / water temperature), fitness data (e.g. heart rate / power / cadence) and nautical data (e.g. boat speed, water depth, etc).

One of the ideas mused over the years has been a standard collection of extensions for different categories of data. After investigating what is important to a runner or cyclist, versus an airplane or helicopter pilot, versus a yachtsmen it seems that a standard collection of extensions has great merit. There are many generic data items that are common to multiple activities, and there are also many bespoke data items that are activity specific.

This page proposes a standard collection of extensions which can potentially be developed into officially blessed extensions. It should be noted that these pages are simply to convey information that is likely to be important when designing the actual schemas. The content of these pages has been created off the back of some long conversations with cyclists, pilots (commercial and military) and sailors (competitive and yacht masters).



### Basic Concepts

- Identify different data categories and group all related data items into the same schema(s)
  - Use a standard system for 3 letter abbreviations - e.g. "gpx_met.xsd" and `<met:xyz>` for meteorological data
- Adhere to the existing GPX [standards](../standards.md)
- Avoid duplication so that a specific data item can only be stored in one way within a GPX file
  - Speed over ground (SOG) is called ground speed (GS) in aviation, but they are synonymous so there should be only one way to store them in GPX
  - Likewise for yaw / heading, pitch / trim, and roll / bank / heel from an IMU which are all synonymous
  - Subtle examples also exist such as outside air temperature (OAT) and static air temperature (SAT) which are essentially the true air temperature
- Ensure 100% compatibility with existing GPX readers, including Garmin software such as Connect, MapSource, etc
  - See [notes](../proposal/garmin.md) from previous GPX 1.1.1 proposal describing the behaviors of Garmin products



### Diving In

There are a huge number of [activities](../landscape/activities.md) that can benefit from the use of GPS / GNSS receivers, many of which will be interested in similar sources of data.

Feel free to take a look at some simple [examples](examples/README.md) prior to looking at the extensions in more detail.

| Schema                       | Description                |
| ---------------------------- | -------------------------- |
| [gpx_fix](gpx_fix/README.md) | Fix type                   |
| [gpx_ico](gpx_ico/README.md) | Icons                      |
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

Additional extensions worth discussion:

- Camera specific information - see [post](https://groups.io/g/gpx/message/83) from Dan on 13 Sep 2023
- Extended satellite information - azimuth, C/N<sub>0</sub>, pseudorange, doppler, carrier phase, etc



### Additional Concepts

- Use of an optional "acc" attribute for elements that can provide accuracy estimates
  - Accuracy estimates tend to be outputs of a Kalman filter so are often available for GPS / GNSS and IMU data
- Use of an optional "id" attribute for elements that have multiple concurrent readings
  - Multiple tachometers; e.g. boats with two motors, helicopters, etc
  - The "id" attribute can also be used to record the same readings from multiple sensors, if required
    - Speed(s) from both a GPS / GNSS receiver and from a bike wheel
    - Heart rates from both a sports watch and a chest strap
- Sources for the different sensor IDs are optional, but if provided would be in elements such as `<gpx>`, `<trk>` or `<trkseg>`
  - See [running](examples/fit/running.md) and [cycling](examples/fit/cycling.md) examples for an illustration of how that could work
- Use of compressed archives ("gpz" files) will significantly reduce any file storage overheads due to the use of extensions
