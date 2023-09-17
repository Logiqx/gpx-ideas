## GPX Ideas

### GPX 1.2

These items need amalgamating with the content of the [GPSXML](../gpsxml/additional.md) notes:

- Changes to main schema
  - Additional fix types - "rtk", "float", etc
  - All complex types should support `<extensions>`
  - Allow relative paths in `<link>` elements, or is this already possible?
  - Extended src elements - maybe, I'm starting to think extensions
- Apply to `<wpt>`, `<rtept>` and `<trkpt>` elements
  - Recording real-time sensor readings in waypoints:
    - e.g. snapshot of speed / cadence / heart rate during a marathon

  - Targets / benchmarks within routes:
    - e.g. target speed / cadence / heart rate during a run

