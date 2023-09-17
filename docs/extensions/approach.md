## GPX Proposal

### History

Back in 2004 the general consensus was that GIS and presentational hints (line styles, polygons, text, symbols, GIS) should be outside of the main GPX schema. This resulted in two official extensions being created:
- gpx_style
- gpx_overlay

There was also talk about a GPX 2.0 a couple of times, which would be much lighter than 1.2 and use addon schemas. 

- azbithead+gmail.com on Wed Nov 24 15:15:36 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#co34m5+isio@eGroups.com))
  - "It is my opinion that GPX already has too much stuff in it. I'd like to see GPX 2.0 made lighter and new add-on schemas developed for related uses."
- egroups+topografix.com on Sun Jan 27 11:05:30 2008 ([link](https://www.topografix.com/gpx_mailing_list.asp#1787503072.20080127140526@topografix.com))
  - "I would like to see a dozen or so officially-blessed extension schemas created to extend the base GPX 2.0 schema in different directions. I'd like to see a commitment from developers using the GPX format to develop common "officially-blessed" schemas for data that might have a use in other hardware or software applications, and to only use private schemas for truly private data that has no meaning outside of that developer's application."
- ptomblin+gmail.com on Tue Jun 23 18:58:19 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#8efd35820906231855r3ecdee3eodcedbfffc8c2c@mail.gmail.com))
  - "Maybe the solution isn't a new GPX, but some sort of standard library of extensions.  I have a pretty decent (in my opinion) GPX extension schema for aviation waypoint data, and I'd be really disappointed if somebody who needed similar but slightly different data would design their own extension schema instead of cooperating with me to extend mine."
- robertlipe+usa.net on Wed Jun 24 12:42:05 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#886NFXTOd6348S17.1245872489@cmsweb17))
  - "I'm reluctant to turn GPX into the kitchen sink.  Ask a runner and a sailor what's important to each of them and they'll give opposite answers and then declare the other half as "obvious bloat", much as you just did."
  - "I'm liking the small core kernel of GPX, a blessed set of extensions for the things that are common now (direction and tilt, temperature, etc.), and the use of the `<extensions>` tag for domain-specific problems that can be integrated into "blessed" status once they get enough exposure to be proven to be workable and useful."

  - "Once those extensions have been implemented by enough programs to be proven useful, they can be frozen in future versions of GPX itself."

  - "It seems a pretty natural progression: experimental->one program->several programs->a proposed GPX extension->a holy GPX extension->official GPX."



### Concepts

- Stick to existing standards
  - Sequenced elements
  - Lowercase element names
  - Short + concise element names
  - Metric units - m, m/s, deg/min, etc
  - Do not include unknown elements when writing GPX files - e.g. if heartrate is unknown, do not include `<fit:hr>0</fit:hr>`
  - Do not calculate unknown elements when writing GPX files - e.g. if speed is unavailable, do not calculate it from lat + lon
  - Mandatory information relating to XML elements must be stored as attributes. However, XML attributes themselves need not be mandatory.
  - Everything should be self-documenting via xsd:documentation and xsd:annotation tags
- Extensions for GPX 1.1
  - Identify general categories and group similar items together in separate schemas
    - I will not touch aviation (Paul Tomblin's work) or change gpx_style / gpx_overlay
  - Use three letter abbreviations - e.g. "gpx_met.xsd" and `<met:xyz>` for meteorological extensions
  - Use optional "id" attribute for elements that can repeat multiple times (e.g. fuel gauges, tachometer)
    - n.b. GPX 1.0 and GPX 1.1 uses attributes for mandatory data, but has not specified optional attributes
  - Propose inclusion of the course and speed into the core schema of GPX 1.2
- Backwards compatibility of GPX 1.2
  - Make it easy for existing GPX 1.1 writers
    - There are many GPX writers in the wild and adoption of GPX 1.2 should be as easy as possible
    - Do not move or remove any existing elements / attributes
      - This includes not changing the definition of `<magvar>`
    - Only a namespace change should be required for GPX 1.1 compliant files to become GPX 1.2 conformant
  - Make it easy for GPX 1.0 and 1.1 readers
    - Most GPX readers do not take any noticed of the namespace, whether it suggests GPX 1.0 or 1.1
    - Most GPX readers simply ignore elements that they don't understand
    - Do not move or remove any existing elements / attributes
      - This includes not changing the definition of `<magvar>`
    - Re-use the GPX 1.0 names for "course" and "speed"
- Continue using Topografix domain for schema and documentation
  - Minimise potential confusion amongst developers... many existing references to topografix.com in GPX files
  - See [comment](https://www.topografix.com/gpx_mailing_list.asp#pbqhps+1tskr5v@YahooGroups.com) from Dan Foster in Apr 2018, saying there is no reason for the topografix domain to become inaccessible
  



### Extensions

TODO - move these comments into individual schema rationale documents

- Course
  - Sometimes referred to as course over ground (COG) or course made good (CMG)
  - Sometimes referred to track or track made good (TMG)
- Temperature
  - Air temperature - atemp
  - Water temperature - wtemp
- Cadence
  - Cyclists call it "pedalling rate" , measured in rpm.
    - It's the number of revolutions the pedals make per minute
    - Not to be confused with the rotational rate of the wheel
  - Runners call it "strike rate", measured in steps per minute
    - Just for clarity, it is the number of single steps per minute
  - Swimmers call "stroke rate", measured in strokes per minute
    - Just for clarity, it is the number of single strokes per minute
- Reps
  - Steps
  - Strokes
  - Jumps



### GPX 2.0

- Changes to main schema
  - New trkptType
    - Addition of course and speed
  - Additional fix types - "rtk", "float", etc
  - All complex types should support `<extensions>`
  - Allow relative paths in `<link>` elements, or is this already possible?
  - Extended src elements - maybe, I'm starting to think extensions
- Apply to `<wpt>`, `<rtept>` and `<trkpt>` elements
  - Recording real-time sensor readings in waypoints:
    - e.g. snapshot of speed / cadence / heart rate during a marathon

  - Targets / benchmarks within routes:
    - e.g. target speed / cadence / heart rate during a run



### TBC

- Consider two independent releases:
  - GPX 1.1 extensions
    - Lacks some of the possible improvements to the core GPX schema
    - 100% compatible with existing GPX readers, including Garmin software (Connect, MapSource, etc)
    - File compression using the GPZ standard
  - GPX 1.2, also supporting the GPX 1.1 extensions
    - Incorporate some or all of the PVT extension into the core GPX schema
    - Implement all of the "worthwhile" improvements to the core GPX schema
    - File compression using the GPZ standard

