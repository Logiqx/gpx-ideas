## GPX Developers Mailing List and GPSXML Archive

### References to Feature Requests

This document captures references to a number of the items being proposed as extensions for GPX 1.1 and possibly for the core of GPX 1.2.

The list may not be exhaustive but it provides a starting point when looking for references to things like "course" and "speed".



#### SOG + COG

egroups+topografix.com on Tue Sep 07 13:13:56 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#2610299958.20040907161853@topografix.com))

> Someone pointed out to me off-list that <course> and <speed> were removed from <trkpt> in GPX 1.1.

egroups+topografix.com on Fri Nov 12 09:06:19 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#703411000.20041112120550@topografix.com))

> I haven't read any arguments against having course and speed be expressable in GPX.  I'd like to see it possible to express them.  I'm not convinced they belong in the main GPX schema, though.  (In line with my current thinking that very very little belongs in the main schema)

robertlipe+usa.net on Tue Jun 28 19:11:57 2005 ([link](https://www.topografix.com/gpx_mailing_list.asp#20050628213710.GN25966@rjloud.sco.com))

> I'm working with another developer on a module for GPSBabel that happens to strongly desire the DOP brothers plus speed and course.  I've long posited that speed and course are kind of silly, but I remembered reading that GPX supported those things, so I decided to roll over and add them to my internal data structures and GPX handlers on the grounds that if two formats could express it, someone must consider them non-silly.

thomas.landspurg+in-fusio.com on Tue Dec 06 14:54:13 2005 ([link](https://www.topografix.com/gpx_mailing_list.asp#dn54pc+a45k@eGroups.com))

> What is the best way to provide speed and course with GPX1.1? I've read that it was supported with GPX1.0, but not anymore?

friteam+gmail.com on Mon Jan 30 14:38:47 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#drm4hk+rm4i@eGroups.com))

> Well from what I've read NMEA is too low-level, not equally supported by all GPS devices and mostly you don't have Time/Position/Velocity in one sentence

friteam+gmail.com on Tue Jan 31 06:13:31 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#drnr8k+bh6q@eGroups.com))

> what I really want is to have one record/row in DB table that represents Time + Position + Velocity and this data is spread in at least 2 sentences of NMEA (as far as I know) and furthermore contain data which is not needed for me.

doolaard+gmail.com on Tue Jan 31 06:32:34 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#bdca9f6b0601310632l783bbe69n5698e1474e3b0fd2@mail.gmail.com))

> This sentence contains position and velocity (see the standard for the complete structure)

mhaxx+postino.it on Tue Mar 21 04:08:35 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#dvoqbi+ovct@eGroups.com))

> Is there possibility to store velocity and direction on a GPX file? Which tags?

robertlipe+usa.net on Tue Mar 21 06:25:44 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#20060321142539.GI13886@rjloud.localdomain))

> GPX 1.0 has a "speed" and "course" tags - link to [manual](http://www.topografix.com/gpx_manual.asp)
>
> Unfortunately, these were accidentally left out of 1.1.

k.raymond+qut.edu.au on Tue Mar 21 16:01:59 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#539D00AEADF27241BF1341D08A7A71C913D228@fitex01.fit.qut.edu.au))

> Redundant, perhaps, but if you have already calculated the velocity/direction, someone may prefer to store these results and not recalculate them.

yahoo+markwigmore.co.uk on Wed Mar 22 07:30:53 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#58995.192.35.35.42.1143041396.squirrel@www.easilymail.co.uk))

> If you are in a boat or flying then your instruments will give you a different course and speed to the GPS if there is significant wind and/or tide. It is only when you are in contact with the ground that there is no (significant) difference, so my vote would be to allow for these to be included in the GPX file.

hannu.lohi+tracker.fi on Thu Mar 30 02:13:57 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#e0gaup+10d7@eGroups.com))

> We are making tracking devices to many systems one example is wild animal. In there the device must be having battery life over 2 years. In that case, track point is taken only e.g. every 2 hour. Calculating speed from track for those points is not giving much information, but having it from GPS would give lot more.

kruhc+seznam.cz on Tue Sep 12 12:39:18 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#ee71us+cnb4@eGroups.com))

> The file may not hold enough data for a precise calculation. With sparse data (eg. using a "azimuth-has-changed-by-5-degrees" filter for saving a position to a file) one would get wrong results.

evanc+irtech.com on Mon Jan 07 15:08:02 2008 (link)

> So would the "velocity" from the GPS be more accurate than v = d/t ? I have a rally application running on a PDA. It cares about distance travelled, average speed and time. 

egroups+topografix.com on Tue Jun 23 08:53:49 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#648699160.20090623103127@topografix.com))

> That speed, which is contained in NMEA messages, the receiver is calculated directly based on the Doppler effect (it is a separate issue, which is covered in numerous articles). If you take the speed of the coordinates and time, especially in the case of small intervals between  oints, errors in determining coordinates (as they inevitably) lead to errors in calculating the speed of tens of percent.

robertlipe+usa.net on Wed Jun 24 12:42:05 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#886NFXTOd6348S17.1245872489@cmsweb17))

> I only support a couple hundred models of GPS receivers and a few million users.  Your experience in other markets may vary.   
>
> The GPSMap 60 in your example does not present speed in any stored format and not even int he GPX it writes in its later firmware versions.  The only references to speed in all of Garmin's non-realtime protocol specs are in reference to flightbook records or their workout devices or in their D800 PVT packets, which are never stored by the devices themselves.

keyork+xtra.co.nz on Wed Dec 23 14:56:33 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#599892.32417.qm@web96012.mail.aue.yahoo.com))

> I am all for providing support for recording any data that is commonly supplied by current GPS based units. Measured speed and course are a definite yes, I'm surprised that they weren't in the original standard.

krheinwald+web.de on Thu Dec 24 04:56:43 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#hgvod7+nns1@eGroups.com))

> Heading gives the orientation of the vehicle while course is the direction of movement of the vehicle. Examples: Airplane flying with wind from its side, sailboat with wind or stream from its side, helicopter flying sideways

tanelilaine+yahoo.com on Fri Apr 23 06:32:34 2010 ([link](https://www.topografix.com/gpx_mailing_list.asp#hqri3o+gghg@eGroups.com))

> I can't find <speed> in GPX1.1 schema but in the 1.0 manual it is listed. Does this mean that I should not use it if I develop an application that exports gpx files?

scbldmophahigrml5egqzwnaacg4b3utahmt2hp2+yahoo.com on Wed Aug 10 16:52:41 2016 ([link](https://www.topografix.com/gpx_mailing_list.asp#no9aa4+ba75f2@YahooGroups.com))

> My analysis of many tracks from many devices leads me to believe that, at the typical speeds of around 10 Kph (6 knots), the raw COG value provide a far more accurate and less "noisy" representation of a yacht's track than the heading deduced with trigonometry from successive lat/lon values. The same appears to be true from speed, but that's of less concern to me at the moment.  

acebrianjuan+gmail.com on Wed Oct 24 08:03:59 2018 ([link](https://www.topografix.com/gpx_mailing_list.asp#CAE6hxOLVB6-wavtDLOjwwwuce=nyXjSVw8Z3Prh+Dqnz0iDosg@mail.gmail.com))

> I have been asked to add velocity information to my GPX files and I was wondering if there is a standard XML tag for this purpose.

robertlipe+gmail.com on Wed Oct 24 13:37:39 2018 ([link](https://www.topografix.com/gpx_mailing_list.asp#CAGJ6+wpK2U80AwyTDNUOMEa+n=kQyNf4t8_xqZWv_duL0Z=qAw@mail.gmail.com)) - see "my thoughts" further below

> What we have seen in practice is that people were using the instantaneous difference in locations a few seconds apart, where the GPS location error may exceed the amount of actual motion, and creating silly <speed> tags. No, your bike ride was never 43 miles per hour at the starting line. MOST of the actual users of the data were recomomputing the speed from the location and time anyway, so it was a bit redundant.

smithalan+bigpond.com on Wed Oct 24 19:38:58 2018 ([link](https://www.topografix.com/gpx_mailing_list.asp#50de90b8.1adf78.166a916bbd9.Webtop.99@bigpond.com))

> Just as an aside, I have determined that many GPS interfaces report  speed (SOG) and course (COG) containing values that are reported to be derived independently of the position and time coordinates. There are some sources that indicate that they may be derived using a doppler measurement. 
>
> In any case, these SOG and COG values provide a smoother result than that derived from position and time, and for that reason they are a valuable resource. I have chosen to record them in my GPX files as extensions.



My thoughts:

- Early Garmin devices did not record COG + SOG in their track logs (limited memory), so GPX files could only calculate them from lat + lon pairs.
- This is no longer true though with COG and SOG routinely being recorded, perhaps since the advent of Garmin Connect and the Fenix watch



#### Accuracy

kerry.raymond+gmail.com on Wed Aug 16 15:18:32 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#003b01c6c181$4f9a1dc0$3c13a8c0@cabernet))

> One thing we might also want to consider (and probably implement through extending the  elements -- which is why I worry about the use of XML attributes) is support for accuracy/precision in values. With GPS, we know there might be a 10 metre error. WIth differential GPS or NGSS, we expect that to be a lot smaller. It would be good to have a way to capture accuracy (I'd see it as an optional element within the various other elements).
>
> But when we start talking about geocoding photos, accuracy becomes a lot more of an ssue. Why? Because some of the geocoding data may not be coming from a GPS but may be based on people using a map or Google Earth and a very rough clock to retrospectively add geo-coding to existing photos. 

mr+marcelruff.info on Mon Dec 31 06:09:31 2007 ([link](https://www.topografix.com/gpx_mailing_list.asp#flaesg+2r5j@eGroups.com))

> I  think it is time to have a GPX 1.2 with such markup as above (including a tag for accuracy).
> Otherwise this info is cluttered in <extensions> by every user of GPX in an incompatible way.

marcel.ruff on 31 Dec 2007:

>  I agree

timfpark+gmail.com on Tue Jan 22 07:47:12 2008 ([link](https://www.topografix.com/gpx_mailing_list.asp#fn3loq+mlmq@eGroups.com))

> I'm interested as well helping work on another revision to the standard.   The internet project I am working on (a digital trail database:   http://www.tierrawiki.org/) could particularly be helped by the addition of an accuracy metric to each track point.

ragge+kth.se on Sun Feb 27 17:56:40 2011 ([link](https://www.topografix.com/gpx_mailing_list.asp#ik6e64+33jh@eGroups.com))

> Is there a recommended way to represent Accuracy or EPE (estimated position error) in distance (meters) in GPX?

ragge+kth.se on Mon Feb 28 03:11:21 2011 ([link](https://www.topografix.com/gpx_mailing_list.asp#ikfvsg+1s34@eGroups.com))

> I am not talking about the EPE value (some strange vendor specific 1-20 value, agreed), but the error in meters (or feet), which many vendors do provide. This value is just as much an approximation as the position, and gives the position much higher value since 95 % (or what is it?) of the positions actually are supposed to be within that radius and almost all of them should be at least pretty close, whereas the receiver almost never is at the given position that is stored in GPX today. In addition, there is no way today to even guess how large the error is.

tt+smartcomsoftware.com on Mon Feb 28 03:18:47 2011 ([link](https://www.topografix.com/gpx_mailing_list.asp#01a201cbd739$39613250$ac2396f0$@com))

> Note that different receiver manufacturers use different figures, e.g. historically many have used 95%, but others user 67%, 50%... Also, the period of time that the position is measured over has a significant effect too.

ragge+kth.se on Mon Feb 28 12:49:08 2011 ([link](https://www.topografix.com/gpx_mailing_list.asp#ikh1o4+ct2i@eGroups.com))

> Is there a standard way to convert between error-in-distance (as meters or feet) and the xDOPs?

Rozzin+geekspace.com on Wed Mar 02 19:52:02 2011 ([link](https://www.topografix.com/gpx_mailing_list.asp#87ipw0dg1k.fsf@slice.rozzin.com))

> GPSd apparently includes code to do this, for the cases in which a GPS unit doesn't provide all of the numbers numbers itself
>
> which involves scaling each of XDOP and YDOP by one of these constants("assumption about the base error of GPS fixes in different directions")
>
> to get absolute lengths of position uncertainty in each dimension (radius being computed from (x, y) in the usual manner)

ragge+kth.se on Wed Mar 02 22:25:48 2011 ([link](https://www.topografix.com/gpx_mailing_list.asp#iknc94+p4ie@eGroups.com)) - see "useful links" further below

>I believe that starting to convert between the different xDOPs and errors
>in distance without knowing the internal workings of the receiver is really
>dangerous business. I believe that the only reasonable thing to do is to
>record whatever the receiver has calculated, and not start to calculate any
>new numbers from that at all in the recording process.
>
>This makes me believe that GPX really should have standardized fields for
>errors in distance, so that if that is what the receiver gives you, you can
>both record it and read it.
>
>Sure it is an estimate - but so is the position itself, as well as the xDOPs,
>and the error estimate is part of the solution when calculating the position,
>you can't really have one without the other. (Or - you could, but then only
>for applications that don't care about the real position but only about an
>estimated position as a point, pretty much like there there are
>applications that don't use the altitude.

on6vd+yahoo.co.uk on Wed Apr 04 11:15:35 2018 ([link](https://www.topografix.com/gpx_mailing_list.asp#pbjvb2+h952tg@YahooGroups.com)) - n.b. I think Harmen means "heading" and not "bearing"

> TrackPoint: speed, heartbeat, horizontalAccuracy, verticalAccuracy,  speedAccuracy, course, bearing, ambient temperature, air pressure

stephane.peneau+wanadoo.fr on Tue May 28 13:47:00 2019 ([link](https://www.topografix.com/gpx_mailing_list.asp#qcjatu+15pqh7t@YahooGroups.com))

> I use a dual frequency gnss receiver with centimeter accuracy, and I'd like to store each point accuracy before uploading the file in the OpenStreetMap gpx database.



Useful links

- gpsd - [libgpsd_core.c](https://github.com/jcable/gpsd/blob/master/libgpsd_core.c) - "Carl Carter of SiRF supplied this algorithm for computing DOPs"



#### Attitude / Orientation

richard+jelbert.com on Tue Aug 01 11:57:40 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#eao840+ahnf@eGroups.com))

> Also, to include aerial photography then height, pitch, roll and yaw (the heading) would cover the cameras position reference the ground. 
> 
> I also fly (student PPL) and can see times when a it would be very useful to communicate the pitch of the image to help sort out the straight ahead, 45 degrees down and 90 degrees down  images which would basically be like a satellite photo.

steveg+swapneat.com on Wed Aug 16 12:04:28 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#44E36BB0.90600@swapneat.com))

> In particular, to support image stitching, the values for lat, long, and pitch, head, roll, g_height, and s_height and flen all need to be able to support floating point values, preferably double precision.

robertlipe+usa.net on Tue Jun 23 13:50:51 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#883NFwuxP4150S02.1245790215@cmsweb02.cms.usa.net))

> yaw, pitch, and roll.     When we did the original GPX stuff, sensors that reported 3D orientation like tilt and compass were rare.  Now that geotagging is common and many of the higher end cameras and even cell phones can record that information and there are programs that can use that information, a standardized way to represent it could be nice.

robertlipe+gmail.com on Wed Dec 23 10:37:27 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#82a839a50912231037x561947b9w351daeb2772f48d@mail.gmail.com))

> `<Orientation>`
>  `<heading>` Rotation about the z axis (normal to the Earth's surface). A value of 0 (the default) equals North.
>  `<tilt>` Rotation about the x axis. A positive rotation is clockwise around the x axis
>  `<roll>` Rotation about the y axis. A positive rotation is clockwise around the y axis.

tacman+gmail.com on Mon Nov 07 15:51:27 2011 ([link](https://www.topografix.com/gpx_mailing_list.asp#j99qn4+gc4m@eGroups.com))

> Have pitch, tilt and heading been accepted into the GPX 1.1 standard?

smithalan+bigpond.com on Thu Jan 05 19:17:34 2012 ([link](https://www.topografix.com/gpx_mailing_list.asp#F498DD3CE71B4946BDA4B35D23D9A174@alansr50))

> I'm looking for an Android app for logging my aircraft's attitude (heading, pitch, roll from its gyro sensors) and position (lat lon, alt from its GPS)

falk+efalk.org on Mon Jan 09 15:01:32 2012 ([link](https://www.topografix.com/gpx_mailing_list.asp#jeauvq+ee4r@eGroups.com))

> Interested pilots should contact me via direct message; I could use a couple of alpha testers for a project that does what you want.

albert.mikolaj+yahoo.com on Tue Feb 11 11:37:20 2014

> I am a total newbie in GPX. I would like to know if it is possible to add sensor information such as roll and tilt onto the gpx file.

robertlipe+gmail.com on Tue Feb 11 11:53:50 2014 ([link](https://www.topografix.com/gpx_mailing_list.asp#CAGJ6+wp6Ao1D-3sNNDyQhgPz0GO-+cMoLEOFEUq3cWNcefjLcg@mail.gmail.com))

> There isn't a formal extension for roll and tilt; you'll have to make your own.



#### UUID

robertlipe+usa.net on Tue Jun 23 13:50:51 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#883NFwuxP4150S02.1245790215@cmsweb02.cms.usa.net))

> Unique identifiers for all objects.   While we have 'name' for most of our objects, it's not necessarily unique.  So there's no way for an external entity to refer to "track FOO" or "waypoint BAR" within a given GPX collection.

robertlipe+gmail.com on Wed Dec 23 10:37:27 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#82a839a50912231037x561947b9w351daeb2772f48d@mail.gmail.com))

> `<guid>` A GUID, uniquely identifying this object so that it may be referenced externally




#### Meteorological

egroups+topografix.com on Wed Apr 24 08:02:08 2002 ([link](https://www.topografix.com/gpx_mailing_list.asp#190130438480.20020424105452@topografix.com))

> There are certainly some elements of the Garmin private data that could be included in GPX.  `<depth>`120`</depth>` makes sense for exchanging data between fish-finders.  

joel+coastaloutdoors.com on Sun Nov 10 19:14:42 2002 ([link](https://www.topografix.com/gpx_mailing_list.asp#aqn7av+nmen@eGroups.com))

> depth:  depth at the waypoint  -  I would assume this would be geoidheight

egroups+topografix.com on Fri Nov 12 09:06:19 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#703411000.20041112120550@topografix.com))

> nautical direct measurements at each trackpoint: engine speed, heading, depth, temperature

egroups+topografix.com on Fri Nov 12 10:52:19 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#94150845.20041112135142@topografix.com))

> Garmin just introduced temperature logging for trackpoints.  Can GPX do this?

egroups+topografix.com on Fri May 13 06:21:31 2005 ([link](https://www.topografix.com/gpx_mailing_list.asp#794769528.20050513092255@topografix.com))

> I'll begin adding support for depth and some of your other extensions to my programs.

robertlipe+usa.net on Tue Aug 29 06:17:35 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#20060829131536.GI16743@rjloud.localdomain))

> Temperature, address, and colour, for example, are hardly concepts proprietary to Garmin. Subclass, an 18 digit hex number, doesn't lend itself nearly as well to a portable spec.
>
> While it's great that GPX _can be_ extended with vendor-specific stuff, if we grow the GPX core to include those concepts, then we get the benefits of true interoperability.

egroups+topografix.com on Mon Oct 23 12:11:49 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#827082229.20061023151028@topografix.com))

> Garmin's MapSource saves temperature and depth data for trackpoints using this GPX 1.1 extension schema - [link](http://www.garmin.com/xmlschemas/GpxExtensions/v3/GpxExtensionsv3.xsd)
>
> As long as there's an effort going on to standardize on a schema for heart rate and other measured values along a track, I'd like to see temp and depth considered as well.

tristanzvazquez+yahoo.com on Fri Dec 01 17:16:28 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#ekuud0+au8g@eGroups.com))

> Garmin has extensions for PhoneNumber, Address, Categories, DisplayMode, Depth, Temperature, and Proximity.

kerry.raymond+gmail.com on Mon Dec 04 12:07:07 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#02dc01c717df$a27bb2b0$3c13a8c0@cabernet))

> Certainly at the moment I create a waypoint, there is an ambient temperature for that time and place and the GPS unit might be able to record that. So temperature is a property of a waypoint, but not a property of a location (clearly temperature can vary at a given location over time). So temperature might arguably be an extension of GPX if GPX is about GPS waypoints etc and not about locations. 

egroups+topografix.com on Tue Dec 05 10:30:04 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#15910526580.20061205132718@topografix.com))

> I've been burned once already - I implemented temperature and depth in ExpertGPS when MapSource first added it to their GPX files.  A few months later my GPX files stopped validating, and I learned that Garmin had come out with a new version of their private schema, and deleted the old schema from their Web site!

egroups+topografix.com on Tue Nov 27 11:07:24 2007 ([link](https://www.topografix.com/gpx_mailing_list.asp#1782820653.20071127140721@topografix.com))

> Depth and Temperature aren't Garmin-specific, either.

egroups+topografix.com on Sun Jan 27 11:05:30 2008 ([link](https://www.topografix.com/gpx_mailing_list.asp#1787503072.20080127140526@topografix.com))

> I agree with the comments others have made that the current situation, where we have multiple private schemas all expressing common items like depth, temperature, and speed in their own way, is wrong. I would like to see a dozen or so officially-blessed extension schemas created to extend the base GPX 2.0 schema in different directions.

Matt+mnorwood.com on Thu Jul 17 17:08:56 2008 ([link](https://www.topografix.com/gpx_mailing_list.asp#20080717190853.xf5js3x6o28cs400@webmail.opentransfer.com))

> Say I want to add an element called "temperature" and it is a type of "float" from a namespace called "tmp"

egroups+topografix.com responded to a post on Tue Feb 10 06:55:16 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#843864940.20090210095530@topografix.com))

> \> sky conditions, precipitation, barometric pressure, air temperature, surface temperature, water temperature, humidity

egroups+topografix.com on Tue Jun 23 12:37:31 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#14410146148.20090623153302@topografix.com))

> There are at least four other observed values that, in my opinion, belong in an official extension schema. They are: temperature, depth, heart_rate, and cadence.  

robertlipe+usa.net on Tue Jun 23 13:50:51 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#883NFwuxP4150S02.1245790215@cmsweb02.cms.usa.net))

> "Temperature" could mean ambient, outside the cockpit, or at the bottom end of a fish-finder.
>
> "Depth" means different things to a boater than to a pilot.

robertlipe+usa.net on Wed Jun 24 12:42:05 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#886NFXTOd6348S17.1245872489@cmsweb17))

> I'm liking the small core kernel of GPX, a blessed set of extensions for the things that are common now (direction and tilt, temperature, etc.), and the use of the `<extensions>` tag for domain-specific problems that can be integrated into "blessed" status once they get enough exposure to be proven to be workable and useful.

robertlipe+gmail.com on Wed Dec 23 10:37:27 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#82a839a50912231037x561947b9w351daeb2772f48d@mail.gmail.com))

> `<temp>` Temperature
> 
> Must include a source: ambient, water, outside air.
> 
> `<depth>` Depth
> 
> Depth, in meters, such as reported by sonar.

robertlipe+gmail.com on Wed Dec 23 15:25:10 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#82a839a50912231525l46ae27a1o1788bc5794330df4@mail.gmail.com))

> Depth-finders for boats is where this seems to come up, but the other place we see "depth" in the industry is in describing "columns" of airspace, such as no-fly zones around tall buildings that matter more to low flying craft than high-flyers.

tt+smartcomsoftware.com on Thu Aug 05 07:49:52 2010 ([link](https://www.topografix.com/gpx_mailing_list.asp#010401cb3490$9ed4c3f0$dc7e4bd0$@com))

> As far as including this information in GPS XML is concerned, you could do an extension like Garmin do depth and other data in their extension. 

tt+smartcomsoftware.com on Tue May 27 01:14:10 2014 ([link](https://www.topografix.com/gpx_mailing_list.asp#000001cf7983$a3b9e760$eb2db620$@smartcomsoftware.com))

> In my sector (marine) some equipment manufacturers (e,g, Garmin) use an extended version of GPX for exporting tracks of boats, with additions for parameters such as depth that aren't in the core GPX spec.

on6vd+yahoo.co.uk on Wed Apr 04 11:15:35 2018 ([link](https://www.topografix.com/gpx_mailing_list.asp#pbjvb2+h952tg@YahooGroups.com)) - n.b. I think Harmen means "heading" and not "bearing"

> TrackPoint: speed, heartbeat, horizontalAccuracy, verticalAccuracy,  speedAccuracy, course, bearing, ambient temperature, air pressure

robertlipe+gmail.com on Sun Nov 10 14:00:32 2019 ([link](https://www.topografix.com/gpx_mailing_list.asp#CAGJ6+wpW7+bA0qN-4Bwv3SkAqrmAwZv5dZqgp1g60+rZ5DKdrg@mail.gmail.com))

> There are several extensions (fitness, temperature, etc.) that  are well proven and that could be collapsed into our core without much fuss if we all follow the normal "ignore tags you don't understand" guidelines in our readers. We'll need a few more contributors to really get behind such work to make it happen.




#### Fitness

egroups+topografix.com on Fri Nov 12 09:06:19 2004 (link)

> measured athlete data at each trackpoint: heartrate
> calculated athlete data: calories burned, etc.

renlindon+yahoo.com on Thu Oct 19 20:23:44 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#453C94A4.6090701@coruskate.net))

> The new(ish) breed of Garmin GPS receivers (Forerunner 305, Edge 305) have additional sensors for heart rate and cadence and log them with each point.  I'd like to be able to represent this data within the GPX format - what existing practice is there for encoding it?

egroups+topografix.com on Mon Oct 23 12:11:49 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#827082229.20061023151028@topografix.com))

> Garmin's MapSource saves temperature and depth data for trackpoints using this GPX 1.1 extension schema - [link](http://www.garmin.com/xmlschemas/GpxExtensions/v3/GpxExtensionsv3.xsd)
>
> ExpertGPS reads and writes this data as well.
>
> As long as there's an effort going on to standardize on a schema for heart rate and other measured values along a track, I'd like to see temp and depth considered as well.
>
> I'll support heart rate and cadence in my software if a standard schema emerges.

robertlipe+usa.net on Fri Dec 22 09:36:20 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#20061222173431.GT19437@rjloud.localdomain))

> I get the impression that a lot of folks in this market just want relatively straightforward HRM/Cadence/Temp collection.

egroups+topografix.com on Tue Jun 23 12:37:31 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#14410146148.20090623153302@topografix.com))

> There are at least four other observed values that, in my opinion, belong in an official extension schema.  They are: temperature, depth, heart_rate, and cadence.  

robertlipe+usa.net on Tue Jun 23 13:50:51 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#883NFwuxP4150S02.1245790215@cmsweb02.cms.usa.net))

> Wheel cadence, crank cadence, or both?

robertlipe+gmail.com on Wed Dec 23 10:37:27 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#82a839a50912231037x561947b9w351daeb2772f48d@mail.gmail.com))

> `<heartrate>` Heart Rate
> Units: beats per minute
>
> `<cadence>` Cadence
> Units: revolutions per minute

egroups+topografix.com on Wed Dec 30 09:46:45 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#817253482.20091230124632@topografix.com))

> It would be helpful to have some of the HW vendors chime in that they are aware of this effort.  Will Garmin eventually migrate from private extensions for common things like cadence, heartrate to a public GPX extension?  Is what we're building what they need?

robertlipe+gmail.com on Sun Nov 10 14:00:32 2019 ([link](https://www.topografix.com/gpx_mailing_list.asp#CAGJ6+wpW7+bA0qN-4Bwv3SkAqrmAwZv5dZqgp1g60+rZ5DKdrg@mail.gmail.com))

> There are several extensions (fitness, temperature, etc.) that  are well proven and that could be collapsed into our core without much fuss if we all follow the normal "ignore tags you don't understand" guidelines in our readers. We'll need a few more contributors to really get behind such work to make it happen.

robertlipe+gmail.com on Mon Jan 04 10:14:06 2010 ([link](https://www.topografix.com/gpx_mailing_list.asp#82a839a51001041013g5ab74bd3l97d6f5698da5300e@mail.gmail.com))

> heartrate and cadence (both wheel and crank) are already in the proposal.




#### Nautical

egroups+topografix.com on Fri Nov 12 09:06:19 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#703411000.20041112120550@topografix.com))

> engine speed, heading, depth, temperature
>
> distance, bearing, speed over ground, grade, etc.



#### Enhanced Source

jeremy+groundspeak.com on Wed Nov 06 17:23:09 2002 ([link](https://www.topografix.com/gpx_mailing_list.asp#00c301c285fc$3756bf80$84a79642@groundspeak.biz))

> This hasn't been discussed, but I'd like to add this: There is a
> `<src>` tag but should separate manufacturer and software version from the
> model. Like: `<src mfr="Garmin" ver="1.2">eTrex Legend</src>`

jeremy+groundspeak.com on Thu Nov 07 13:11:35 2002 ([link](https://www.topografix.com/gpx_mailing_list.asp#004201c286a2$3c5a9af0$84a79642@groundspeak.biz))

> `<src mfr="Garmin" model="eTrex Vista" ver="1.2" /> `
>
> or even...
>
> `<src mfr="Garmin" ver="1.2">eTrex Vista</src> `


