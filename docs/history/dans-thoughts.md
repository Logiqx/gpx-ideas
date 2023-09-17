## GPX Developers Mailing List and GPSXML Archive

### Dan's Thoughts

This is a small collection of posts that provide some insight into Dan's thoughts on the future of GPX.



#### Nov 2004

egroups+topografix.com on Fri Nov 12 09:06:19 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#703411000.20041112120550@topografix.com))

```
There are actually a number of different measurements that users might
want to store.  We should probably allow all or most of them.
course - the direction from startpoint to endpoint
heading - the direction your boat is actually pointing
bearing - the direction from your current position to the endpoint
track - the direction you're actually going (different from heading if
there's a cross-current, for example)
speed - how fast your wheels, screws, propellers are turning
speed over ground - how fast you're actually moving (factoring in
currents)

Some of these can be calculated after the fact using
distance/speed/time calculations.  Others are direct measurements from
the compass and tachometer on your craft.

I haven't read any arguments against having course and speed be
expressable in GPX.  I'd like to see it possible to express them.  I'm
not convinced they belong in the main GPX schema, though.  (In line with
my current thinking that very very little belongs in the main schema)

I'd like to see a major gutting of wptType in GPX 1.2, and I'd like to
see a separate trkptType created for tracks.  Currently wptType is
used for waypoints (good), routes (good - they are composed of
waypoints), and tracks (bad, IMO).  In GPX 1.0, trackpoints were
identical to waypoints, but they had two additional elements (course
and speed).  I failed to remember that in GPX 1.1 and mistakenly
combined the two types, thinking they were identical.

I'd like to see us take a broad look at what's currently missing from
GPX that should be added, and what's currently in GPX 1.1 that should
be changed or moved.  I think some general categories of data will
emerge, and we can consider grouping similar items together in
separate schemas, much as we're doing for line-drawing and stylistic
stuff.

At the same time, I'd like to revive the discussion about how changes
to the schemas should be proposed, discussed, and adopted, so that
developers can have a timeline for adopting new GPX schemas into their
product schedules.

Some suggested additions I've heard so far:

nautical direct measurements at each trackpoint: engine speed, heading, depth,
temperature
calculated values at each trackpoint: distance, bearing, speed over
ground, grade, etc.

measured athlete data at each trackpoint: heartrate
calculated athlete data: calories burned, etc.

public schema for aviation: Paul Tomblin's schema, AeroPlanner.com
schema

change <magvar> range to (-180, 180]

Add <extensions> to the following GPX 1.1 complex types:
copyrightType
linkType
emailType
personType
ptType
ptsegType
boundsType
(see my email on 22 Sept, 2004)

Proximity waypoints

Real-time tracking info

Maybe all of these things can get lumped into their own schemas and
can be made to work with the existing GPX 1.1 schema.  More likely,
we'll find some minor changes to the main 1.1 schema need to be made.
It would be very helpful to get as many proposed additions out in the
open now, so we can try to propose a solution that handles all of
them.
```

egroups+topografix.com on Fri Nov 12 10:52:19 2004 ([link](https://www.topografix.com/gpx_mailing_list.asp#94150845.20041112135142@topografix.com))

```
T> Forgive my ignorance, but why on earth would you want to add things like
T> heart rate, engine speed, depth, etc.?

I'll fight tooth and nail along side you to make sure heart rate never
gets added to the main GPX schema.  But if you look at what's
happening in the endurance training market right now, you'll realize
that heart rate data combined with position, speed, and elevation data
(from GPS) is going to be the next big thing in personal training.

T> GPX is about global positioning and no GPS device I know of tells me my
T> heart rate. If developers want to combine non-GPS data with their GPS data
T> they are welcome to do so by extending the GPX format to fit their unique
T> needs.

If we can provide an opportunity for various equipment manufacturers
(Ed gave you a link to Timex' offering) and Web training sites (try
http://www.trainingpeaks.com or http://www.motionbased.com ) to come
together and create a vendor-neutral schema for heart rate data - why
shouldn't we?  As a programmer, I'd rather deal with one public schema
for heart rate than have to deal with each vendor's private
extensions.

Of course, if heart rate doesn't concern you or your application, you
can ignore it and any schema that emerges.  I'm ignoring it for now,
but I suspect my customers will be clamoring for it within a year.

T> Rather than trying to come up with a spec that will work for everyone in
T> every scenario, GPX should be a solid base that works for GPS and mapping
T> needs. 

We're pretty much there, right?  Where should we go from here?  Rather
than shut the mailing list down and let people extend the schema on
their own, why not let smaller groups find each other and work on
creating sub-schemas to handle stuff that's related to, but not directly
associated with, the traditional GPS position/speed/elevation/time.

T> Then the focus should be getting corporate support. Getting Garmin, Delorme,
T> and or Topo to support GPX will go a long ways toward legitimizing this
T> format.
 
The most convincing way I know to do this is to present them with a
set of schemas that handle 100% of the things they want to express.
Topo! has colored tracks.  Can GPX do this?  (that's the purpose of my
gpx_style sub-schema)  Garmin just introduced temperature logging for
trackpoints.  Can GPX do this?

Honestly, I thought GPX 1.1 would be the final revision of the main
GPX schema, and at this point there would be nothing to do but work on
related public schemas.  I've been focusing on the map drawing
features that Topo!, OziExplorer, and other mapping programs would
insist on before adopting GPX.  In doing so, I've come across a few
things that lead me to believe a GPX 1.2 revision will be needed.  I
realize how disruptive it is to switch to a new version, so if we
really do need to make some changes in the future, I'd rather get them
all worked out and lump them all together instead of dealing with them
one at a time as people discover them.
```



#### Aug 2006

egroups+topografix.com on Fri Aug 25 13:16:02 2006 ([link](https://www.topografix.com/gpx_mailing_list.asp#885169760.20060825161206@topografix.com))

```
>  Is an extension schema better or a new version of GPX incorporating
>  perhaps other new elements?

If we do a new GPX 1.2 or 2.0 schema, I would suggest breaking most of
the GPX 1.1 elements off into their own schemas for reusability
purposes.

This stuff all belongs together somewhere:
<fix> fixType </fix> [0..1] ?
<sat> xsd:nonNegativeInteger </sat> [0..1] ?
<hdop> xsd:decimal </hdop> [0..1] ?
<vdop> xsd:decimal </vdop> [0..1] ?
<pdop> xsd:decimal </pdop> [0..1] ?
<ageofdgpsdata> xsd:decimal </ageofdgpsdata> [0..1] ?
<dgpsid> dgpsStationType </dgpsid> [0..1] ?

This needs to get fixed so it can be extended:
<link> linkType </link>
<xsd:complexType name="linkType">
<xsd:sequence>
<-- elements must appear in this order -->
<xsd:element name="text" type="xsd:string" minOccurs="0"/>
<xsd:element name="type" type="xsd:string" minOccurs="0"/>
</xsd:sequence>
<xsd:attribute name="href" type="xsd:anyURI" use="required"/>
</xsd:complexType>

It seems to me that the best way to proceed would be to work on making
a bunch of highly-specialized sub-schemas that can all be mixed
together to meet individual needs.

We do need to come up with some answers as to how GPX should handle
things like photos embedded in waypoints, waypoints embedded in
photos, and your hotspots and other map symbols.
```




#### 27 Jan 2008

egroups+topografix.com on Sun Jan 27 11:05:30 2008 ([link](https://www.topografix.com/gpx_mailing_list.asp#1787503072.20080127140526@topografix.com))

```
My own personal opinion is that a new version of GPX is needed, and
that it should be 2.0, not 1.2 (Signifying that a GPX 1.0 or 1.1
document may not validate as a GPX 2.0 document) I would strip the
base GPX 2.0 schema down to the bare minimum, removing things like
hdop, magvar, and ageofdgpsdata to their own officially-blessed
extension schemas.

I agree with the comments others have made that the current situation,
where we have multiple private schemas all expressing common items
like depth, temperature, and speed in their own way, is wrong. I would
like to see a dozen or so officially-blessed extension schemas created
to extend the base GPX 2.0 schema in different directions. I'd like to
see a commitment from developers using the GPX format to develop
common "officially-blessed" schemas for data that might have a use in
other hardware or software applications, and to only use private
schemas for truly private data that has no meaning outside of that
developer's application.

I'd also like to see some of our XML design gurus step forward and
propose a framework for future GPX schemas based on the latest best
practices in XML design.
```



#### 23 Jun 2009

egroups+topografix.com on Tue Jun 23 12:37:31 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#14410146148.20090623153302@topografix.com))

```
> Would an official GPX extension to 1.1 that added <extensions><speed> and
> <extensions><course> get any traction with fellow developers? Like most
> developers, I could probably add it to GPSBabel without a lot of fuss if we
> got together and worked out the official angle brackets.

I'd support an official extension schema. But my endorsement won't
mean much, because my apps don't currently
consider speed and course to be anything but calculated values
(distance/time). So when I output GPX data, I'd skip these two new
tags, since I'm not adding any new information that couldn't just be
calculated by the program that parsed my GPX output. (That is, I think
<gpx_ext_observed::speed> or whatever it is called should be reserved
for actual observed data, not speed as calculated from distance
divided by time.)

There are at least four other observed values that, in my opinion,
belong in an official extension schema.  They are: temperature, depth,
heart_rate, and cadence.  (Recognize these, Garmin?)

And then there are the POI extensions.  <garmin::phone_number> or
whatever we have now on the nuvis.

Unfortunately, because there's been no interest in a GPX 1.2 spec,
developers have been putting common data that ought to be shared
between apps in an official schema into private namespace schemas, so
we end up with <garmin:color> and <garmin:phone_number> rather than
<gpx_style:color> and <gpx_poi:phone_number>

Sorry to muddy the issue, but I think any discussion of what we do
about course and speed has to keep in mind the other common bits of
GPS info that are currently getting stuffed in private schemas.  (And
I'm not trying to pick on Garmin, merely using them as an example
since most of us are familiar with their GPX output)
```

egroups+topografix.com on Tue Jun 23 14:37:22 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#201129910.20090623173255@topografix.com))

```
> I'm trying to understand if you [meaning Simon] think "GPX" should
> really be only concerned with things that are strictly GPS. (And I'm
> already on record in this very thread as noting it's a slippery
> slope!)

My personal opinion is that we made a grave mistake by declaring that
GPX was about "exchanging GPS info" when we should have said it was
about "exchanging spatial info", or "exchanging everything and
anything that someone could possibly attach to a real-world location".

For better or for worse, the world doesn't want an XML schema for
exchanging GPS waypoints.  They want an XML schema for exchanging
waypoints, POIs, geocaches, vector maps, flight plans, and a bunch of
other things all based around the fact that they are tied to
real-world points and lines.

I'd really like to see us get back to extending GPX to provide a
common solution for the data exchange problems that are flourishing
again as GPS technology extends beyond the Garmin GPS 12 and Magellan
315 receivers that were our model when GPX 1.0 was written.

Seriously, we just sat back and watched 20 different automotive GPS
manufacturers create 20 different file formats for POIs. Would things
have been different (better?) if GPX had offered a common extension
schema for things like address and phone number?
```

