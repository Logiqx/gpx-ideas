## GPX Extensions - Icons

### Background

This document has been written to illustrate the possibility of a generic approach for icons within GPZ files.

There are at least a couple of Android apps which already support GPZ files and custom icons via the `<sym>` element.

e.g. If `<sym>dining</sym>` is within `<wpt>` / `<trkpt>` / `<rtept>` then `icons/dining.png` will be displayed on the map.

This basic functionality has been demonstrated to work very nicely, but there are some additional capabilities which are desirable.



### Features / Capabilities

This extension has been drafted to illustrate some desirable features / capabilities:

- Support for multiple icon folders, allowing the creators of GPZ files to logically group their icons.
- Support for anchor points / hot spots, applied to groups of icons via a single definition in the GPX metadata.
- Scope for multiple resolutions of icons, thus catering for different display resolutions and platforms.

These features can all be confined to the `<metadata>` section of the GPX file, leaving  `<wpt>` / `<trkpt>` / `<rtept>` elements looking simple.



### Examples

#### Example 1

A simple example can show the use of a `dining` icon:

```xml
<wpt lat="50.514898" lon="-2.455531">
  <name>Lobster Pot</name>
  <sym>dining</sym>
  <type>icon</type>
</wpt>
```

The `<metadata>` section provides the information required to locate the `dining` icon within the GPZ file:

```xml
<metadata>
  <extensions>
    <ico:style id="icon">
      <ico:path href="icons/shapes" />
    </ico:style>
  </extensions>
</metadata>
```

The metadata above can be summarised as follows:

- `<ico:style id="icon">` defines a single `icon` style, which can be used by `<type>` of `<wpt>` / `<trkpt>` / `<rtept>`.
- `<ico:path href="icons/shapes">` specifies the path / folder containing the icon file(s).

Based on the information in this example an app can then be expected to display the dining icon, centered over the waypoint.

![dining](0/1/icons/shapes/dining.png)



#### Example 2

A slightly more complex example uses two different types of icon (pushpin and paddle) with different anchor points / hotspots:

```xml
<wpt lat="50.513380" lon="-2.456620">
  <name>Portland Bill</name>
  <desc>Recommended viewpoint for Portland Bill</desc>
  <sym>ylw-pushpin</sym>
  <type>pushpin-ico</type>
</wpt>
  
<wpt lat="50.222776" lon="-3.642783">
  <name>Start Point</name>
  <desc>Recommended viewpoint for Start Point</desc>
  <sym>ylw-blank</sym>
  <type>paddle-ico</type>
</wpt>
```

The `<metadata>` includes all of the information relating to pushpin and paddle icons:

```xml
<metadata>
  <extensions>
    <ico:style id="pushpin-ico">
      <ico:path href="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:path>
    </ico:style>
    <ico:style id="paddle-ico">
      <ico:path href="icons/paddle">
        <ico:size x="64" y="64" />
        <ico:hotspot x="32" y="1" />
      </ico:path>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

The metadata extension can be summarised as follows:

- Two different icon styles that can be referenced by the `<type>` element of `<wpt>` / `<trkpt>` / `<rtept>`.
- A single image format (PNG) has been listed, but more than one image format may be specified.
- The sizes of icons are optional, but can be stated explicitly. Explicit sizes are probably quite desirable for applications supporting icons.
- The anchor points / hotspots are unique to each icon style. All images in the same path / folder share the same anchor point / hotspot.

For example, pushpin icons have an anchor point / hotspot which is towards the bottom-left of the icon, right at the sharp point.

![dining](0/1/icons/pushpin/ylw-pushpin.png)

Likewise, paddle icons have an anchor point / hotspot with is bottom-center of the icon.

![dining](0/1/icons/paddle/ylw-blank.png)

Although the difference between the pushpin and paddle icons is relatively small, anchor points / hotspots provide obvious benefits.



#### Example 3

An alterative approach for example 2 is to use a single `icon` style, instead of `pushpin-ico` and `paddle-ico`.

```xml
<wpt lat="50.513380" lon="-2.456620">
  <name>Portland Bill</name>
  <desc>Recommended viewpoint for Portland Bill</desc>
  <sym>ylw-pushpin</sym>
  <type>icon</type>
</wpt>
  
<wpt lat="50.222776" lon="-3.642783">
  <name>Start Point</name>
  <desc>Recommended viewpoint for Start Point</desc>
  <sym>ylw-blank</sym>
  <type>icon</type>
</wpt>
```

The `<metadata>` section provides all of the information within the single `icon` style:

```xml
<metadata>
  <extensions>
    <ico:style id="icon">
      <ico:path href="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:path>
      <ico:path href="icons/paddle">
        <ico:size x="64" y="64" />
        <ico:hotspot x="32" y="1" />
      </ico:path>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

This single `icon` style is slightly neater implementation of example 2, which used two icon styles;  `pushpin-ico` and `paddle-ico`.

It should be noted that the pushpin and paddle icons still have their own anchor points / hotspots.



### Further Discussion

#### Icon Sizes

It has been shown that metadata allows for icon sizes to be specified for individual paths / folders.

One of the main benefits of explicit sizes is the provision for different icon sizes for various display resolutions and platforms.

Applications can decide for themselves how the paths / folders should be searched for the most suitable size(s) available.



#### Anchor Points / Hotspots

This extension only uses pixel units for icon sizes and the specification of anchor points / hotspots.

KML / KMZ supports pixels, fractions and mixtures thereof, but it is worth remembering that it will always be possible to determine pixel offsets.

The decision to only use pixel units for anchor points / hotspots keeps things simple and avoids unnecessary complexity.



#### Scalable Vector Graphics (SVG)

It is conceivable that some creators of GPZ files may wish to include icons in SVG format.

When using SVG icons and wanting to define anchor points / hotspots, simply define a "virtual" size, plus the equivalent hotspot.

```xml
<ico:path href="icons/svg">
  <ico:size x="256" y="256" />
  <ico:hotspot x="128" y="0" />
</ico:path>
<ico:suffix>svg</ico:suffix>
```



### Application Development

Applications capable of reading GPZ files and displaying icons will not require any complicated logic to support the concept of icon styles.

The presence of a `<sym>` element indicates an icon and the `<type>` element indicates the icon style - e.g. `pushpin-ico`.

```xml
<wpt lat="50.513380" lon="-2.456620">
  <name>Portland Bill</name>
  <desc>Recommended viewpoint for Portland Bill</desc>
  <sym>ylw-pushpin</sym>
  <type>pushpin-ico</type>
</wpt>
```

The icon `lw-pushpin` appeared in the `<wpt>`, so the application needs to examine `<type>` and the corresponding icon style `pushpin-ico`.

```xml
<metadata>
  <extensions>
    <ico:style id="pushpin-ico">
      <ico:path href="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:path>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

In most GPZ files it is expected that icon styles will be the most simple case - i.e. single folder, single suffix.

However, icon styles may reference multiple paths / folders, multiple file types / suffixes and multiple icon sizes.

Applications will ultimately have the ability to choose the most appropriate icons for their display resolution / platform.

In the absence of an anchor point / hotspot the icons should simply be centered over the `<wpt>` / `<trkpt>` / `<rtept>`.



### Summary

This page and the examples have been created to demonstrate some basic icon features, without mandating a folder structure for GPZ files. The creator of the GPZ file is ultimately free to decide the most applicable folder structure for their own requirements.

Through the use of icon styles the GPZ creator can classify their icons in whatever way seems most appropriate. It may be a single folder called "icons", or it may use a number of different folders, perhaps providing different icon sizes for different screen resolutions.

Links to an illustrative schema (XSD), plus examples of usage (GPX + GPZ) are available on a separate page - click the [link](0/1/README.md) to access.
