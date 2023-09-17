## GPX Developers Mailing List and GPSXML Archive

### Additional Suggestions

#### Schema endpoints - HTTPS support

- Suggested by Dan in 2018 - [link](https://www.topografix.com/gpx_mailing_list.asp#698030247.20180425090713@topografix.com)
  - See new [thread](https://groups.io/g/gpx/topic/tools_for_validating_gpx/95697089?p=,,,20,0,0,0::recentpostdate/sticky,,,20,2,0,95697089,previd%3D1693402933996920097,nextid%3D1607599082822356246&previd=1693402933996920097&nextid=1607599082822356246) about tools and HTTPS



#### Compressed Files

- gpz - supported by Robert Lipe and Jeremy Irish
  - egroups+topografix.com on Mon Jan 05 12:04:36 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#796201311.20090105144640@topografix.com))
    - "My implementation plan was to mimic KMZ as much as possible - the program that opened the compressed GPX archive would extract data from any and all GPX files contained therein.  I wasn't planning to use other data in the archive (.jpg, etc) but would probably support it if others caught on to the idea of compressed GPX archives."
  - jeremy+groundspeak.com on Mon Jan 05 13:10:23 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#20090105211019.4ac0c100@rosie.groundspeak.biz))
  - n.b. kmz is a kml file and resources in a zip file



#### Signed Keys

#me - I saw signed keys mentioned but dismissed it due to the complexity and limited benefit



#### Relative Paths

Relative paths in `<link>` elements

- egroups+topografix.com on Mon Jan 04 10:42:16 2010 ([link](https://www.topografix.com/gpx_mailing_list.asp#953828510.20100104134157@topografix.com))
  - Proposal

- robertlipe+gmail.com on Mon Jan 04 10:54:01 2010 ([link](https://www.topografix.com/gpx_mailing_list.asp#82a839a51001041053u8541b76x8f36c0ed7e9329fe@mail.gmail.com))
  - "It's worth mentioning that during the process of formalizing KML for the OGC, there was a surprisingly large effort required to try to nail corner cases with relative paths and ssociated files.   It's harder to do well than it sounds."
- #me
  - Combine this with GPZ usage as it could be really useful?



#### Embedded Icons, Images, Photos, Videos, etc

[Creation vs modification times](https://www.topografix.com/gpx_mailing_list.asp#885169760.20060825161206@topografix.com) - Dan F, 25 Aug 2006

- "We do need to come up with some answers as to how GPX should handle things like photos embedded in waypoints, waypoints embedded in photos, and your hotspots and other map symbols."



#### Base Types

[Base definitions schema](https://www.topografix.com/gpx_mailing_list.asp#625504761.20050119143522@topografix.com) for gpx_style and gpx_overlay

- Create a base definitions schema that only contains elements that will be referenced by other schemas



#### Complex Types

Complex types need to end in extensions

- egroups+topografix.com on Fri Nov 12 09:06:19 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#703411000.20041112120550@topografix.com))
  
  - copyrightType, linkType, emailType, personType, ptType, ptsegType, boundsType - see email on 22 Sept 2004
  
- egroups+topografix.com on Wed Dec 30 09:46:45 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#817253482.20091230124632@topografix.com))

  - "All complexType elements should end in `<extensions>` so they can be extended privately.  (I believe <link> in GPX 1.1 needs this fix)"



#### Track Type

- on6vd+yahoo.co.uk on Wed Apr 04 11:15:35 2018 ([link](https://www.topografix.com/gpx_mailing_list.asp#pbjvb2+h952tg@YahooGroups.com))
  - track type information (i.e. cycling track, pedestrian track, flight track)



#### Source Elements

Extended `<src>` elements

- Perhaps make it a complex type and add extensions?
- [textType](https://www.topografix.com/gpx_mailing_list.asp#dbjvr8+101af@eGroups.com)  would be a possible way of declaring `<src>` as mixed content?



#### UUID

- Maybe consider it where `<src>` elements are allowed?
- Should the field's content follow the string representation in RFC 4122 at http://www.ietf.org/rfc/rfc4122.txt?




#### Strict Extensions

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



#### Documentation

Add clarification for the following topics

  - [Magnetic variation](https://www.topografix.com/gpx_mailing_list.asp#8efd358205010315274f43f5d4@mail.gmail.com)
    - Cannot change due to compatibility issues, just add 360 to negative values
  - Decimal places - lat and lon
  - Explanation of elevation
    - Post by Dan F, Apr 2009 - [link](https://www.topografix.com/gpx_mailing_list.asp#156410363.20090407134425@topografix.com) 
    - [Re: explanation of <ele> is unclear](https://www.topografix.com/gpx_mailing_list.asp#grnrhu+fcic@eGroups.com) by Dan A, Apr 2009
    - [summary](https://www.topografix.com/gpx_mailing_list.asp#49DBADDD.2040307@free.fr) by jrepetto+free.fr
    - [what people care about](https://www.topografix.com/gpx_mailing_list.asp#8efd35820904071617l19952617lf33fec04e6d1deef@mail.gmail.com) by Paul Tomblin
    - [Garmin have a model of the geoid](https://www.topografix.com/gpx_mailing_list.asp#grnrhu+fcic@eGroups.com) by Dan Anderson
    - "The NMEA $GPGGA sentence gives the altitude above mean sea level and the height of the geoid (MSL) above the WGS84 ellipsoid."
    - [GPS units need a geoid model](https://www.topografix.com/gpx_mailing_list.asp#49E099F8.7050907@free.fr) by jrepetto+free.fr
      - Claims SiRF Star II doesn't have this model. I can check if required using GT-11.



### FYI

#### 2009 / 2010 Proposal

- GPX extensions [proposed](robert-ext.md) by Robert L, 23 Dec 2009 to 12 Jan 2010 - [link](https://www.topografix.com/gpx_mailing_list.asp#82a839a50912231037x561947b9w351daeb2772f48d@mail.gmail.com)
  - Garmin responses - FYI
    - Initially a positive response to Steve Hales (azbithead) at Garmin - [link](https://www.topografix.com/gpx_mailing_list.asp#hhgg2h+10l5s@eGroups.com)
    - Second response from Garmin offered their extensions - [link](https://www.topografix.com/gpx_mailing_list.asp#hi0dp8+740i@eGroups.com)
    - Third response from Garmin suggested an extension schema for 1.1 and a new 1.2
    - Final response from Garmin was that it was unlikely they'd adopt it - [link](https://www.topografix.com/gpx_mailing_list.asp#hiitni+a64o@eGroups.com)
    - Summary in Apr 2018 talks about several vendors contacting him privately, presumably back in 2010 - [link](https://www.topografix.com/gpx_mailing_list.asp#CAGJ6+wq4Pp9d2Qb-YVmkPtkG-h_sOiqR6d=PEpR-rinLuQ6T_Q@mail.gmail.com)
      - Robert's response was "deflated" - [link](https://www.topografix.com/gpx_mailing_list.asp#CAGJ6+wq4Pp9d2Qb-YVmkPtkG-h_sOiqR6d=PEpR-rinLuQ6T_Q@mail.gmail.com)



#### 2018 Proposal

- [GPX version 2](https://www.topografix.com/gpx_mailing_list.asp#pbjvb2+h952tg@YahooGroups.com) by Topo GPS

  - Suggested [IETF](https://www.ietf.org) standard



#### Miscellaneous

- [Aviation Database Waypoint](https://www.topografix.com/gpx_mailing_list.asp#cs5n3f+jjlh@eGroups.com)
  - P Tomblin has created an extension schema - http://navaid.com/GPX/
- Points of interest?
  - [Re: POI/Waypoint Phone Number Attribute](https://www.topografix.com/gpx_mailing_list.asp#el3k6n+hmlu@eGroups.com) by Doug in Dec 2006. Distinguishes waypoints and POIs
- Proximity waypoints / alerts
  - slavins+hearsay.demon.co.uk on Sun Dec 31 15:08:05 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#en9fdj+su5p@eGroups.com))
  - See garmin [xsd](https://www8.garmin.com/xmlschemas/GpxExtensions/v3/GpxExtensionsv3.xsd)

