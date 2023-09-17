## GPX Developers Mailing List and GPSXML Archive

### Extending GPX 1.1

robertlipe+gmail.com on Wed Dec 23 10:37:27 2009 ([link](https://www.topografix.com/gpx_mailing_list.asp#82a839a50912231037x561947b9w351daeb2772f48d@mail.gmail.com))



### Status

Draft. Consuming focus isn't on angle brackets yet.



### Summary


Publish an extention to GPX 1.1 to address perceived shortcomings with GPX as a storage for GPS and similar data.



### Background

GPX [http://www.topografix.com/gpx.asp](http://www.topografix.com/gpx.asp) is an XML file format focusing on a lightweight interchange of GPS data. It is produced or consumed by over a
hundred applications [http://www.topografix.com/gpx_resources.asp](http://www.topografix.com/gpx_resources.asp), making it a leading representation of GPS data. It has gained such widespread use that many Garmin and other receivers actually parse and generate GPX as their native file format.


GPX 1.0 was published in in 2002 with an incremental bump to GPX 1.1 to add an <extensions> scheme and a few other enhancements in August of 2004.

The specification is showing a bit of age. Many of the concepts in it are rooted in GPS receivers that were designed around the turn of the decade. Concepts like geotagging, cross-file linking, device sensors such as compass or accelerometers, and representation in 3D spinny globes were simply not widespread at the time.



### Overview

The GPX 1.1 schema [http://www.topografix.com/GPX/1/1/](http://www.topografix.com/GPX/1/1/) defines an extensionsType [http://www.topografix.com/gpx/1/1/#type_extensionsType](http://www.topografix.com/gpx/1/1/#type_extensionsType) that
may be used to extend most data type by adding another schema.

We will extend GPX to include current interesting sensor data such as compass data, select workout data, orientation (heading/tilt/roll), and similar data, but while we have the XSD open, we'll capture some of the common requests of the GPX user base that don't complicate our implementation just in the name of having a single, comprehensive, extension.




### Example of current art using extensions.


Garmin has successfully extended GPX 1.1. Here's an example of a single waypoint and a two point track:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<gpx
version="1.0"
creator="GPSBabel - http://www.gpsbabel.org"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns="http://www.topografix.com/GPX/1/1"
xsi:schemaLocation="http://www.topografix.com/GPX/1/1
http://www.topografix.com/GPX/1/1/gpx.xsd
http://www.garmin.com/xmlschemas/GpxExtensions/v3
http://www.garmin.com/xmlschemas/GpxExtensions/v3/GpxExtensionsv3.xsd
http://www.garmin.com/xmlschemas/TrackPointExtension/v1
http://www.garmin.com/xmlschemas/TrackPointExtension/v1/TrackPointExtensionv1.xsd
">

<time>2009-07-10T15:52:58Z</time>
<bounds minlat="25.061784000" minlon="-122.274499000" maxlat="50.982884000" maxlon="121.640268000"/>

<wpt lat="35.825017000" lon="-86.847151000">
  <ele>244.540000</ele>
  <time>2008-04-26T17:47:58Z</time>
  <name>HOME</name>
  <cmt>26-APR-08 12:46:58PM</cmt>
  <desc>26-APR-08 12:46:58PM</desc>
  <sym>Residence</sym>
</wpt>

  <trk>
    <name>Current Track: 11 MAY 2008 12:46</name>
      <trkseg>
        <trkpt lat="35.825031000" lon="-86.847124000">
          <ele>262.100000</ele>
          <time>2008-05-11T17:46:24Z</time>
          <extensions>
            <gpxtpx:TrackPointExtension>
              <gpxtpx:atemp>22.4</gpxtpx:atemp>
            </gpxtpx:TrackPointExtension>
        </extensions>
      </trkpt>

      <trkpt lat="35.825016000" lon="-86.847110000">
        <ele>261.140000</ele>
        <time>2008-05-11T17:47:15Z</time>
        <extensions>
          <gpxtpx:TrackPointExtension>
            <gpxtpx:atemp>22.4</gpxtpx:atemp>
          </gpxtpx:TrackPointExtension>
        </extensions>
      </trkpt>
    </trkseg>
  </trk>
</gpx>
```

Cluetrust has also made an attempt at extending GPX specifically for the sporting markets. See [http://www.cluetrust.com/Schemas/gpxdata10.xsd](http://www.cluetrust.com/Schemas/gpxdata10.xsd)



### Extensions

The extensions break down into four categories: sensor data, physical orientation, unique IDs, and human-recognizable addresses. Some of the items
may not make immediate sense for each of the waypoint, track, route (what is the heart rate of a point?) but no attempt is made to separate them. If you
want to use cadence for the average RPMs of a windmill or something similar, we don't go out of our way to stop you.



#### Sensor Data

##### mSpeed - Measured Speed

Speed as measured via an external source such as water transducer or via doppler calculation. Notably, this is NOT simply speed as computed via successive timestamped position fixes.

Units: meters per second

Extends: wptType, trkType, rteType

Simple Type



##### mCourse - Measured Course

Instantaneous direction of motion or facing direction as computed via a non-GPS source such as a compass. This is not course as computed via successive position fixes.

Units: degrees, true

Extends: wptTpe, trkType, rteType

SimpleType



##### temp - Temperature

Must include a source: ambient, water, outside air.

Units: degrees Celsius

Extends: wptTpe, trkType, rteType

SimpleType



##### depth - Depth

Depth, in meters, such as reported by sonar.

Extends: wptType, trkType, rteType

Simple Type



##### heartrate - Heart Rate

Heart rate

Units: beats per minute

Extends: wptType, trkType, rteType

SimpleType



##### cadence - Cadence

Revolutions per minute of crank or wheel.

TODO - Decide if a complex type with a source is better or worse than two simple types.

Units: revolutions per minute

ComplexType ??

<here down gets sketchy>



#### Physical Orientation

Orientation Describes the rotation of an object in space, such as the orientation of a flux gate compass.

ComplexType

##### heading

Rotation about the z axis (normal to the Earth's surface). A value of 0 (the default) equals North. A positive rotation is clockwise around the z-axis.

Units: degrees 0-360

SimpleType

##### tilt

Rotation about the x axis. A positive rotation is clockwise around the x-axis

Units: degrees 0-360

SimpleType


##### roll

Rotation about the y axis. A positive rotation is clockwise around the y-axis.

Units: degrees 0-360

SimpleType



#### Unique IDs

`<guid>` A GUID, uniquely identifying this object so that it may be referenced externally

SimpleType



#### Addresses

`<address>` street, city, state, country, postal

ComplexType

`<phone>` Phone

Simple May repeat. *Allow infinite? Try to separate H/W/Fax?*



### Example XSD

2009-10-15 - Here's a snapshot of the XSD

```xml
<?xml version="1.0"?>
<xsd:schema targetNamespace="http://www.robertlipe.com/blahblah"
    elementFormDefault="qualified"
    xmlns="http://www.robertlipe.com/blahblah"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema">

    <xsd:element name="GPXExtension" type="GPXExtension" />

    <xsd:complexType name="GPXExtension">
    <xsd:sequence>
      <!-- TODO: Tigthten up these types -->
      <xsd:element name="mSpeed" type="xsd:double" minOccurs="0" />
      <xsd:element name="mCourse" type="degreesType" minOccurs="0" />
      <xsd:element name="temperature" type="temperatureType" minOccurs="0" maxOccurs="unbounded"/>
      <xsd:element name="depth" type="xsd:double" minOccurs="0" />
      <xsd:element name="heartrate" type="xsd:double" minOccurs="0" />
      <xsd:element name="cadence" type="xsd:double" minOccurs="0" />
      <xsd:element name="Address" type="AddressType" minOccurs="0" />
      <xsd:element name="Phone" type="PhoneType" minOccurs="0" maxOccurs="unbounded"/>
      <xsd:element name="Orientation" type="OrientationType" minOccurs="0" />
    </xsd:sequence>
  </xsd:complexType>

  <xsd:simpleType name="tempSource">
     <xsd:restriction base="xsd:token">
       <xsd:enumeration value="ambient"/>
       <xsd:enumeration value="water"/>
       <xsd:enumeration value="outer"/>
     </xsd:restriction>
   </xsd:simpleType>

   <xsd:complexType name="temperatureType">
     <xsd:simpleContent>
       <xsd:extension base="xsd:token">
         <xsd:attribute name="source" type="tempSource" default="ambient" />
       </xsd:extension>
     </xsd:simpleContent>
  </xsd:complexType>

  <!-- From the GPX 1.1 XSD -->
  <xsd:simpleType name="degreesType">
    <xsd:annotation>
      <xsd:documentation>
            Used for bearing, heading, course.  Units are decimal degrees, true (not magnetic).
      </xsd:documentation>
    </xsd:annotation>
    <xsd:restriction base="xsd:decimal">
      <xsd:minInclusive value="0.0"/>
      <xsd:maxExclusive value="360.0"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:complexType name="AddressType">
    <xsd:sequence>
    <xsd:element maxOccurs="2" type="xsd:token" name="streetAddress" />
    <xsd:element minOccurs="0" type="xsd:token" name="city" />
    <xsd:element minOccurs="0" type="xsd:token" name="state" />
    <!-- ISO 3166 ? -->
    <xsd:element minOccurs="0" type="xsd:token" name="country" />
    <xsd:element minOccurs="0" type="xsd:token" name="postalCode" />
    </xsd:sequence>
  </xsd:complexType>

  <xsd:simpleType name="phoneType">
     <xsd:restriction base="xsd:token">
       <xsd:enumeration value="home"/>
       <xsd:enumeration value="work"/>
       <xsd:enumeration value="fax"/>
     </xsd:restriction>
   </xsd:simpleType>
<!-- Maybe phoneType is an arbitrary string.  Maybe phone # should be stricter, but how well will that internationalize? -->
  <xsd:complexType name="PhoneType">
    <xsd:simpleContent>
      <xsd:extension base="xsd:token">
        <xsd:attribute name="category" type="phoneType" />
      </xsd:extension>
    </xsd:simpleContent>
  </xsd:complexType>

  <xsd:complexType name="OrientationType">
    <xsd:sequence>
      <xsd:element name="heading" type="degreesType" minOccurs="0" />
      <xsd:element name="tilt" type="degreesType" minOccurs="0" />
      <xsd:element name="roll" type="degreesType" minOccurs="0" />
    </xsd:sequence>
  </xsd:complexType>
</xsd:schema>
```



### Example GPX

And here's a horror of a GPX file that shows what such a GPX might look like:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<gpx
  version="1.1"
  creator="GPSBabel - http://www.gpsbabel.org"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://www.topografix.com/GPX/1/1"
  xmlns:gpxe="http://www.robertlipe.com/blahblah"
  xsi:schemaLocation="http://www.topografix.com/GPX/1/1
http://www.topografix.com/GPX/1/1/gpx.xsd
http://www.robertlipe.com/blahblahgpxe.xsd">
<wpt lat="1.000000000" lon="1.000000000">
  <name>WPT001</name>
  <cmt>WPT001</cmt>
  <desc>WPT001</desc>
  <extensions>
    <GPXExtension xmlns="http://www.robertlipe.com/blahblah">
      <mSpeed>120</mSpeed>
      <mCourse>93.1</mCourse>
      <temperature source="water">23.1</temperature>
      <temperature> 35.1</temperature>
      <depth>1234</depth>
      <heartrate>56</heartrate>
      <cadence>78</cadence>
        <Address>
          <streetAddress>1600 Oak Street</streetAddress>
          <streetAddress>Building 1234</streetAddress>
          <city>Mountain View</city>
          <state>TN</state>
          <country>USA</country>
          <postalCode>37064</postalCode>
        </Address>
        <Phone category="home">615-123-4568</Phone>
        <Phone category="work">615-234-5678</Phone>
        <Phone category="fax">615-234-5678</Phone>
        <Orientation>
          <heading>12</heading>
          <tilt>34</tilt>
          <roll>56</roll>
        </Orientation>
    </GPXExtension>
  </extensions>
</wpt>
</gpx>
```
