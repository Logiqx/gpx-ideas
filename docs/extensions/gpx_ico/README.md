## GPX Extensions - Icons

### Background

This document has been written to illustrate the possibility of a generic approach for icon usage within GPX / GPZ files.

There are at least a couple of Android apps which already support GPZ files and custom icons via the `<sym>` element.

If `<sym>dining</sym>` is found within `<wpt>` / `<trkpt>` / `<rtept>` then `icons/dining.png` will be displayed at those locations.

This basic functionality has been demonstrated to work quite nicely, but there are some additional capabilities which are desirable.



### Features / Capabilities

This extension has been drafted to illustrate some desirable icon features / capabilities:

- Support for multiple icon folders, allowing the creators of GPX / GPZ files to logically group their icons.
- Support for anchor points / hot spots, applied to groups of icons via a single definition in the GPX metadata.
- Support for multiple resolutions of icons, thus catering for different display resolutions and devices.
- Support for multiple image formats, such as PNG and SVG.

These features can all be confined to the `<metadata>` section of the GPX file, allowing for simple  `<wpt>` / `<trkpt>` / `<rtept>` elements.



### Basic Examples

#### Example 1

This first example will simply demonstrate the use of a generic `dining` icon:

```xml
<wpt lat="50.514898" lon="-2.455531">
  <name>Lobster Pot</name>
  <extensions>
    <ico:icon name="dining" />
  </extensions>
</wpt>
```

The  `<metadata>` element includes a single icon style, providing the information required to locate the `dining` icon:

```xml
<metadata>
  <extensions>
    <ico:style id="default">
      <ico:folder url="icons/shapes" />
    </ico:style>
  </extensions>
</metadata>
```

The metadata can be summarised as follows:

- `<ico:style>` defines the default style for `<ico:icon>` elements.
- `<ico:folder>` specifies the folder containing the icon file(s).

The information in this first example allows an app to easily display the dining icon, centered over a `<wpt>` / `<trkpt>` / `<rtept>`.



#### Example 2

This example shows how a collection of similar icons with identical anchor points / hotspots can be used by `<wpt>` / `<trkpt>` / `<rtept>`.

![pushpins](img/pushpins.png)

The waypoints themselves are no different to the first example, simply providing the icon name in `<ico:icon>`:

```xml
<wpt lat="50.513380" lon="-2.456620">
  <name>Portland Bill</name>
  <extensions>
    <ico:icon name="ylw-pushpin" />
  </extensions>
</wpt>
  
<wpt lat="50.222776" lon="-3.642783">
  <name>Start Point</name>
  <extensions>
    <ico:icon name="grn-pushpin" />
  </extensions>
</wpt>
```

The `<metadata>` includes a single icon style providing not only the folder, but also the icon sizes and anchor points / hotspots:

```xml
<metadata>
  <extensions>
    <ico:style id="default">
      <ico:folder url="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:folder>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

The metadata can be summarised as follows:

- The default icon style for individual `<ico:icon>` elements.
- The size of the icons is optional, but can be stated explicitly. Although optional, icon size is probably to be recommended.
- The anchor points / hotspots are specific to a group of icons. All images in the group essentially share the same anchor point.
- The image format (PNG) has been explicitly stated, but more than one image format may be specified.

This example demonstrates how a default icon style in the GPX metadata allows for simple icons within `<wpt>` / `<trkpt>` / `<rtept>`.

The two example waypoints only need to include `<ico:icon>ylw-pushpin</ico:icon>` or `<ico:icon>grn-pushpin</ico:icon>`.



#### Example 3

The final example demonstrates how multiple categories of icon (e.g. pushpins and paddles) can be defined within the default icon style.

```xml
<wpt lat="50.513380" lon="-2.456620">
  <name>Portland Bill</name>
  <extensions>
    <ico:icon name="ylw-pushpin" />
  </extensions>
</wpt>
  
<wpt lat="50.222776" lon="-3.642783">
  <name>Start Point</name>
  <extensions>
    <ico:icon name="ylw-blank" />
  </extensions>
</wpt>
```

The `<metadata>` section includes all of the information for the pushpins and paddles within the default icon style:

```xml
<metadata>
  <extensions>
    <ico:style id="default">
      <ico:folder url="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:folder>
      <ico:folder url="icons/paddle">
        <ico:size x="64" y="64" />
        <ico:hotspot x="32" y="1" />
      </ico:folder>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

This default style demonstrates how it is possible to include multiple categories of icon (e.g. pushpins and paddles) within a single style.

It should however be noted that the pushpin and paddle icons still have their own unique anchor points / hotspots.



### Application Development

#### Basic Concepts

Applications capable of reading GPX / GPZ files and capable of displaying icons do not need to implement any complicated logic.

The `<ico:icon>` element in a `<wpt>` / `<trkpt>` / `<rtept>` indicates the icon name, and the `style` attribute indicates the icon style.

Note that the style attribute has a default value of `default`, allowing the style attribute to be omitted for most icons.

```xml
<wpt lat="50.513380" lon="-2.456620">
  <name>Portland Bill</name>
  <extensions>
    <ico:icon name="ylw-pushpin" style="demo" />
  </extensions>
</wpt>
```

The snippet above references an icon called `lw-pushpin` and an icon style of `demo`, rather than the `default` style.

The application must therefore use the corresponding icon style, which in this example is simply called `demo`.

```xml
<metadata>
  <extensions>
    <ico:style id="demo">
      <ico:folder url="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:folder>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

The majority of GPX / GPZ files using icons are expected to use a single `default` icon style.



#### Default Hotspots

In the absence of an anchor point / hotspot the icons should simply be centered over the `<wpt>` / `<trkpt>` / `<rtept>`.



#### Additional Concepts

Icon styles may reference multiple folders, multiple image formats / suffixes, and / or multiple icon sizes.

Applications will ultimately have the ability to choose the most appropriate icons for their display resolution / device.

It is also conceivable that icons may be acquired from external sources (e.g. URL in `<ico:folder>`) and cached locally, described later.



### Further Discussion

#### Icon Styles

The examples above used a single icon style called `icon`, but the creator of the GPX / GPZ may name the icon style however they desire.

Different creators of GPX / GPZ files may have different requirements, including the desire for multiple icon styles within a single GPX file.



#### Icon Sizes

It has been shown that metadata allows for icon sizes to be specified for individual folders.

One of the main benefits of explicit sizes is the provision for different icon sizes for various display resolutions and devices.

Applications can decide for themselves how the folders should be searched for the most suitable icons available.



#### Anchor Points / Hotspots

This extension only supports pixel units for icon sizes and the specification of anchor points / hotspots.

KML supports pixels or percentages (and combinations) for hotspots, but it should always be possible to determine pixel units.

The decision to only use pixel units for anchor points / hotspots keeps things simple and avoids unnecessary complexity in the schema.

If you know the percentage (e.g. 50%) then just do the math to determine the pixel equivalent.



#### Scalable Vector Graphics (SVG)

It is conceivable that some creators of GPX / GPZ files may wish to use SVG icons.

When using SVG icons and requiring anchor points / hotspots, simply specify a "virtual" size, plus the equivalent hotspot.

```xml
<ico:folder url="icons/svg">
  <ico:size x="256" y="256" />
  <ico:hotspot x="128" y="0" />
</ico:folder>
<ico:suffix>svg</ico:suffix>
```

GPX / GPZ files that use SVG icons may also wish to include PNG (or GIF) icons, thus providing an alternative for applications unable to support SVG.



#### External Links

It is worth noting that external links for the icon files can also be provided within the metadata.

If applications wish to support external links (i.e. downloaded from a URL) then they should consider caching the files locally.

One of the benefits of external links would be when a GPX somehow becomes separated from its icons, outside of a GPZ file.

```xml
<metadata>
  <extensions>
    <ico:style id="default">
      <ico:folder url="icons/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:folder>
      <ico:folder url="http://maps.google.com/mapfiles/kml/pushpin">
        <ico:size x="64" y="64" />
        <ico:hotspot x="20" y="2" />
      </ico:folder>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

The above snipped shows what is possible using different folders, which could prove to be useful for a variety of application requirements.



### Summary

This page and the examples have been created to demonstrate some basic icon features, without mandating a specific folder structure. The creator of the GPX / GPZ file is ultimately free to decide the most applicable folder structure for their own requirements.

Through the use of icon styles the creator of the GPX / GPZ can classify their icons in whatever way they deem appropriate. It may be a single folder called "icons", or it may be a number of different folders, perhaps providing different icon sizes or image formats.

Applications are not required to support all of the features such as anchor points / hotspots, SVG support or external links. These concepts have only been documented to illustrate what is possible, should an application wish to make use of such advanced features.

Links to a draft schema, plus GPX 1.1 compliant examples (GPX + GPZ) are available on a separate page - click the [link](0/2/README.md) to access.

The latest draft schema is [gpx_ico.xsd](0/2/gpx_ico.xsd) and it enables full verification of all the examples using [freeformatter.com](https://www.freeformatter.com/xml-validator-xsd.html).



#### References

- Icon collections and hotspot details taken from [Google Earth/Maps Icons](https://kml4earth.appspot.com/icons.html)
- KML reference - specifically [IconStyle](https://developers.google.com/kml/documentation/kmlreference#iconstyle)
