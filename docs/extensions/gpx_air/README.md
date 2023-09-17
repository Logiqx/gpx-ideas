## GPX Extensions

### Air / Aviation - gpx_air

#### Overview

Air / aviation elements can be added to `<wpt>`, `<rtept>` and `<trkpt>`elements via GPX extensions.


| Name                         | Values       | Description                                                  |
| ---------------------------- | ------------ | ------------------------------------------------------------ |
| `<ias>`                      | >= 0         | Indicated airspeed (IAS) is measured by a pitot-static system in meters per second (m/s) |
| `<cas>`                      | >= 0         | Calibrated airspeed (CAS) is a more accurate version of IAS and sometimes used as the the indicated air speed. |
| `<eas>`                      | >= 0         | Equivalent airspeed (EAS) is closely related to Mach number and can therefore be measured via pressure differences |
| `<tas>`                      | >= 0         | True airspeed (TAS) is the speed of the aircraft relative to the airmass in which it is flying in meters per second (m/s)<br />Calculated using EAS and density (i.e. pressure altitude and OAT, ignoring humidity) or from mach + OAT |
| `<mach>`                     | >= 0         | Mach number<br />Calculated directly from the pitot-static system, or from TAS and OAT |
| `<ialt set="nnn" ref="xxx">` |              | Indicated altitude shows elevation / altitude / height of an aircraft in meters (m)<br />"set" is the pressure setting / sub-scale shown in the Kollsman window in hectopascals (hPa)<br />"ref" is the pressure reference and might be "qnh" (elevation / altitude), "qfe" (height) or "std" (pressure altitude) |
| `<palt>`                     |              | Pressure altitude is the height above the standard datum plane (SDP) in meters (m). Pressure altitude uses a pressure setting of 1013.25 hPa and is used to determine the flight level (FL) of the aircraft above MSL. |
| `<dalt>`                     |              | Density altitude is the altitude relative to standard atmospheric conditions at which the air density would be equal to the indicated air density in meters (m). Density altitude is affected by pressure, temperature and humidity. |
| `<agl>`                      |              | Height above ground level (HAGL) is the vertical distance with respect the underlying terrain in meters (m). AGL is determined by a radar / radio altimeter as opposed to a barometric altimeter. |
| `<slip>`                     | -180 to +180 | Slip / skid indicates whether the aircraft is in coordinated flight during a turn, measured in degrees (°)<br />positive = [slip]((https://en.wikipedia.org/wiki/Slip_(aerodynamic)), negative = [skid](https://en.wikipedia.org/wiki/Skid_(aerodynamic)) |



#### Example Usage

Air / Aviation

- [Microlight](../examples/air/microlight.md)
- [Light Aircraft](../examples/air/aircraft.md) 

