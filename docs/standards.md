## GPX Ideas

### Standards

- Existing GPX standards
  - Sequenced elements
  - Lowercase element names
  - Short + concise element names
    - e.g. `<atemp>` and `<wtemp>` for air + water temperature
  - Metric units - m, m/s, deg/min, etc
  - Mandatory information relating to XML elements must be stored as attributes.
    - However, XML attributes themselves need not be mandatory.
  - Guidance
    - Do not include unknown elements when writing GPX files - e.g. if heartrate is unknown, do not include `<fit:hr>0</fit:hr>`
    - Do not calculate unknown elements when writing GPX files - e.g. if speed is unavailable, do not calculate it from lat + lon
  - Everything should be self-documenting via xsd:documentation and xsd:annotation tags

