## GPX Core

### Basic Concepts

- Adhere to existing GPX [standards](../standards.md)
- Backwards compatibility
  - Make life easy for existing GPX 1.1 writers
    - There are many GPX writers in the wild and adoption of GPX 1.2 should be as easy as possible
    - Do not move or remove any existing elements / attributes
      - This includes not changing the definition of `<magvar>`
    - Only a namespace change should be required for GPX 1.1 compliant files to be GPX 1.2 compliant 
  - Make life easy for existing GPX 1.0 and 1.1 readers
    - Most GPX readers do not take any noticed of the namespace, whether it refers to GPX 1.0 or 1.1
    - Most GPX readers simply ignore elements that they don't understand
    - Do not move or remove any existing elements / attributes
      - This includes not changing the definition of `<magvar>`
- Continue using the Topografix domain for GPX schema and documentation, assuming this is possible
  - Limit the potential confusion amongst GPX developers... many existing references to topografix.com in GPX files
  - See [comment](https://www.topografix.com/gpx_mailing_list.asp#pbqhps+1tskr5v@YahooGroups.com) from Dan Foster in Apr 2018, saying there is no reason for the topografix domain to become inaccessible



### Schema Changes / Additions

This document is yet to be written but some scruffy notes can be found amongst my [GPSXML](../gpsxml/additional.md) notes.

