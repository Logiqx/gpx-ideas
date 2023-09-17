## GPX Extensions

### Air / Aviation - gpx_air

#### Random Notes - UNEDITED

- Abbreviations - [Wiki](https://en.wikipedia.org/wiki/List_of_aviation,_avionics,_aerospace_and_aeronautical_abbreviations) - [FAA](https://www.faa.gov/air_traffic/publications/atpubs/aip_html/part1_gen_section_2.2.html) - [Pegasus](https://www.flypgs.com/en/travel-glossary/abbreviations) - [UK gov](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/1059508/Glossary_of_Abbreviations.pdf)
  - FAA, Pegasus and UK gov do not list PA / DA, hence my use of palt and dalt

TBC - 2 x angle of attack (AOA) sensors

Notes

- True altitude should be recorded in `<ele>`
- OAT / SAT should be recorded in `<met:atemp>`
  - RAT / TAT can be recorded in `<met:atemp id="2">`

- Engine stuff should use the engine extension
  - e.g. Tachometer data should be recorded in `<eng:tach>`
    - Use `<eng:tach id="2">` for helicopters, etc

- pressure altitude would be recorded as `<alt set="1013.25">...</alt>`
- On large jet aircraft the IAS is by far the most important speed indicator. Most aircraft speed limitations are based on IAS, as IAS closely reflects dynamic pressure. TAS is usually displayed as well, but purely for advisory information and generally not in a prominent location.
- CAS can be calculated from TAS, OAT and pressure altitude - [link](https://en.wikipedia.org/wiki/Indicated_airspeed#IAS_and_navigation)
- Easiest way to calculate EAS is from the mach number.
- TAS is becoming less necessary now because of the advent of GPS which provides ground speed (SOG)

Temperature stuff can be deemed redundant perhaps?

| Name    | Values | Description                                                  |
| ------- | ------ | ------------------------------------------------------------ |
| `<tat>` |        | Total air temperature (TAT) / indicated air temperature (IAT) in degrees centigrade (° C)<br />n.b. This isn't quite the same as RAT which is dependent on the ram-rise-coefficient (aka recovery factor)<br />Is this redundant as it is used for maths within the air data computer (ADC)?<br />Small aircraft only have OAT |
| `<oat>` |        | Outside air temperature (OAT) / static air temperature (SAT) in degrees centigrade (° C)<br />n.b. This is essentially the same as `<atemp>` in gpx_met |
| `<isa>` |        | ISA temperature - TBC, redudant?                             |



Pressure altitude can be calculated using a formula - [link](https://aviation.stackexchange.com/questions/96885/what-is-the-real-formula-for-pressure-altitude)



Complex stats on Garmin include density altitude, wind direction - [link](https://www.euroga.org/forums/hangar-talk/4752-oat-versus-tat)

Apple app - [link](https://apps.apple.com/ie/app/altimeter-for-aviators/id1463100680)

Pitot-static system mentions multiple static ports - [wiki](https://en.wikipedia.org/wiki/Pitot-static_system#)

Variometer (vspeed) with picture of device for paragliders, hang gliders, ballooners - [wiki](https://en.wikipedia.org/wiki/Variometer)

Airspeed indicator - [wiki](https://en.wikipedia.org/wiki/Airspeed_indicator)

- mach number is relative to the speed of sound which is dependent on temperature / altitude - [wiki](https://en.wikipedia.org/wiki/Mach_number#)
- EAS and mach number are directly linked
- Mach number is a function of temperature and true airspeed. Aircraft flight instruments, however, operate using pressure differential to compute Mach number, not temperature.
- Most detailed explanation of IAS, CAS, EAS, TAS - [link](https://aviation.stackexchange.com/questions/64735/how-to-calculate-equivalent-airspeed-immediately-from-calibrated-airspeed)
  - another article about slow aircraft and link to TAS video - [link](https://aviation.stackexchange.com/questions/60542/temperature-sensor-are-needed-to-compute-true-airspeed-for-low-speed-aircrafts) + [video](https://www.youtube.com/watch?v=Qd1oCqzJZPM)

- Good explanation in aviation stackoverflow describes mach, etc  - [link](https://aviation.stackexchange.com/questions/1793/how-does-a-mach-meter-determine-the-speed-of-sound-at-a-given-altitude)
  - mach is only dependent on dynamic and static pressure


Hi Heather. Can I ask you a few basic aeronautical questions? I'm working on some proposed enhancements to the GPX file format, primarily for sports interested in speed but there is some basic sailing and aviation stuff included as well. I want to ensure that my understanding and use of terminology is correct with regards aviation. Firstly, there are obviously multiple conventions for airspeed (e.g. ias, cas, eas, tas). I am proposing that ias and tas be recorded and that cas / eas can be considered redundant because they can easily be calculated retrospectively when you also have the indicated altitude (plus the altimeter pressure setting) and outside air temperature. Does this make sense or have I overlooked something? Secondly, I am aware of 6 types of altitude (indicated, absolute, true, height, pressure, density). I'm proposing to include indicated altitude (plus the altimeter pressure setting) and the absolute altitude (i.e. radar altimeter reading) as I think the others can all be re-calculated when you also know the altitude and outside air temperature. Lastly, I've seen 6 names for temperature (iat / rat / tat, oat / sat / true) and I'm thinking of recording two values referred to as iat and oat. I'm assuming that as a pilot you are most interested in "indicated air temperature" and you sometimes tell passengers the "outside air temperature". Hopefully I've understood things correctly (please correct me if I am wrong, or if alternative names / conventions are more common) because you know, stuff on the internet can easily mislead. :D



Air Data Computer (ADC) - [link](https://aviation.stackexchange.com/questions/1793/how-does-a-mach-meter-determine-the-speed-of-sound-at-a-given-altitude) and [wiki](https://en.wikipedia.org/wiki/Air_data_computer)

- inputs = static pressure, pitot pressure, TAT





RAT and TAT are slightly different - [link](https://aviation.stackexchange.com/questions/1640/what-is-the-difference-between-oat-rat-tat-and-sat)

​	Another example with code and mentioning the difference of IAT and TAT - [link](https://www.hpmuseum.org/forum/thread-18073.html)




- Standard abbreviations used where applicable; ias / tas, iat / oat



There are multiple types of everything, I've chosen two of each as the others can be calculated:

- 4 common conventions for airspeed - **ias**, cas, eas, **tas**
- 6 types of altitude in aviation - **indicated**, **absolute**, true, height, pressure, density
- 6 types of temperature - **iat** / rat / tat, **oat** / sat / true



What is the source for the flight data shown on in-flight entertainment systems? - [link](https://aviation.stackexchange.com/questions/11411/what-is-the-source-for-the-flight-data-shown-on-in-flight-entertainment-systems)



Details

- 4 common conventions for airspeed - [link](https://en.wikipedia.org/wiki/Airspeed)
  - ias - Indicated airspeed is measured by a pitot-static system in meters per second (m/s)
  - cas - Calibrated airspeed is the indicated airspeed adjusted for pitot system position and installation error in meters per second (m/s)
  - eas - Equivalent airspeed is the calibrated airspeed adjusted for compressibility effects in meters per second (m/s)
  - tas - True airspeed is the equivalent airspeed adjusted for air density (requires temperature) in meters per second (m/s)
    - shown on glass panel displays
    - conversion tool exists - [link](https://aerotoolbox.com/airspeed-conversions/) and [another](http://www.luizmonteiro.com/altimetry.aspx) (not sure if it is accurate)
- 6 types of altitude in aviation - [link](https://en.wikipedia.org/wiki/Altitude#In_aviation)
  - pressure altitude - [wiki](https://en.wikipedia.org/wiki/Pressure_altitude)
    - Pressure altitude is used to indicate "flight level" which is the standard for altitude reporting, measured in meters (m)
    - Altitude indicated when the altimeter setting window (barometric scale) is adjusted to 29.92 "Hg. This is the altitude above the standard datum plane, which is a theoretical plane where air pressure (corrected to 15 °C) equals 29.92 "Hg
    - can be calculated - [link](https://www.flight-insight.com/post/pressure-altitude-vs-density-altitude)
    - see video from inside helicopter showing pressure altitude and density altitude - [link](https://youtu.be/regka_rS2Rw?t=568)
  - density altitude can also be calculated using static pressure (or pressure altitude) and outside air temperature - [link](https://en.wikipedia.org/wiki/Density_altitude#Approximation_formula_for_calculating_the_density_altitude_from_the_pressure_altitude)
  - true altitude can be calculated - [link](https://aviation.stackexchange.com/a/37790)
    - height can therefore be calculated using GIS data
  - altitude setting should be "at least 27.50 - 31.50 inches of Hg / 931.3 to 1066.7  mb" - [link](https://aviation.stackexchange.com/questions/58676/what-s-the-setting-range-altimeters-can-handle#:~:text=The%20specified%20scale%20range%20is,(931.3%20to%201066.7%20mb).)
    - Altimeter setting - [wiki](https://en.wikipedia.org/wiki/Altimeter_setting)
    - The setting may be inches or mb
  - [Height above ground level](https://en.wikipedia.org/wiki/Height_above_ground_level#Aviation) (AGL) can be determined using a [radar altimeter](https://en.wikipedia.org/wiki/Radar_altimeter#)

- 6 types of temperature


    - Indicated air temperature (IAT) / ram air temperature (RAT) / total air temperature (TAT)


    - Outside air temperature (OAT) / static air temperature (SAT) / true air temperature


Kinda extra...

  - TAS can potentially be calculated after the event but it is included for a similar reason as apparent wind vs true wind in yachts
  - OAT can potentially be calculated after the event but it is included for a similar reason as apparent wind vs true wind in yachts
    - See video from inside helicopter showing OAT in F and C - [link](https://youtu.be/regka_rS2Rw?t=557)
    - OAT is also shown on the in-flight entertainment systems


See [article](https://www.mcico.com/resources/flight-instruments/six-pack-aircraft-instruments-explained) about the 6 basic aircraft instruments. Many of the metrics are in other extension schemas

- Standard position / velocity / time (PVT) - elevation (altitude above MSL), vertical speed (rate of climb / descent)
- Inertial Navigation System (INS) - pitch + bank (roll) are referred to as "attitude"

TODO - links to the two good videos on the six pack

Magnetic north vs true north

- Mag2True - [Time for a change of direction](https://www.aerosociety.com/news/time-for-a-change-of-direction) - 4 Aug 2023
  - [working group](https://www.navnin.nl/new/mag2true/) information page - possibly in less than 10 years


Notes:

- The altimeter, airspeed indicator, and vertical speed indicator (variometer) all rely on the Pitot-static tube. 
- The heading indicator, attitude indicator, and turn coordinator rely on gyroscopes.
- Rate of turn (ROT):
  - ROT represents the rate of change of heading, included in the "[six pack](https://www.mcico.com/resources/flight-instruments/six-pack-aircraft-instruments-explained)" of aircraft instruments - [link](https://en.wikipedia.org/wiki/Standard_rate_turn)
  - ROT should <u>not</u> be derived from COG information - [link](https://www.navcen.uscg.gov/ais-class-a-reports)
- Slip and skid
  - Stuff about sideslip - [link](https://aviation.stackexchange.com/questions/77125/how-does-sideslip-indicator-react-during-crosswind)
  - Gliders tend to have a [yaw string](https://en.wikipedia.org/wiki/Yaw_string) instead of an elaborate slip / skid indicator and they do not have an attitude indicator ("artificial horizon").
    - See [link](http://airplanegroundschools.com/Glider-Airplanes/glider-flight-instruments.html) used for insights into sensors on a glider and [photo](https://aviation.stackexchange.com/questions/63959/is-it-normal-for-gliders-not-to-have-attitude-indicators)
- Excluded
  - Glide ratio (slope) can be determined from ground "speed" (SOG) and "vspeed" (rate of descent) - [link](https://www.nasa.gov/pdf/582952main_Glide-Slope%20Ratio%20Explanation.pdf)
    - glide ratio = horizontal distance /  change in altitude
    - glide ratio (instantaneous) = horizontal speed (SOG) / vertical speed
    - n.b. glide slope may be used in combination with VNAV (vertical navigation)
  - Drift angle - "drift"
    - "Drift angle is just the difference between your heading and your ground track" - [link](https://aviation.stackexchange.com/a/95984) 
    - n.b. Cars also have concepts of drift (deliberate oversteer) and skid (2 types which are equivalent to slip and skid) - [link](https://thecontentauthority.com/blog/drift-vs-skid)
- Useful links
  - drone [log](PressDiff, IndicatedAirSpeed, Temperature)
    - TBC - consider ENU / NED extension?

