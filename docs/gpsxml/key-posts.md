## GPX Developers Mailing List and GPSXML Archive

### History of GPX

- [History of GPXML, timeline](https://www.topografix.com/gpx_mailing_list.asp#g8uv4i+5rs9@eGroups.com) by Doug A, Aug 2008
  - "I'm writing an article that documents the history of exchanging GPS data.  And I could use some help filling in significant events in the GPX timeline."



### GPX 1.0

- [Things we can agree on?](https://www.topografix.com/gpx_mailing_list.asp#9418153312.20011029175959@topografix.com) - Dan Foster, 29 Oct 2001
  - To be a "compliant GPX application", a program must only be able to read any GPX file without crashing.  There is no requirement to actually parse and import any or all of the data in the file.  Any tag can be ignored by the application.  However, any program that produces an error on well-formed GPX data is not compliant.   We'll have a suite of test files from various applications for everyone to test against for compliance.
  - The Metric system is to be used for all applicable units. (meters for altitude, for example).
- [Schema - first go](https://www.topografix.com/gpx_mailing_list.asp#001b01c1764f$3f9a8630$fc00a8c0@krlap) by Kevin Read, 25 Nov 2001
  - "Here's a quick first draft of the XSD for .gpx - I have also placed it in the files section of yahoogroups.com"
- [Schema Rel Candidate 1.0](https://www.topografix.com/gpx_mailing_list.asp#001501c1850c$f752e030$fc00a8c0@krlap) by Kevin Read, 14 Dec 2001
  - "Draft #2 of the Release candidate for the Schema"
- [Are Schemas required in GPX?](https://www.topografix.com/gpx_mailing_list.asp#a1oiuf+a9ka@eGroups.com) -  Dave W, 11 Jan 2002
  - "I'll accept Dan's offer to maintain and explain, or at least host, the schema"
- [Finishing up GPX 1.0](https://www.topografix.com/gpx_mailing_list.asp#004101c1ab89$ae5d1690$1900a8c0@krlap) by Kevin Read, 1 Feb 2002
  - Regarding the user of lower case element names
- [Including app specific data in `<gpx>`](https://www.topografix.com/gpx_mailing_list.asp#a9aa47+k9hq@eGroups.com) - Dave W, 13 Apr 2002
  - Schemas, namespaces, extensions in GPX 1.0



GPSml was also mentioned a few times, put not directly related to GPX:

- [GPSml first public version posted](https://www.topografix.com/gpx_mailing_list.asp#3C55C96D.17138.CDDF5674@localhost) by Andrzej Jan Taramina, 28 Jan 2002



### GPX 1.1

- [Proposed schemas for specifying colors, fonts, and sizes for text and polygons on maps](https://www.topografix.com/gpx_mailing_list.asp#910366965.20030812165539@topografix.com) - Dan Foster, 12 Aug 2003
  - gpx_style and gpx_overlay schemas, plus the first changes that went into GPX 1.1
- [GPX 1.1 metadata sample file](https://www.topografix.com/gpx_mailing_list.asp#180480177.20040610081437@topografix.com) - Dan Foster, 10 Jun 2004
  - "Here's some sample output from ExpertGPS."
- [GPX 1.1 documentation](https://www.topografix.com/gpx_mailing_list.asp#573222960.20040728144207@topografix.com) - Dan Foster, 28 Jul 2004
  - "I've made some stylistic changes to the GPX 1.1 schema, and used xsd:annotation to add documentation to the schema document itself."
- [GPX 1.1 schema released!](https://www.topografix.com/gpx_mailing_list.asp#16710466593.20040809122848@topografix.com) - Dan Foster, 9 Aug 2004
  - "I've updated the GPX Web site to point to the new GPX 1.1 schema and documentation."
- [GPX 1.1 `<extensions>` allows broken GPX to validate](https://www.topografix.com/gpx_mailing_list.asp#124423616.20050119080422@topografix.com) - Dan Foster, 19 Jan 2005
  - "I've created a GPX 1.2 namespace with this single change so that I could continue testing my instance documents correctly.  Feel free to use it for your own testing, but be sure to switch back to GPX 1.1 namespace before releasing software."
- [More problems with GPX 1.1 and multiple namespaces](https://www.topografix.com/gpx_mailing_list.asp#197383556.20050121114718@topografix.com) - Dan Foster, 21 Jan 2005
  - Describes strict validation and Garmin MapSource import
  - Note subsequent comment about mixing SVG or XHTML
    - egroups+topografix.com on Fri Jan 21 11:40:38 2005 ([link](https://www.topografix.com/gpx_mailing_list.asp#23758964.20050121144123@topografix.com))



### Styling

Line colours, polygons, text:

- [Support for Polygon features](https://www.topografix.com/gpx_mailing_list.asp#000901c3602e$6cc07460$84a79642@groundspeak.biz) - Jeremy Irish, 11 Aug 2003
  - "GPX is XML for Global Positioning Systems. GML is for what you're looking for. I'm sure you could combine the two schemas to get your intended result."
- [Line Type Styles for Tracks](https://www.topografix.com/gpx_mailing_list.asp#1819745382.20041111133343@topografix.com) - Dan Foster, 11 Nov 2004
  - "I think there's general agreement (if silence can be interpreted to be agreement) that line styles ought to be broken out into their own namespace to avoid cluttering up the base GPX definition."
- [Representing shapes, lines, and text notes that aren't destined for the GPS](https://www.topografix.com/gpx_mailing_list.asp#1772492287.20041123135521@topografix.com) - Dan Foster, 23 Nov 2004
  - "I'm trying to solve the "green line" issue in a generic way that can be quickly understood and implemented by anyone."
- [Confusion over the term "GPX"?](https://www.topografix.com/gpx_mailing_list.asp#1414556792.20041124203120@topografix.com) - Dan Foster, 24 Nov 2004
  - "Nobody is suggesting that GIS go into the GPX schema.  It doesn't belong there.  It belongs in an external schema.  We all agree on this."
- [gpx_style extension schema](https://www.topografix.com/gpx_mailing_list.asp#co8olb+922q@eGroups.com) - Dan Foster, 6 Dec 2004
  - "There seems to be general consensus that an external schema for adding map presentation hints to GPX files is a good idea."
- [GPX Overlay and Style schema updated](https://www.topografix.com/gpx_mailing_list.asp#625504761.20050119143522@topografix.com) - Dan Foster, 19 Jan 2005
  - "I've updated the gpx_overlay and gpx_style schemas to reflect the comments you all made on the prior attempt.  I made some further changes based on issues that arose when I tried to implement most of gpx_overlay in ExpertGPS."



### GPX 2.0

- [GPX 2.0](https://www.topografix.com/gpx_mailing_list.asp#co0v4n+e4i5@eGroups.com) - feedback+gpxchange.com, 23 Nov 2004 - read whole thread
  - Dan Foster mentioned gpx_style and gpx_overlay for use with GPX 1.1
  - Steve Hales (Garmin) expressed opinion that GPX is too heavy and would like GPX 2.0 made lighter, using add-on schemas



### Miscellaneous

- [Newbie question: decimal precision](https://www.topografix.com/gpx_mailing_list.asp#cjt0b6+9ida@eGroups.com) - Dave W, 4 Oct 2004
  - Historical definition of 1 meter, which is 0.000009 degrees.
  - "6 decimal places would give you accuracy down to about 10 centimeters, or four inches, which is probably good enough."
- [schemaLocation required?](https://www.topografix.com/gpx_mailing_list.asp#6103930504111716584abe4aa2@mail.gmail.com) - Steve Hales (Garmin), 17 Nov 2004 - read whole thread about future interoperability
  - "Dan Foster and I have been having a discussion via email regarding the schemaLocation attribute in GPX instance documents."
  - "At Garmin, we believe it is a very good thing and MapSource does validation when it reads GPX documents"
- [More problems with GPX 1.1 and multiple namespaces](https://www.topografix.com/gpx_mailing_list.asp#ctr3di+r3a7@eGroups.com) - Steve Hales (Garmin), 2 Feb 2005
  - Detailed explanation of the Garmin validation and parsing
- Final [post](https://www.topografix.com/gpx_mailing_list.asp#d2vmbo+n0qk@eGroups.com) - Dave W, 5 Apr 2005
  - Still engaged but subsequently disappeared, prior to joining Garmin
- [Garmin MapSource GPX 1.1 extensions](https://www.topografix.com/gpx_mailing_list.asp#d60mlb+dsnq@eGroups.com) - Steve Hales (Garmin), 12 May 2005
  - "If you are interested in the MapSource-specific extensions to GPX 1.1, the schema is available" - [GpxExtensionsv1.xsd](http://www.garmin.com/xmlschemas/GpxExtensions/v1/GpxExtensionsv1.xsd)
  - Quickly superseded by GpxExtensionsv2.xsd and GpxExtensionsv1.xsd was removed from the Garmin website
- [Date/Time in a GPX File](https://www.topografix.com/gpx_mailing_list.asp#20051003191823.GD27276@rjloud.sco.com) by Robert Lipe, Oct 2005
  - "You could adjust the time to some _other_ timezone, as long as you specify the correct offset. Stylistically, I prefer busting everything to GMT"
- [Extensions for heart rate/cadence data?](https://www.topografix.com/gpx_mailing_list.asp#827082229.20061023151028@topografix.com) - Dan Foster, Oct 2006
  - "As long as there's an effort going on to standardize on a schema for heart rate and other measured values along a track, I'd like to see temp and depth considered as well."
- [POI/Waypoint Phone Number Attribute](https://www.topografix.com/gpx_mailing_list.asp#1103712371.20061203122858@topografix.com) by Dan Foster, Dec 2006
  - "There seems to be a common mis-understanding about how this mailing list (and GPX itself) works.  Nobody is in charge.  Decisions are made by consensus.  If you want something done, step up to the plate and make a case for it, and present a finished, working schema."
- [POI/Waypoint Phone Number Attribute](https://www.topografix.com/gpx_mailing_list.asp#15910526580.20061205132718@topografix.com) by Dan Foster, Dec 2006
  - "I implemented temperature and depth in ExpertGPS when MapSource first added it to their GPX files.  A few months later my GPX files stopped validating, and I learned that Garmin had come out with a new version of their private schema, and deleted the old schema from their Web site!"
- [Waypoints, Tracks, Routes](https://www.topografix.com/gpx_mailing_list.asp#fl9inu+s6eu@eGroups.com) (regarding Garmin logs) by Dan Anderson, Dec 2007
  - "The actual tracklog is stored in the "active log" and contains x, y, z, and timestamps. Saved is not saved but usually processed and reduced."
- [Explanation of <ele> is unclear](https://www.topografix.com/gpx_mailing_list.asp#156410363.20090407134425@topografix.com) by Dan Foster, Apr 2009
- "We intended it to be the same as GGA.  I went back to Kjeld's original request to include it"



### Robert Lipe's Proposal in 2009/2010

- [GPX 1.1 speed and course](https://www.topografix.com/gpx_mailing_list.asp#883NFwuxP4150S02.1245790215@cmsweb02.cms.usa.net) - Robert Lipe, 23 June 2009
  - This thread started the discussion
  - Mentioned temperature, depth, cadence (crank / wheel), pitch / roll / yaw, UIDs
  - "It does strike me that above we have two different classes of data: one that's location or real-world temporal data measured by external sensors that's associated with a location, but not really GPS itself, and one that's just external data (phone numbers, etc.) that happens to be at a location."
  - "Do we like the way this conversation just turned from "putting a few thing we forgot back in" to "formalize the most common requests we've accumulated in the 4 years since GPX 1.1 has been out"? :-)"
- [Draft of proposed GPX 1.1 extensions](https://www.topografix.com/gpx_mailing_list.asp#82a839a50912231037x561947b9w351daeb2772f48d@mail.gmail.com) - Robert Lipe, 23 Dec 2009
  - Proposal for GPX 1.1 extensions or GPX 1.2
  - I've created a formatted version of the [RJL proposal](rjl-proposal.md)
  - Garmin responses
    - Initially a positive response to Steve Hales (azbithead) at Garmin - [link](https://www.topografix.com/gpx_mailing_list.asp#hhgg2h+10l5s@eGroups.com)
    - Second response from Garmin offered their extensions - [link](https://www.topografix.com/gpx_mailing_list.asp#hi0dp8+740i@eGroups.com)
    - Third response from Garmin suggested an extension schema for 1.1 and a new 1.2
    - Final response from Garmin was that it was unlikely they'd adopt it - [link](https://www.topografix.com/gpx_mailing_list.asp#hiitni+a64o@eGroups.com)
    - Summary in Apr 2018 talks about several vendors making contact privately, presumably back in 2010 - [link](https://www.topografix.com/gpx_mailing_list.asp#CAGJ6+wq4Pp9d2Qb-YVmkPtkG-h_sOiqR6d=PEpR-rinLuQ6T_Q@mail.gmail.com)
      - Robert's response was described as "deflated" - [link](https://www.topografix.com/gpx_mailing_list.asp#CAGJ6+wq4Pp9d2Qb-YVmkPtkG-h_sOiqR6d=PEpR-rinLuQ6T_Q@mail.gmail.com)
  
- [GPX version 2](https://www.topografix.com/gpx_mailing_list.asp#pbjvb2+h952tg@YahooGroups.com) by Topo GPS
  - Need to read

