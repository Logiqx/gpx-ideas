## GPX Developers Mailing List and GPSXML Archive

### Suggestions for GPX 1.2

There have been a number of suggestions over the years, some of which are listed below.

A fair few of these (but perhaps not all) seem like worthwhile changes and should go into a GPX 1.2 proposal.



#### Track Type

- on6vd+yahoo.co.uk on Wed Apr 04 11:15:35 2018 ([link](https://www.topografix.com/gpx_mailing_list.asp#pbjvb2+h952tg@YahooGroups.com))
  - track type information (i.e. cycling track, pedestrian track, flight track)
  - it might be best to do this as an extension so that the list can be extended, without needing yet another core GPX release in the future?



#### Fix Type

Additional fix types that aren't available in GPX 1.0 / GPX 1.1

- "dr", "float", "manual", rtk", "sim"
  - see [summary](../proposal/fix-type.md) of fix type in previous proposal



#### Extensions for all Complex Types

All complex types should support extensions

- egroups+topografix.com on Wed Sep 22 09:26:43 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#1754117908.20040922123201@topografix.com))
  - We left <extensions> out of the following GPX 1.1 complex types
- egroups+topografix.com on Fri Nov 12 09:06:19 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#703411000.20041112120550@topografix.com))
  - copyrightType, linkType, emailType, personType, ptType, ptsegType, boundsType - see email on 22 Sept 2004
- egroups+topografix.com on Wed Dec 30 09:46:45 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#817253482.20091230124632@topografix.com))
  - "All complexType elements should end in `<extensions>` so they can be extended privately.  (I believe <link> in GPX 1.1 needs this fix)"



#### Extensions for Source Elements

Add support for extended `<src>` elements

- Perhaps make `<src>` a complex type so that additional information can be supported using `<extensions>`
- The example [textType](https://www.topografix.com/gpx_mailing_list.asp#dbjvr8+101af@eGroups.com)  might be an option for declaring `<src>` as mixed content?



#### UUID

- UUID information has been suggested a few times and was included in RJL's 2009 proposal
- Maybe consider placing it everywhere that `<src>` elements are allowed?
- Should the field's content follow the string representation in RFC 4122 at http://www.ietf.org/rfc/rfc4122.txt?



#### Relative Paths

Support for relative paths in `<link>` elements has been suggested but it's not clear if there is an actual problem - TBC

- egroups+topografix.com on Mon Jan 04 10:42:16 2010 ([link](https://www.topografix.com/gpx_mailing_list.asp#953828510.20100104134157@topografix.com))
  - Proposal

- robertlipe+gmail.com on Mon Jan 04 10:54:01 2010 ([link](https://www.topografix.com/gpx_mailing_list.asp#82a839a51001041053u8541b76x8f36c0ed7e9329fe@mail.gmail.com))
  - "It's worth mentioning that during the process of formalizing KML for the OGC, there was a surprisingly large effort required to try to nail corner cases with relative paths and ssociated files.   It's harder to do well than it sounds."
- #me
  - Combining this with file compression ("gpz" files) could be rather useful



#### Embedded Icons, Images, Photos, Videos, etc

[Creation vs modification times](https://www.topografix.com/gpx_mailing_list.asp#885169760.20060825161206@topografix.com) - Dan F, 25 Aug 2006

- "We do need to come up with some answers as to how GPX should handle things like photos embedded in waypoints, waypoints embedded in photos, and your hotspots and other map symbols."
- This ties in particularly well with the use of file compression ("GPZ" files) where files can be bundled together.



#### Base Types

[Base definitions schema](https://www.topografix.com/gpx_mailing_list.asp#625504761.20050119143522@topografix.com) for gpx_style and gpx_overlay - TBC

- Create a base definitions schema that only contains elements that will be referenced by other schemas
- This may be useful if sensors have common attributes like "src" and "acc", but may be overkill for this use-case.




#### Validation of Extensions

- [GPX 1.1 `<extensions>` allows broken GPX to validate](https://www.topografix.com/gpx_mailing_list.asp#124423616.20050119080422@topografix.com)
  - The <extensions> element in GPX 1.1 imposes "lax" processing on elements included from other schemas.
  - Endorsed by Dave W - [link](https://www.topografix.com/gpx_mailing_list.asp#csn437+atac@eGroups.com)
- [Namespace ""##other"](https://www.topografix.com/gpx_mailing_list.asp#csqu4i+54ei@eGroups.com)
  - The problem appears to be the namespace="##other" constraint in the /extensions field. I don't think that this is needed now that the extensions are separately wrapped.
  - Check https://www.gpstrailmaps.com/gpx/1/1/strict/gpx.xsd using archive.org
- [More problems with GPX 1.1 and multiple namespaces](https://www.topografix.com/gpx_mailing_list.asp#197383556.20050121114718@topografix.com) - 2005
  - I don't like knowing that GPX 1.1 allows invalid GPX to validate.  I don't like the fact that GPX 1.1 makes it very difficult to reference base types in extension schemas.
  - This also talks about MapSource schema checks when loading GPX
  - Dave W suggested an alternative "strict" schema - inspired by W3C
  - Explanation of lax vs strict by Steve Hales (azbithead) - maybe lax is not as bad as thought?
  - Garmin response regarding "strict" schema and the need for an internet connection - [Link](https://www.topografix.com/gpx_mailing_list.asp#ctmeq7+ggmq@eGroups.com)



#### Tweaks to Documentation

Add clarification for the following topics

  - [Magnetic variation](https://www.topografix.com/gpx_mailing_list.asp#8efd358205010315274f43f5d4@mail.gmail.com)
    - Cannot change due to compatibility issues, just add 360 to negative values
  - Decimal places - lat and lon
    - No more than 9 decimal places makes sense - precision of 1/10th of a millimeter
  - Explanation of elevation which is above MSL so far as I know?
    - Post by Dan F, Apr 2009 - [link](https://www.topografix.com/gpx_mailing_list.asp#156410363.20090407134425@topografix.com) 
    - [Re: explanation of <ele> is unclear](https://www.topografix.com/gpx_mailing_list.asp#grnrhu+fcic@eGroups.com) by Dan A, Apr 2009
    - [summary](https://www.topografix.com/gpx_mailing_list.asp#49DBADDD.2040307@free.fr) by jrepetto+free.fr
    - [what people care about](https://www.topografix.com/gpx_mailing_list.asp#8efd35820904071617l19952617lf33fec04e6d1deef@mail.gmail.com) by Paul Tomblin
    - [Garmin have a model of the geoid](https://www.topografix.com/gpx_mailing_list.asp#grnrhu+fcic@eGroups.com) by Dan Anderson
    - "The NMEA $GPGGA sentence gives the altitude above mean sea level and the height of the geoid (MSL) above the WGS84 ellipsoid."
    - [GPS units need a geoid model](https://www.topografix.com/gpx_mailing_list.asp#49E099F8.7050907@free.fr) by jrepetto+free.fr
      - Claims SiRF Star II doesn't have this model. I can check if required using GT-11.

See previous [proposal](../proposal/definitions.md) for additional details.



### Miscellaneous Topics

- [GPX version 2](https://www.topografix.com/gpx_mailing_list.asp#pbjvb2+h952tg@YahooGroups.com) by Topo GPS - pretty much covered by the list above and "standard" [extensions](../extensions/README.md)
  - Suggested [IETF](https://www.ietf.org) standard
- [Aviation Database Waypoint](https://www.topografix.com/gpx_mailing_list.asp#cs5n3f+jjlh@eGroups.com)
  - Paul Tomblin has created the aviation database extension schema - http://navaid.com/GPX/
    - Namespace http://navaid.com/GPX/NAVAID/0/8
- Geo-caching for GPX 1.0
  - [http://static.groundspeak.com/cache/1/0/cache.xsd](http://static.groundspeak.com/cache/1/0/cache.xsd)
- Points of interest?
  - [Re: POI/Waypoint Phone Number Attribute](https://www.topografix.com/gpx_mailing_list.asp#el3k6n+hmlu@eGroups.com) by Doug in Dec 2006. Distinguishes waypoints and POIs
- Proximity waypoints / alerts
  - slavins+hearsay.demon.co.uk on Sun Dec 31 15:08:05 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#en9fdj+su5p@eGroups.com))
  - See Garmin GpxExtensions [xsd](https://www8.garmin.com/xmlschemas/GpxExtensions/v3/GpxExtensionsv3.xsd)

