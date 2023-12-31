## Proposal for GPX

### Environment

Elements such as temperature and water depth have been suggested for the GPX standard:

| Name  | Description                                                  |
| ----- | ------------------------------------------------------------ |
| atemp | Air temperature in degrees centigrade (° C)                  |
| baro  | Barometric pressure in hectopascals (hPa)                    |
| depth | Depth of water in metres (m)                                 |
| hum   | Relative humidity as a percentage (%)                        |
| twd   | True wind direction (TWD), relative to true north in degrees (°) |
| tws   | True wind speed (TWS) in metres per second (m/s)             |
| wtemp | Water temperature in degrees centigrade (° C)                |

Omissions:

- There is no need for wind chill, because it is calculated from air temperature and wind speed
- There is no need for dew point or heat index, because they are calculated from air temperature and relative humidity
- There is no need for true wind angle (TWA), because it is calculated from true wind direction (TWD) and heading



#### References

- GPX developers list
  - [Aug 24](https://groups.io/g/gpx/message/47)
  - [Aug 5](https://groups.io/g/gpx/message/35)
- GPX proposal
  - Summary of common GPX [extensions](extensions.md)
- Garmin
  - TrackPointExtension v2 - [schema](https://www8.garmin.com/xmlschemas/TrackPointExtensionv2.xsd)
  - Sailing Terminology and Definitions - [article](https://support.garmin.com/en-GB/?faq=e5LwusViLZ95VTDwn2Alt7)
- ClueTrust
  - GPXData - [schema](http://www.cluetrust.com/Schemas/gpxdata10.xsd) download - search for `<xsd:complexType name="dataPointType">`
- NMEA revealed
  - [$WIMDA](https://gpsd.gitlab.io/gpsd/NMEA.html#_mda_meteorological_composite) - meteorological composite
- NMEA 2000
  - Garmin - [data types](https://www8.garmin.com/manuals/webhelp/GUID-1415AAD0-FE63-42A6-8F8D-DB713D616122/EN-US/GUID-FACE3DF9-D18C-43B2-A586-B14F670077E1.html)
- Sailmon
  - Max - [Live data](https://sailmon.com/max/#1675689499683-c73158df-1d1313e9-e463)
- Airmar 200WX-IPX7 - [data outputs](https://www.airmar.com/Product/200WX-IPX7)
  - [$WIMDA](http://www.nuovamarea.net/blog/wimda) - standard meteorological composite
  - [$WIMWD](http://www.nuovamarea.net/blog/wimwd) - wind direction and speed, with respect to north
  - $WIMWR - relative wind direction and speed
  - $WIMWT - theoretical wind direction and speed
  - [$WIMWV](http://www.nuovamarea.net/blog/wimwv) - wind speed and angle, in relation to the vessel's bow / centerline
