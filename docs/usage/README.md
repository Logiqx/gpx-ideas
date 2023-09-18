## GPX Usage

### Background

All of the topics listed in this document apply to multiple versions of GPX. Currently this means GPX 1.0 and GPX 1.1 but they also apply to GPX 1.2. All of the items described below relate to standards / best practices and are essentially documentation activities, although compressed archives will require some development and testing.



### Compressed Archives

- Document compressed archives (GPZ) for GPX 1.0 / 1.1 / 1.2
- Inspired by the KMZ format of KML which is based on the ZIP format
- This idea was supported by Dan Foster, Robert Lipe, Jeremy Irish and numerous other people



### Embedded Icons, Images, Photos, Videos

- "We do need to come up with some answers as to how GPX should handle things like photos embedded in waypoints, waypoints embedded in photos, and your hotspots and other map symbols." - see [link](https://www.topografix.com/gpx_mailing_list.asp#885169760.20060825161206@topografix.com)
- This ties in particularly well with compressed archives (GPZ) where multiple files can be bundled together
- However, use of relative paths may have some issues as described in the possible [improvements](../core/README.md) to the GPX core



### Schema Endpoints

- HTTPS support was discussed by Dan in 2018 - [link](https://www.topografix.com/gpx_mailing_list.asp#698030247.20180425090713@topografix.com)
  - It was also raised new [thread](https://groups.io/g/gpx/topic/tools_for_validating_gpx/95697089?p=,,,20,0,0,0::recentpostdate/sticky,,,20,2,0,95697089,previd%3D1693402933996920097,nextid%3D1607599082822356246&previd=1693402933996920097&nextid=1607599082822356246) in the GPX developers mailing list, discussing validation tools and HTTPS



### Documentation Tweaks

- Clarification about `<ele>` which is relative to MSL
  - See "Definition of `<ele>` is unclear" discussion on [Github](https://github.com/Logiqx/gpx-ideas/discussions/1) for more information
- Clarification about the use of WGS84
  - See "WGS84" discussion on [Github](https://github.com/Logiqx/gpx-ideas/discussions/2) for more information
- Make it clear that latitude and longitude values should not provide more than 9 decimal places
