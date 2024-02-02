## GPX Extensions - Icons

### Background

This document has been written to illustrate the possibility of a generic approach for icons within GPZ files.

There are at least a couple of Android apps which already support GPZ files and custom icons via the `<sym>` element.

If `<sym>dining</sym>` is found within `<wpt>` / `<trkpt>` / `<rtept>` then `icons/dining.png` will be displayed at those locations.

This basic functionality has been demonstrated to work very nicely, but there are some additional capabilities which are desirable.



### Features / Capabilities

This extension has been drafted to illustrate some desirable features / capabilities:

- Support for multiple icon folders, allowing the creators of GPZ files to logically group their icons.
- Support for anchor points / hot spots, applied to groups of icons via a single definition in the GPX metadata.
- Support for multiple resolutions of icons, thus catering for different display resolutions and platforms.
- Support for multiple image formats, such as PNG and SVG.

These features can all be confined to the `<metadata>` section of the GPX file, allowing for simple  `<wpt>` / `<trkpt>` / `<rtept>` elements.



### Basic Examples

#### Example 1

This first example will simply demonstrate the use of a generic `dining` icon:

```xml
<wpt lat="50.514898" lon="-2.455531">
  <name>Lobster Pot</name>
  <sym>dining</sym>
  <type>icon</type>
</wpt>
```

The  `<metadata>` element below defines a single icon style, providing the information required to locate the `dining` icon within the GPZ file:

```xml
<metadata>
  <extensions>
    <ico:style id="icon">
      <ico:path href="icons/shapes" />
    </ico:style>
  </extensions>
</metadata>
```

The metadata can be summarised as follows:

- `<ico:style id="icon">` defines a single `icon` style, which can be used in `<type>` of `<wpt>` / `<trkpt>` / `<rtept>`.
- `<ico:path href="icons/shapes">` specifies the path / folder containing the icon file(s).

The information in this first example allows an app to easily display the dining icon, centered over a `<wpt>` / `<trkpt>` / `<rtept>`.



#### Example 2

This example shows how a collection of similar icons with identical anchor points / hotspots can be used by `<wpt>` / `<trkpt>` / `<rtept>`,

![pushpins](img/pushpins.png)

The waypoints themselves are no different to the first example, simply providing the icon name in `<sym>` and icon style in `<type>`:

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
  <sym>grn-pushpin</sym>
  <type>icon</type>
</wpt>
```

The `<metadata>` includes a single icon style providing not only the path / folder, but also the icon sizes and anchor points / hotspots:

```xml
<metadata>
  <extensions>
    <ico:style id="icon">
      <ico:path href="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:path>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

The metadata can be summarised as follows:

- A single icon style that can be referenced by the `<type>` element of `<wpt>` / `<trkpt>` / `<rtept>`.
- The sizes of icons are optional, but can be stated explicitly. Although optional, icon size is probably to be recommended.
- The anchor points / hotspots are specific to a group of icons. All images in the same path / folder share the same anchor point / hotspot.
- The image format (PNG) has been explicitly stated, but more than one image format may be specified.

This example demonstrates how a single icon style in the GPX metadata enables the simple usage within `<wpt>` / `<trkpt>` / `<rtept>`. The two waypoints simply include `<sym>ylw-pushpin</sym>` / `<sym>grn-pushpin</sym>`, and `<type>icon</type>`.



#### Example 3

The final example demonstrates how multiple categories of icon (e.g. pushpins and paddles) can be included within a single icon style.

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

The `<metadata>` section provides all of the information for the pushpins and paddles within the single `icon` style:

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

This single `icon` style is a simple demonstration of multiple categories of icon (e.g. pushpins and paddles) within a single style.

It should however be noted that the pushpin and paddle icons still have their own anchor points / hotspots.



### Application Development

#### Basic Concepts

Applications capable of reading GPZ files and displaying icons should not require any complicated logic to support the concept of icon styles.

The `<sym>` element in the following `<wpt>` indicates the icon name, and the `<type>` element indicates the icon style.

```xml
<wpt lat="50.513380" lon="-2.456620">
  <name>Portland Bill</name>
  <desc>Recommended viewpoint for Portland Bill</desc>
  <sym>ylw-pushpin</sym>
  <type>icon</type>
</wpt>
```

The snippet above shows the icon name `lw-pushpin` in `<sym>`, and the icon style `pushpin-ico` in `<type>`.

The application must therefore look at the corresponding icon style, which in this example is simply `icon`.

```xml
<metadata>
  <extensions>
    <ico:style id="icon">
      <ico:path href="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:path>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

In the majority of GPZ files it is expected that icon styles will be relatively simple.



#### Default Hotspots

In the absence of an anchor point / hotspot the icons should simply be centered over the `<wpt>` / `<trkpt>` / `<rtept>`.



#### Additional Concepts

Icon styles may reference multiple paths / folders, multiple image formats / suffixes, and / or multiple icon sizes.

Applications will ultimately have the ability to choose the most appropriate icons for their display resolution / platform.

It is even conceivable that icons can be acquired from external sources (and cached locally), if a URL is in the icon style.



### Further Discussion

#### Icon Styles

The examples above used a single icon style with an ID of `icon` but the creator of the GPX / GPZ may name the style however they wish.

Different creators of GPX / GPZ files may have different requirements, including the desire to use multiple icon styles within a single GPX file.



#### Icon Sizes

It has been shown that metadata allows for icon sizes to be specified for individual paths / folders.

One of the main benefits of explicit sizes is the provision for different icon sizes for various display resolutions and platforms.

Applications can decide for themselves how the paths / folders should be searched for the most suitable size(s) available.



#### Anchor Points / Hotspots

This extension only supports pixel units for icon sizes and the specification of anchor points / hotspots.

KML / KMZ supports pixels, fractions and combinations, but it is worth remembering that it will always be possible to determine a pixel offset.

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

However, it is recommended that the creators of GPX / GPZ files consider the inclusion of PNG (or GIF) icons in addition to the SVG icons, thus allowing applications unable to support SVG to use the PNG (or GIF) icons.



#### External Links

It is worth noting that an external source for the icon files can also be provided within the metadata.

If applications wish to support external icons then they should look to cache them locally.

One of the benefits of these external sources is in the instance where the GPX someone becomes separated from its icons.

```xml
<metadata>
  <extensions>
    <ico:style id="icon">
      <ico:path href="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:path>
      <ico:path href="http://maps.google.com/mapfiles/kml/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:path>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

Note that due to the definition of GPZ it is also possible to reference paths outside of the GPZ:

```xml
<metadata>
  <extensions>
    <ico:style id="icon">
      <ico:path href="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:path>
      <ico:path href="../shared.gpz/icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:path>
      <ico:path href="http://maps.google.com/mapfiles/kml/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:path>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

The above snipped shows what is possible using different paths, and could prove to be useful for a variety of application requirements.



### Summary

This page and the examples have been created to demonstrate some basic icon features, without mandating a specific folder structure within GPZ files. The creator of the GPX / GPZ file is ultimately free to decide the most applicable folder structure for their own requirements.

Through the use of icon styles the creator of the GPX / GPZ can classify their icons in whatever way they deem appropriate. It may be a single folder called "icons", or it may be a number of different folders, perhaps providing different icon sizes or image formats.

Links to an illustrative schema (XSD), plus examples of usage (GPX + GPZ) are available on a separate page - click the [link](0/1/README.md) to access.



#### References

- Icon collections and hotspot details taken from [Google Earth/Maps Icons](https://kml4earth.appspot.com/icons.html)
- KML reference - specifically [IconStyle](https://developers.google.com/kml/documentation/kmlreference#iconstyle)
