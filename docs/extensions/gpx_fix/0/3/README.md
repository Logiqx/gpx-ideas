## GPX Extensions

### gpx_fix/0/3

Links to the provisional schema (XSD), plus examples (GPX) reflecting the original [proposal](../../README.md) are available:

- [gpx_fix.xsd](gpx_fix.xsd)
- [examples.gpx](examples.gpx)



### Change History

#### 0.3

- Add GNSS signals, replacing frequency bands.
- Add SBAS element after the existing GNSS elements.
  - SBAS observables (pseudo-range, doppler, carrier) can be used in PVT solutions.

- Change validation within extensions from "lax" to "strict".
- Tweak comments for extensions.
- Remove blank lines within complex types, hopefully improving readability.

#### 0.2

- Add GNSS elements - GPS, GLONASS, Galileo, BeiDou, QZSS, NavIC.

#### 0.1

- Initial draft.

