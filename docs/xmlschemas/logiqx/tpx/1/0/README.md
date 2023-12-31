## TrackPointExtras

### Background

GPS / GNSS chipsets from a number of manufacturers provide position and speed accuracy estimates; SiRF, u-blox, Broadcom, Qualcomm, etc.

This data is typically available via binary protocols (e.g. SiRF and UBX) or proprietary NMEA sentences (e.g. `$PGLOR,...,LSQ`).

Estimated location and speed accuracy information is also available via the Android and Apple location [APIs](../../../../apis/location.md), summarised in the linked document.

However, GPX 1.1 provides no standard mechanism to store the accuracy estimates (or Doppler-derived course and speed), hence these GPX extensions.



### Extensions

This [TPX 1.0](tpx.xsd) schema defines universal extensions to be used with the [GPX 1.1](https://www.topografix.com/GPX/1/1/gpx.xsd) schema.

The "extras" element defined by this schema is intended to be used as a child element of the "extensions" elements in the trkpt element.

For example:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <extensions>
    <tpx:extras>
      <tpx:course>157.19</tpx:course>
      <tpx:speed>0.543</tpx:speed>
      <tpx:hacc>2.0</tpx:hacc>
      <tpx:vacc>4.0</tpx:vacc>
      <tpx:cacc>5.0</tpx:cacc>
      <tpx:sacc>0.5</tpx:sacc>
    </tpx:extras>
  </extensions>
</trkpt>
```

A more elaborate `<src>` element is also provided to give some idea of reliability and accuracy of the data:

```xml
<trk>
  <trkseg>...</trkseg>
  <extensions>
    <tpx:src>
      Apple Watch Series 8
      <tpx:device>
        <tpx:manufacturer>Apple</tpx:manufacturer>
        <tpx:product>Watch Series 8</tpx:product>
        <tpx:serial>123456789</tpx:serial>
        <tpx:name>Nathan's Apple Watch</tpx:name>
        <tpx:version>8.5.1</tpx:version>
      </tpx:device>
      <tpx:software>
        <tpx:developer>Hoolan Ltd</tpx:developer>
        <tpx:application>Hoolan</tpx:application>
        <tpx:link>
          <tpx:href>https://www.hoolan.app/</tpx:href>
        </tpx:link>
        <tpx:version>1.6.0</tpx:version>
      </tpx:software>
    </tpx:src>
  </extensions>
</trk>
```



### Decisions + Rationale

All of the element names have been intentionally kept as short as possible to avoid too much bloat of the GPX:

- The `<extras>` element is a complex type which ensures consistent ordering of the sub-elements.
- The elements `<course>` and `<speed>`  have been carried forward from GPX 1.0
  - They also match the elements in version 2 of Garmin's [TrackpointExtension](https://www8.garmin.com/xmlschemas/TrackPointExtensionv2.xsd) schema.

- Estimated "accuracy" elements have been given short names - e.g. `<hacc>` is the "horizontal accuracy" estimate.

These short names are closely related to the names used by u-blox (e.g. "hAcc" for horizontal accuracy estimate) and Broadcom ("HErr" for horizontal error estimate) in their GNSS chipset documentation.

The accuracy estimates have been named concisely (e.g. `<hacc>` and `<vacc>`) and use entirely lower case names for consistency with the GPX schema, much like the elements `<hdop>`, `<vdop>`, and `<pdop>` in GPX 1.0 and 1.1.

Note: The term "accuracy" has been chosen over "error" because it is used by the [Android](https://developer.android.com/reference/android/location/Location) and [Apple](https://developer.apple.com/documentation/corelocation/cllocation) APIs, plus notable GPS / GNSS chipset manufacturers such as u-blox. Although some chipset manufacturers use the word "error" those items essentially represent the same thing. It represents RMS, 1-sigma or 68% confidence.



### Trackpoint Extensions

#### COG, SOG and ROC

The following elements can all be added to `<wpt>`, `<rtept>` and `<trkpt>` elements, under `<extensions>`.

They are all optional, although the values of `<course>` and `<speed>` as provided by the GPS / GNSS chipset are highly recommended in GPX 1.1.1 files.

| Name       | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| `<course>` | Course over ground (COG) in degrees is the actual direction of travel relative to true north.<br/>COG is an independent measurement from position, so it is possible (and not an error) for the difference between two successive positions to be inconsistent with the COG values. |
| `<speed>`  | Speed over ground (SOG) in m/s is the horizontal speed calculated by the GPS / GNSS chipset.<br/>SOG is an independent measurement from position, so it is possible (and not an error) for the difference between two successive positions to be inconsistent with the SOG values. |
| `<roc>`    | Rate of climb (ROC) in m/s is the vertical speed calculated by the GPS / GNSS chipset.<br/>ROC is an independent measurement from position, so it is possible (and not an error) for the difference between two successive positions to be inconsistent with the ROC values. |


#### Accuracy Estimates

The following accuracy elements can all be added to `<wpt>`, `<rtept>` and `<trkpt>` elements, under `<extensions>`.

These are available from a variety of NMEA sentences, binary messages and location services provided by Apple and Android.

| Name     | Description                                                  |
| -------- | ------------------------------------------------------------ |
| `<hacc>` | Horizontal accuracy / error estimate in meters, such that the difference from the true position and the reported position is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<vacc>` | Vertical accuracy / error estimate in meters, such that the difference from the true position and the reported position is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<cacc>` | Course over ground (COG) accuracy / error estimate in degrees, such that the difference from the true COG and the reported COG is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<sacc>` | Speed over ground (SOG) accuracy / error estimate in m/s, such that the difference from the true SOG and the reported SOG is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |
| `<racc>` | Rate of climb (ROC) accuracy / error estimate in m/s, such that the difference from the true ROC and the reported ROC is less than the accuracy / error estimate 68% of the time. 68% corresponds to 1-sigma of a normal distribution, but this does not imply that errors are independent or normally distributed. |


#### Source Elements

GPX 1.0 and 1.1 both support `<src>` elements in `<wpt>`, `<rte>`, `<rtept>`, `<trk>`, and `<trkpt>` elements.

These are simply `xsd:string` types and may contain values such as "Apple Watch Series 8".

The GPX 1.1.1 proposal introduces a more sophisticated `<src>` element containing `<device>` and `<software>`.

**`<device>`** contains the following optional elements:

| Name             | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| `<manufacturer>` | Manufacturer of the GPS device / wearable.<br/>e.g. "Apple"  |
| `<product>`      | Product name of the GPS device / wearable, preferably without mentioning the product manufacturer.<br/>e.g. "Watch Series 8" |
| `<serial>`       | Serial number of the GPS device / wearable.<br/>e.g. "123456789" |
| `<name>`         | Name of the GPS device / wearable, typically chosen by the owner.<br/>e.g. "Nathan's Apple Watch". |
| `<version>`      | Firmware / software / OS version of the GPS device / wearable.<br/>e.g. "8.5.1" |

**`<software>`** contains the following optional elements:

| Name            | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| `<developer>`   | Developer of the software / application used to capture + export the GPS data.<br/>This may match the "creator" attribute but unlike "creator", it should persist after (possible) post-processing.<br/>e.g. "Hoolan Ltd" |
| `<application>` | Name of the software / application used to capture + export the GPS data.<br/>This may match the "creator" attribute but unlike "creator", it should persist after (possible) post-processing.<br/>e.g. "Hoolan" |
| `<link>`        | Link to the software / application used to capture + export the GPS data:<br/>e.g. "`<href>https://www.hoolan.app/</href>`" |
| `<version>`     | Version of the software / application used to capture + export the GPS data.<br/>e.g. "1.6.0" |

Note: Since the `<src>` element is a "mixed" type you can still include a simple string to describe the device, such as "Apple Watch Series 8".



### Usage

GPX 1.1 compliant files should begin with something like the following:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<gpx creator="GPS Wizard"
     version="1.1"
     xmlns="http://www.topografix.com/GPX/1/1"
     xmlns:tpx="http://logiqx.github.io/gpx-ideas/xmlschemas/logiqx/tpx/1/0"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:schemaLocation="http://www.topografix.com/GPX/1/1
                         https://www.topografix.com/GPX/1/1/gpx.xsd
                         http://logiqx.github.io/gpx-ideas/xmlschemas/logiqx/tpx/1/0
                         https://logiqx.github.io/gpx-ideas/xmlschemas/logiqx/tpx/1/0/tpx.xsd">
```

It is recommended that source information be provided within the `<trk>` element:

```xml
<trk>
  <trkseg>...</trkseg>
  <extensions>
    <tpx:src>
      Apple Watch Series 8
      <tpx:device>
        <tpx:manufacturer>Apple</tpx:manufacturer>
        <tpx:product>Watch Series 8</tpx:product>
        <tpx:serial>123456789</tpx:serial>
        <tpx:name>Nathan's Apple Watch</tpx:name>
        <tpx:version>8.5.1</tpx:version>
      </tpx:device>
      <tpx:software>
        <tpx:developer>Hoolan Ltd</tpx:developer>
        <tpx:application>Hoolan</tpx:application>
        <tpx:link>
          <tpx:href>https://www.hoolan.app/</tpx:href>
        </tpx:link>
        <tpx:version>1.6.0</tpx:version>
      </tpx:software>
    </tpx:src>
  </extensions>
</trk>
```

Track points should always include course and speed when available. Ideally they should also include accuracy estimates when available:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <sat>6</sat>
  <hdop>1.4</hdop>
  <extensions>
    <tpx:extras>
      <tpx:course>157.19</tpx:course>
      <tpx:speed>0.5429</tpx:speed>
      <tpx:hacc>2.0</tpx:hacc>
      <tpx:vacc>4.0</tpx:vacc>
      <tpx:cacc>5.0</tpx:cacc>
      <tpx:sacc>0.5</tpx:sacc>
    </tpx:extras>
  </extensions>
</trkpt>
```



### Validation

Software developers should validate their GPX files during the development / testing process.

Validation methods are described in a technical [overview](https://logiqx.github.io/gps-wizard/gpx/) of the GPX format.
