## GPX Core

### Clarifications

#### Elevation

The existing GPX schema does not make it clear whether elevation represents height above the ellipsoid or height above the geoid.

```xml
<xsd:element name="ele" type="xsd:decimal" minOccurs="0">
  <xsd:annotation>
    <xsd:documentation> Elevation (in meters) of the point. </xsd:documentation>
  </xsd:annotation>
</xsd:element>

<xsd:element name="geoidheight" type="xsd:decimal" minOccurs="0">
  <xsd:annotation>
    <xsd:documentation> Height (in meters) of geoid (mean sea level) above WGS84 earth ellipsoid. As defined in NMEA GGA message. </xsd:documentation>
  </xsd:annotation>
</xsd:element>

<xsd:attribute name="lat" type="latitudeType" use="required">
<xsd:annotation>
<xsd:documentation> The latitude of the point. This is always in decimal degrees, and always in WGS84 datum. </xsd:documentation>
</xsd:annotation>
</xsd:attribute>

<xsd:attribute name="lon" type="longitudeType" use="required">
  <xsd:annotation>
    <xsd:documentation> The longitude of the point. This is always in decimal degrees, and always in WGS84 datum. </xsd:documentation>
  </xsd:annotation>
</xsd:attribute>
```

Proposed schema simply adds some more words to the documentation for `<ele>` and `<geoidheight>`.


```xml
<xsd:element name="ele" type="xsd:decimal" minOccurs="0">
  <xsd:annotation>
    <xsd:documentation> Elevation (in meters) of the point above the geoid (approximation of mean sea level). This is referred to as the orthometric height, and always in WGS84 datum.</xsd:documentation>
  </xsd:annotation>
</xsd:element>

<xsd:element name="geoidheight" type="xsd:decimal" minOccurs="0">
  <xsd:annotation>
    <xsd:documentation> Height (in meters) of the geoid (approximation of mean sea level) above the WGS84 ellipsoid. As defined in the NMEA GGA sentence. </xsd:documentation>
  </xsd:annotation>
</xsd:element>

<xsd:attribute name="lat" type="latitudeType" use="required">
<xsd:annotation>
<xsd:documentation> The latitude of the point. This is always in decimal degrees, and always in WGS84 datum. </xsd:documentation>
</xsd:annotation>
</xsd:attribute>

<xsd:attribute name="lon" type="longitudeType" use="required">
  <xsd:annotation>
    <xsd:documentation> The longitude of the point. This is always in decimal degrees, and always in WGS84 datum. </xsd:documentation>
  </xsd:annotation>
</xsd:attribute>
```

References

- See some useful [links](../elevation.md) and discussion on [Github](https://github.com/Logiqx/gpx-ideas/discussions/1) for more information about the ellipsoids and geoids.



#### Precision

It is probably worth providing some guidance on the maximum precision for common items.

- Latitude and longitude values should not exceed 9 decimal places
- Elevation should not exceed 4 decimal places

Garmin Connect currently provides far too much precision:

```xml
<trkpt lat="50.57713455520570278167724609375" lon="-2.46620426885783672332763671875">
  <ele>2.2000000476837158203125</ele>
  <time>2022-06-11T12:23:41.000Z</time>
  <extensions>
  <ns3:TrackPointExtension>
    <ns3:atemp>25.0</ns3:atemp>
    <ns3:hr>97</ns3:hr>
  </ns3:TrackPointExtension>
  </extensions>
</trkpt>
```

UBX-NAV-HPPOSLLH (high precision geodetic position solution) of the u-blox F9 high precision GNSS receiver was used for reference.

Perhaps suitable levels of precision can be clarified in `<xsd:documentation>`



#### Magnetic Variation

This isn't simply a clarification, but rather the correction of an existing definition, and therefore a candidate for GPX 1.2:

```xml
<xsd:element name="magvar" type="degreesType" minOccurs="0">
  <xsd:annotation>
    <xsd:documentation> Magnetic variation (in degrees) at the point </xsd:documentation>
  </xsd:annotation>
</xsd:element>

<xsd:simpleType name="degreesType">
  <xsd:annotation>
    <xsd:documentation> Used for bearing, heading, course. Units are decimal degrees, true (not magnetic). </xsd:documentation>
  </xsd:annotation>
  <xsd:restriction base="xsd:decimal">
    <xsd:minInclusive value="0.0"/>
    <xsd:maxExclusive value="360.0"/>
  </xsd:restriction>
</xsd:simpleType>
```

Proposed to use a new simple type for `<magvar>` and various GPX extensions:

```xml
<xsd:element name="magvar" type="angleType" minOccurs="0">
  <xsd:annotation>
    <xsd:documentation> Magnetic variation (in degrees) at the point. </xsd:documentation>
  </xsd:annotation>
</xsd:element>

<xsd:simpleType name="angleType">
  <xsd:annotation>
    <xsd:documentation> Used for magnetic variation and some GPX extensions. Units are decimal degrees, positive = clockwise, negative = counter-clockwise. </xsd:documentation>
  </xsd:annotation>
  <xsd:restriction base="xsd:decimal">
    <xsd:minInclusive value="-180.0"/>
    <xsd:maxExclusive value="180.0"/>
  </xsd:restriction>
</xsd:simpleType>
```

The impact of the `<magvar>` change needs to be assessed / quantified, bearing in mind the following assertions:

- Generic code can easily be written to interpret `<magvar>` from GPX 1.1 files (0 to 360) and GPX 1.2 files (-180 to +180).
- Magnetic variation is rarely found in GPX files, so changing the definition will only impact a relatively small number of users.
