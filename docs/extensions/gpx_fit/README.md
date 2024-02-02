## GPX Extensions - Fitness

### Overview

Core outputs from fitness and cycling sensors / devices are commonly added to GPX files via proprietary extensions.

| Name        | Values   | Description                                                  |
| ----------- | -------- | ------------------------------------------------------------ |
| `<hr>`      | int > 0  | Heart rate in beats per minute (bpm)                         |
| `<spo2>`    | 0-100    | SpO2 (oxygen saturation) as a percentage (%)                 |
| `<cad>`     | >= 0     | Cycling (cadence), running (stride rate), or swimming / rowing (stroke rate) |
| `<power>`   | >= 0     | Power in watts (W)                                           |
| `<energy>`  | >= 0     | Total energy in kilo calories (kcal)                         |
| `<elegain>` |          | Total elevation gain in meters (m)                           |
| `<steps>`   | int >= 0 | Total steps during the session                               |

Sources for these metrics are optional, but if provided would be in elements such as `<gpx>`, `<trk>` or `<trkseg>` as per the examples.



### Notes

- A universal cadence metric is included in this extension, since the word "cadence" is universal across multiple sports
  - Cadence is essentially a rhythm and is typically measure of how many times something happens (e.g. steps, strokes) in a minute
- Energy is included to avoid the cumulative errors that might occur when converting from power readings
- Elevation gain is included to avoid cumulative errors



### Example Usage

Land / Fitness

- [Running](../examples/fit/running.md)
- [Cycling](../examples/fit/cycling.md)

