## GPX Developers Mailing List and GPSXML Archive

### Common Principles

These posts provided some insight into some of the early design decisions.

davewissenbach+yahoo.com on Thu Nov 08 21:36:07 2001 ([link](https://www.topografix.com/gpx_mailing_list.asp#9sfq05+ehv2@eGroups.com))

> we have previously agreed that required attributes of an element would be coded with the XML attribute syntax, and that optional data would be coded as elements.

davewissenbach+yahoo.com on Thu Jan 24 20:17:24 2002 (link)

> I'd recommend that all applications code to a rigid sequence that follows the schema but allow any order of elements when parsing. I believe that's what the topografix applications do, and that's what my application does.

davewissenbach+yahoo.com on Fri Apr 05 17:54:11 2002 ([link](https://www.topografix.com/gpx_mailing_list.asp#a8lkaq+33pf@eGroups.com))

> Protect your application against schema changes by ignoring unknown elements. Protect other applications from yours by validating test files from your application against the schema.

davewissenbach+yahoo.com on Sat Jan 11 19:37:43 2003 ([link](https://www.topografix.com/gpx_mailing_list.asp#avqnu4+dklo@eGroups.com))

> However, If I had to do this over again, I'd use the same code for routes and tracks, and/or program using the xml document object model, or DOM. The reason that I would do this is so that my program could work with an existing program but not lose data for tags which I don't implement

davewissenbach+yahoo.com on Wed Nov 17 18:25:22 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#cnh15d+evfo@eGroups.com))

> I don't think that validation is a good idea for a reader, anyways because minor glitches and programming errors that would otherwise slide right through your parser will cause the document to be rejected. Instead, be strict on your output, but not on input. 

davewissenbach+yahoo.com on Fri Nov 26 18:27:01 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#co8olb+922q@eGroups.com))

> We did have discussion early on as to whether gpx was just an exchange or document format and decided to provide the extensions in any other namespace in order to resolve the dilemna.

dananderson2+yahoo.com on Tue Jan 18 13:18:36 2005 ([link](https://www.topografix.com/gpx_mailing_list.asp#csjuel+6nu5@eGroups.com))

> I generally go with a lenient reader/receiver and a strict (correct) writer/sender.  The user primarily only cares about whether it works or not.  Not doing it that way can put a big strain on your technical support department even though your product is right.

dananderson2+yahoo.com on Wed Jan 17 19:42:46 2007 ([link](https://www.topografix.com/gpx_mailing_list.asp#eomqbj+phc4@eGroups.com))

> I'd like to see us address the immediate problems that people are having.  Small additions to the GPX schema and/or the GPX_Overlay schema (or some new extension schema) could help many people.

dananderson2+yahoo.com on Fri Apr 10 09:19:24 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#grnrhu+fcic@eGroups.com))

> The NMEA $GPGGA sentence gives the altitude above mean sea level and the height of the geoid (MSL) above the WGS84 ellipsoid.
>
> Most consumer receivers give the user the altitude above mean sea level, which is what I want for travel in the mountains. This is the value I would expect to see in the GPX "ele" field (and is in all of my files)

jeremy+groundspeak.com on Thu Jul 17 09:13:14 2003 ([link](https://www.topografix.com/gpx_mailing_list.asp#007c01c34c7e$4f4a1030$84a79642@groundspeak.biz))

> GPX should be restricted to waypoint, track, and route sharing with the addition of display specifics. Maps should be in its own XML spec and separate from GPX. Track display options, however, have its place in GPX.

kevin+synergysa.com.au on Wed Feb 06 01:58:16 2002 ([link](https://www.topografix.com/gpx_mailing_list.asp#001801c1aef4$bba65d20$1900a8c0@krlap))

> Sequencing is used to sort and re-order waypoints as well as routes and tracks trather than manipulating the timestamp and modifying the base data.

