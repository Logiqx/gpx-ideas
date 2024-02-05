## GPX Extensions - Icons

### Background

This document has been written to illustrate the possibility of a generic approach for icon usage within GPX / GPZ files.

There are at least a couple of Android apps which already support GPZ files and custom icons via the `<sym>` element.

This basic functionality has been demonstrated to work quite nicely, but there are some additional capabilities which are desirable.



### Features / Capabilities

This extension has been drafted to illustrate some desirable icon features / capabilities:

- Support for multiple icon folders, allowing the creators of GPX / GPZ files to logically group their icons.
- Support for multiple resolutions of icons, thus catering for different display resolutions and devices.
- Support for multiple image formats and transparency / alpha channels, such as PNG and SVG.
- Support for anchor points / hot spots, applied to related icons via a single definition.

These features should all be confined to the `<metadata>` section of the GPX file, allowing for simple  `<wpt>` / `<trkpt>` / `<rtept>` elements.



### Simple Examples

This document kicks off with some simple examples, rather than explaining everything in detail upfront. Many creators of GPX / GPZ files that wish to include icons are not expected to require functionality beyond the first example.

The remainder of the document will provide additional technical details relating to the icon functionality.



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

The  `<metadata>` element defines the default icon style, providing the information required to locate the `dining` icon:

```xml
<metadata>
  <extensions>
    <ico:style id="default">
      <ico:folder url="icons/shapes" />
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

The metadata can be summarised as follows:

- `<ico:style id="default">` defines the default style for `<ico:icon>` elements.
- `<ico:folder url="icons/shapes">` specifies the folder containing the icon file(s).
- `<ico:suffix>` specifies the image format of the icon file(s).

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

The `<metadata>` includes a single icon style providing not only the folder, but also the size of the icons an anchor point / hotspot:

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
- The size of the icons is optional, but can be stated explicitly. Although optional, inclusion of icon size is recommended.
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

The `<ico:icon>` element in a `<wpt>` / `<trkpt>` / `<rtept>` indicates the icon name, and the `style` attribute provides necessary details.

Note that the style attribute has a default value of `default`, allowing the style attribute to be omitted for most `<icon>` elements.

```xml
<wpt lat="50.513380" lon="-2.456620">
  <name>Portland Bill</name>
  <extensions>
    <ico:icon name="ylw-pushpin" style="demo" />
  </extensions>
</wpt>
```

The snippet above references an icon called `lw-pushpin` and an icon style of `demo`, rather than the `default` style.

The application must refer to the corresponding icon style, which in this example is simply called `demo`.

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

n.b. The majority of GPX / GPZ files using icons are expected to use a single `default` icon style.



#### Folder URLs

URLs may be relative paths to icons that are held locally (e.g. local folder or inside GPZ), or a `http` / `https` URL.

In the case of relative paths they may (or may not) start with `./` and they may (or may not) end with `/`. Applications should ensure that they can handle the presence or absence of a leading `./` and trailing `/`.

Remote files should be cached locally by the application, thus avoiding repeat downloads and providing an offline capability.



#### Default Suffixes

The creator of a GPX / GPZ file is advised to include one or more `<suffix>` elements in the icon style. If there are no `<suffix>` elements within the icon style the application should search for icon files with a suffix of `png`, `gif`, or `svg`.



#### Default Hotspots

In the absence of an anchor point / hotspot the icons should simply be centered over the `<wpt>` / `<trkpt>` / `<rtept>`.



#### Additional Concepts

Icon styles may have multiple folders, multiple image formats / suffixes, and / or multiple icon sizes.

Applications will ultimately have the ability to choose the most appropriate icons for their display resolution / device.

It is also possible that icons may be acquired from external sources (e.g. URL in `<ico:folder>`) but then cached locally.



### Further Discussion

#### Icon Styles

The examples only had a `default` icon style, but the creator of the GPX / GPZ may include several different icon styles.

Different creators of GPX / GPZ files may have different requirements, including the desire for multiple icon styles within a single GPX file.

It is highly recommended that icon styles in a GPX / GPZ file list the appropriate file suffixes, to save checking URLs for an unknown suffix.



#### Icon Sizes

It has been shown that icon styles allow the icon sizes to be specified for individual folders.

One of the main benefits of explicit sizes is the provision of different icon sizes for various display resolutions and devices.

```xml
<metadata>
  <extensions>
    <ico:style id="default">
      <ico:folder url="icons/flags/64x64">
        <ico:size x="64" y="64" />
      </ico:folder>
      <ico:folder url="icons/flags/32x32">
        <ico:size x="32" y="32" />
      </ico:folder>
      <ico:folder url="icons/flags/16x16">
        <ico:size x="16" y="16" />
      </ico:folder>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

Notes:

- 16 x 16, 32 x 32, 64 x 64 are the most common sizes for multiple platforms.
- 24 x 24 and 48 x 48 are also common fixes for multiple platforms.
- 18 x 18, 20 x 20, 36 x 36 and 40 x 40 are less common but often found.

Applications can decide for themselves how the folders should be searched, according to the most suitable icon sizes for the display.



#### Image Formats

The icon extension supports PNG, GIF and SVG files. 32-bit PNG files (including an alpha channel) or SVG are recommended.

Legacy icons in BMP format should be converted to PNG, ensuring that relevant transparency information is present in the PNG. Use of magenta / cyan / white backgrounds to represent transparency is not going to be supported, hence the conversion from BMP.

TIFF will not be supported by GPX / GPZ, although the TIFF format does allow for an alpha channel. Any icons in TIFF format should also be converted to PNG format, ensuring the alpha channel is preserved.

The JPEG format is not suitable for icons. Miniature versions of JPEG photos are [thumbnails](https://en.wikipedia.org/wiki/Thumbnail) and should not be considered icons. 



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



#### Transparency

Icons are typically square and often opaque but individual pixels may sometimes be transparent, or semi-transparent.

The use of an alpha channel results in excellent results when the icon is displayed over a variety of different backgrounds / colors. It is therefore recommended that [raster](https://en.wikipedia.org/wiki/Raster_graphics) icons with transparent / semi-transparent pixels are 32-bit PNG files or SVG files, thus including an [alpha](https://en.wikipedia.org/wiki/Alpha_compositing) channel.

PNG files with indexed colors can also have an alpha value for each palette index which may suffice, as per the [specification](https://www.w3.org/TR/2003/REC-PNG-20031110/#6AlphaRepresentation). GIF files can only mark a single palette index as transparent which is not the same as an alpha channel, but does facilitate transparency as per the [specification](https://www.w3.org/Graphics/GIF/spec-gif89a.txt)

Image files that use solid colors such as magenta, cyan, or white to indicate transparency are not to be supported. Such images should be converted to PNG or GIF files that include an alpha channel, or transparency information / alpha value for the specific palette index (or RGB value).



#### Anchor Points / Hotspots

Anchor points / hotspots are most useful for icons that are transparent or semi-transparent. They will typically be used to ensure that a specific part of the image is aligned with a specific latitude and longitude, regardless of the level of zoom.

This extension supports pixel units for icon sizes and the specification of anchor points / hotspots. KML also supports percentages for hotspots, but it should always be possible to determine pixel units.

The decision to use pixel units for anchor points / hotspots keeps things simple and avoids unnecessary complexity within the schema. If a percentage is desired (e.g. 50%) then just do the math to determine the pixel equivalent.



#### Folder URLs

URLs may be relative paths to icons that are held locally (e.g. local folder or inside GPZ), or a `http` / `https` URL.

In the case of relative paths they may (or may not) start with `./` and they may (or may not) end with `/`. The creator of the GPX / GPZ file may use a leading `./` and trailing `/` if desired but it is not mandated.

There may be occasions when it is advantageous to provide remote links to icon folders, additional to the relative paths within the GPZ.



#### External Links

External links have several possible uses but here are two examples:

- Icons sets can be hosted online so that individual icons can downloaded by applications as required and cached locally.
- Icons can be re-acquired if the GPX somehow becomes detached from its icons, such as a GPX which was originally in a GPZ file.

Note: If applications wish to support external links they should seriously consider using a local cache of the icon files.

```xml
<metadata>
  <extensions>
    <ico:style id="default">
      <ico:folder url="icons/shapes">
        <ico:size x="64" y="64" />
      </ico:folder>
      <ico:folder url="http://maps.google.com/mapfiles/kml/shapes">
        <ico:size x="64" y="64" />
      </ico:folder>
      <ico:suffix>png</ico:suffix>
    </ico:style>
  </extensions>
</metadata>
```

The above snipped shows what is possible using multiple folders, which could prove to be useful for a variety of application requirements.



### Summary

This page and the examples have been created to demonstrate some basic icon features, without mandating a specific folder structure. The creator of the GPX / GPZ file is ultimately free to decide the most applicable folder structure for their own requirements.

Through the use of icon styles the creator of the GPX / GPZ can classify their icons in whatever way they deem appropriate. It may be a single folder called "icons", or it may be a number of different folders, perhaps providing different icon sizes or image formats.

Applications are not required to support all of the features such as anchor points / hotspots, SVG support or external links. These concepts have been documented to illustrate what is possible, should an application wish to make use of such features.

Links to a draft schema, plus GPX 1.1 compliant examples (GPX + GPZ) are available on a separate page - click the [link](0/2/README.md) to access.

The latest draft schema is [gpx_ico.xsd](0/2/gpx_ico.xsd) and it enables full verification of all the examples using [freeformatter.com](https://www.freeformatter.com/xml-validator-xsd.html).



#### References

- Icon collections and hotspot details taken from [Google Earth/Maps Icons](https://kml4earth.appspot.com/icons.html)
- KML reference - specifically [IconStyle](https://developers.google.com/kml/documentation/kmlreference#iconstyle)
