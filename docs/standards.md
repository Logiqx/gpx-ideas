## GPX Ideas

### Standards

A number of GPX standards currently exist.
- Sequenced elements using `<xsd:sequence>`
- Lowercase element names to reduce the risk of inconsistencies and typos
- Short and concise element names wherever possible
  - e.g. `<ele>` for elevation
- Metric units such as m, m/s, deg/min, etc
- Mandatory information must be stored as XML attributes with a schema stating `use="required"`
  - e.g. `<trkpt lat="50.5710623" lon="-2.4563484">`
  - Future XML attributes need not be mandatory imho, despite the existing XML attributes stating `use="required"`
- General guidance to developers
  - XML writers
    - "Protect other applications from yours by validating test files from your application against the schema."
    - Do not include unknown elements when writing GPX files - e.g. if elevation is unknown, do not include `<ele>0</ele>`
    - Do not calculate unknown elements when writing GPX files - e.g. if speed is unavailable, do not calculate it from lat + lon
  - XML readers
    - "Protect your application against schema changes by ignoring unknown elements."
    - This applied to XML elements and attributes that are not recognised
- Everything within a GPX / extension schema should be self-documenting via `<xsd:documentation>` and `<xsd:annotation>`

