## GPX Developers Mailing List and GPSXML Archive

### Random Takeaways

This list is by no means exhaustive, just a few posts that have some historical relevance.

- General consensus that GPX should only hold geographic data, and not presentation data.
  - Dave Wissenbach was firmly of the opinion that styling belongs in extension schemas - [link](https://www.topografix.com/gpx_mailing_list.asp#co8olb+922q@eGroups.com)
- There was talk about GPX 1.2 back in 2005
  - Strict schema validation was proposed
  - Fix for `<magvar>` was discussed - i.e. -180 to +180
- Workaround for loading into Garmin MapSource (using the GPX 1/0 namespace) was already known in 2005 - [link](https://www.topografix.com/gpx_mailing_list.asp#756031977.20050201101607@topografix.com)
  - Dan also referred to MapSource being the only program to validate GPX when loading - [link](https://www.topografix.com/gpx_mailing_list.asp#1182069704.20050201165622@topografix.com)
  - Detailed explanation of the validation and parsing performed by Garmin MapSource - [link](https://www.topografix.com/gpx_mailing_list.asp#ctr3di+r3a7@eGroups.com) 
- Suggestion of IETF or W3C standard
  - W3C [SPATIAL DATA ON THE WEB INTEREST GROUP](https://www.w3.org/2017/sdwig/)
    - Meeting in Mar 2018 - [minutes](https://www.w3.org/2018/06/06-sdw-minutes.html#x14)
- GPX 2.0 could involve breaking most of the GPX 1.1 elements out into their own schemas
  - [GPX creation vs modification times - proposed schema](https://www.topografix.com/gpx_mailing_list.asp#885169760.20060825161206@topografix.com) - Dan F, 25 Aug 2006
- Third party extensions can introduce risk since they can be deleted
  - [POI/Waypoint Phone Number Attribute](https://www.topografix.com/gpx_mailing_list.asp#15910526580.20061205132718@topografix.com) by Dan F, Dec 2006
- What is GPX for?
  - Jeremy Irish posted in Jul 2003 - [link](https://www.topografix.com/gpx_mailing_list.asp#000701c34c8c$4ab95c20$84a79642@groundspeak.biz)
    - "What I suggest is that additional display parameters for tracks, routes and waypoints are perfectly acceptable in GPX, which it's intent (correct me if I'm wrong) is an open standard to exchange data between GPS receivers. As GPS receivers get more sophisticated I wouldn't be surprised if you will be able to suggest display parameters for data. We already have this for the GPS symbol freetext."
- Lower case names were explained by Kevin Read in Feb 2002 - [link](https://www.topografix.com/gpx_mailing_list.asp#004101c1ab89$ae5d1690$1900a8c0@krlap)
  - "The original GPX schemas that I produced upto 1.1 has lowercase tags."
- Sequencing was explained by Kevin Read in Feb 2002 - [link](https://www.topografix.com/gpx_mailing_list.asp#001801c1aef4$bba65d20$1900a8c0@krlap)
  - "Sequencing is used to sort and re-order waypoints as well as routes and tracks trather than manipulating the timestamp and modifying the base data."



### Philosophy

kerry.raymond+gmail.com on Mon Dec 04 12:07:07 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#02dc01c717df$a27bb2b0$3c13a8c0@cabernet))

  - Quite thought provoking. I'd sum it up by saying that temporal data associated with a GPS fix belongs in GPX trackpoints.

egroups+topografix.com on Wed Jan 17 16:53:17 2007 ([link](https://www.topografix.com/gpx_mailing_list.asp#8339231.20070117194852@topografix.com))

> I'm going to suggest that GPX isn't really about exchanging GPS data. It may have started out that way, but it's really become a way to exchange spatial data - points and lines on the Earth.
>
> If we were starting from scratch, I would suggest that the base schema contain nothing more than the definition of a geographic point (lat/lon required, elevation and timestamp optional) and line, and that everything else be built (through extension schemas) on top of that.

robertlipe+usa.net on Tue Jun 23 13:50:51 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#883NFwuxP4150S02.1245790215@cmsweb02.cms.usa.net))

> It does strike me that above we have two different classes of data: one that's location or real-world temporal data measured by external sensors that's associated with a location, but not really GPS itself, and one that's just external data (phone numbers, etc.) that happens to be at a location.

