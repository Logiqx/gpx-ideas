## GPX Extensions

#### Fitness - gpx_fit

#### Overview

Core outputs from fitness and cycling sensors / devices are commonly added to GPX files via proprietary extensions.

| Name        | Values   | Description                                                  |
| ----------- | -------- | ------------------------------------------------------------ |
| `<hr>`      | int > 0  | Heart rate in beats per minute (bpm)                         |
| `<cad>`     | >= 0     | Cycling (cadence), running (stride rate), or swimming / rowing (stroke rate) |
| `<power>`   | >= 0     | Power in watts (W)                                           |
| `<kcal>`    | >= 0     | Total energy in kilo calories (kcal)                         |
| `<elegain>` |          | Total elevation gain in meters (m)                           |
| `<steps>`   | int >= 0 | Total steps during the session                               |

Sources for the sensor metrics are optional, but if provided can be in elements such as `<gpx>`, `<trk>` or `<trkseg>` as per the examples.



#### Notes

- A universal cadence metric is included, since the term is universal across multiple sports
  - Cadence is essentially a rhythm and is measure such as steps or strokes per minute
- Energy is included to avoid the cumulative errors that might occur when converting from power
- Elevation gain is included to avoid cumulative errors



#### Example Usage

Land / Fitness

- [Running](../examples/fit/running.md)
- [Cycling](../examples/fit/cycling.md)

