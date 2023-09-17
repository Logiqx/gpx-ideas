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
  - Additional XML attributes need not be mandatory, despite all existing XML attributes stating `use="required"`
- General guidance
  - XML writers
    - "Protect other applications from yours by validating test files from your application against the schema."
    - Do not include unknown elements when writing GPX files - e.g. if heartrate is unknown, do not include `<fit:hr>0</fit:hr>`
    - Do not calculate unknown elements when writing GPX files - e.g. if speed is unavailable, do not calculate it from lat + lon
  - XML readers
    - "Protect your application against schema changes by ignoring unknown elements."
- Everything within a GPX / extension schema should be self-documenting via `<xsd:documentation>` and `<xsd:annotation>`

