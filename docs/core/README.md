## GPX 1.2

### Background

In addition to the proposal for a collection of officially blessed GPX [extensions](../extensions/README.md) there are several possible enhancements that can be made to the core GPX schema. This page lists possible enhancements and how they might be implemented in a way that is beneficial and non-disruptive. If these improvements are implemented it would essentially be GPX 1.2 but with a strong emphasis on compatibility with GPX 1.1.



### Basic Concepts

- Implement worthwhile schema enhancements to produce GPX 1.2 
- Adhere to the existing GPX [standards](../standards.md)
- Ensure backwards compatibility with GPX 1.1
  - Make life easy for existing GPX 1.1 writers
    - There are many GPX writers in the wild, so adoption of GPX 1.2 should be as easy as possible
      - Do not rename, move or remove any existing elements / attributes
      - Do not make changes to the schema that will cause compatibility issues
    - Only a namespace change should be required for GPX 1.1 compliant files to be GPX 1.2 compliant
      - The only exception is that `<magvar>` will need to use values between -180 and 180
  - Make life easy for existing GPX 1.0 and 1.1 readers
    - Most GPX readers do not take any notice of the namespace, whether it refers to GPX 1.0 or 1.1
    - Most GPX readers simply ignore elements that they don't understand
    - Do not rename, move or remove any existing elements / attributes
- Continue using the Topografix domain for GPX schema and documentation, assuming this is possible
  - Limit the potential confusion amongst GPX developers... many existing references to topografix.com in GPX files
  - See [comment](https://www.topografix.com/gpx_mailing_list.asp#pbqhps+1tskr5v@YahooGroups.com) from Dan Foster in Apr 2018, saying there is no reason for the topografix domain to become inaccessible



### Possible Improvements

There are a number of changes and additions that can potentially be included in GPX 1.2

- Add track type - e.g. walking, running, cycling, driving, sailing, flying, etc.
  - It might be best to do this as an extension so the list of track types can be extended, without requiring future GPX releases
- Add accuracy horizontal / vertical position and time accuracy estimates to `<trkpt>` `<rtept>` `<wpt>` elements
  - See the [gpx_pvt](../extensions/gpx_pvt/README.md) proposal for further details
- Add missing fix types
  - See separate [page](fix-type.md) for full details
- Add display color
  - Provide a standard way to specify display colors for tracks, routes and waypoints - see [GpxExtensionsv3.xsd](https://www8.garmin.com/xmlschemas/GpxExtensionsv3.xsd)
- Add UUID
  - Maybe consider introducing `<uuid>` elements everywhere that `<src>` elements are currently allowed?
- Improvements to complex types
  - All complex types should support `<extensions>`
    - This applies to copyrightType, linkType, emailType, personType, ptType, ptsegType, boundsType
  - Change `<src>` elements to be a complex type
    - This will allow more detailed / structured information to be stored in `<src>` elements via `<extensions>`
  - Create a base definitions schema that can be referenced by the gpx, gpx_style and gpx_overlay schemas
    - See [post](https://stackoverflow.com/questions/8194112/basics-of-referencing-a-xsd-schema-from-another-schema/8197798#8197798) which describes the use of relative paths in schema locations
- Add support for relative paths to `<link>` elements which will be useful for GPZ files with embedded icons / images, etc
  - The "href "attribute of `<link>` elements is currently defined as "xsd:anyURI" so it expects a valid URI
- Enforce "strict" validation of elements within `<extensions>`
  - Change `<extensions>` from "lax" validation to "strict" validation
- Fix the definition of `<magvar>`
  - Magnetic variation should really be -180 and 180, but is defined as 0 to 360 in the GPX 1.0 and 1.1 schemas
- Standard use of whitespace
  - The GPX schema currently uses a mixture of tabs and spaces for indentation. Perhaps use 2 spaces instead of tabs?
- XSD documentation tweaks
  - Clarification about `<ele>` which is the "WGS84 orthometric height (relative to MSL)" for elevation and altitude
    - See useful [links](../elevation.md) and "Definition of `<ele>` is unclear" discussion on [Github](https://github.com/Logiqx/gpx-ideas/discussions/1) for more information
  - Clarification about the use of WGS84
    - See "WGS84" discussion on [Github](https://github.com/Logiqx/gpx-ideas/discussions/2) for more information
  - Make it clear that latitude and longitude values should not provide more than 9 decimal places
