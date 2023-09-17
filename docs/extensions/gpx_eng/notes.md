## GPX Extensions

### Engine - gpx_eng

#### Random Notes - UNEDITED

Original idea, prior to generic elements

| Name        | Values | Description                                                  |
| ----------- | ------ | ------------------------------------------------------------ |
| tach        |        | Tachometer for engine / rotor / propeller for revolutions per minute (RPM)<br />See [RPM](https://gpsd.gitlab.io/gpsd/NMEA.html#_rpm_revolutions) in NMEA 0183 - only record when status "A" |
| trim        |        | Propeller pitch as a percentage of the maximum (%) - boats<br />See [RPM](https://gpsd.gitlab.io/gpsd/NMEA.html#_rpm_revolutions) in NMEA 0183 - only record when status "A" |
| torq        |        | Engine torque in Newton metres (Nm)<br />e.g. helicopters    |
| temp id="n" |        |                                                              |
| chttemp     |        | Cylinder head temperature (CHT) in degrees centigrade (° C)<br />planes and boats |
| egttemp     |        | Exhaust gas temperature (EGT) in degrees centigrade (° C)<br />e.g. planes |
| carbtemp    |        | Carburetor temperature in degrees centigrade (° C)<br />e.g. planes |
| bstpres     |        | Boost pressure (turbo or supercharger) in kilopascals (kPa)<br />e.g. boats |
| vacpres     |        | Vacuum pressure in kilopascals (kPa)<br />e.g. boats, planes and helicopters |
| oiltemp     |        | Oil temperature in degrees centigrade (° C)<br />e.g. boats, planes and helicopters |
| oilpres     |        | Oil pressure in kilopascals (kPa)<br />e.g. engine or transmission |
| cooltemp    |        | Coolant / water temperature in degrees centigrade (° C)      |
| coolpres    |        | Coolant / water pressure in kilopascals (kPa)                |
| fuelqty     |        | Fuel quantity in litres (L)                                  |
| fuelpres    |        | Fuel pressure in kilopascals (kPa)                           |
| battvolt    |        | Battery level in volts (V)                                   |
| battamp     |        | Battery current - negative (charging) or positive (discharging) in amps (A) |





All elements have have maxOccurs="unbounded", plus an two optional attributes.

Examples of the "src" attribute:

- "e" (engine), "s" (shaft), "r" (rotor), "p" (propeller), "i" (impeller), "w" (wheel)

Examples of the "id" attribute:

- numerical - e.g. "1", "2", "3" or "4" for cylinder heads
- textual - e.g. "l" / "r" (left / right) for aircraft fuel tanks, or "p" / "s" (port / starboard) for boat engines



Notes

- Tachometers can be found on motor vehicles (rev counter), motor boats (motor RPM) and aircraft (tachometer / tach).
  - Multiple readings are allowed, primarily for helicopters and tanks

WIP

- planes - see [video](https://www.youtube.com/watch?v=fmTsLe8J8QQ) and [another](https://www.youtube.com/watch?v=GU2o2h3EE38) and [another](https://www.youtube.com/watch?v=NZn7Dd2jYFw)

  - Engine
    - Temperature
      - exhtemp - EGT - exhaust gas temperature, either just one cylinder or one for each cylinder - e.g 4 readings
      - engtemp - CHT - cylinder head temperature for each cylinder - e.g 4 readings
    - engrpm - Tachometer for engine - RPM or percentage
  - Carburetor
    - carbtemp - Temperature - positive or negative degrees C
  - Fuel
    - fuelqty - Fuel in each tank (left and right) absolute values (e.g. pounds or US gallons) or percentage
    - fuelpres  - Fuel pressure in psi >= 0 - use kPa
  - Oil
    - oiltemp - Temperature - displayed in C or F
    - oilpres - Pressure in psi >= 0 - use kPa
  - Battery
    - battamp - Ammeter - negative (charging) or positive (discharging) in amps
    - battvolt - Voltage >= 0
  - Vacuum pressure
    - Gyro "suction" float >= 0
- helicopter - [video](https://www.youtube.com/watch?v=regka_rS2Rw)
  - Engine
    - Temperature
      - engtemp - engine / gas generated turbine in degrees C
    - Tach indicators
      - engrpm - engine / gas generated turbine - RPM (or percentage)
      - rotrpm - rotor - RPM or percentage
    - engtorq - Torque indicator (power out of the engine) - PSI (or percentage)
  - Fuel
    - fuelqty - in tank - absolute or percentage
    - fuelpres - Fuel pressure in bars or PSI - use kPa
  - Oil
    - oiltemp - Turbine oil temperature (TOT) - displayed in C or F
    - oilpres - Pressure in bars or PSI - use kPa
  - Battery
    - battamp - Ammeter (DC Amp) - negative (charging) or positive (discharging) in amps
    - battvolt - Voltage >= 0
  - IGNORED FOR NOW
    - warning lights - [video](https://youtu.be/regka_rS2Rw?t=307)
- Boat - stuff not in plane or helicopter
  - Analogue gauges
    - speedometer, tachometer, fuel, trim, water pressure, voltmeter - [video](https://www.youtube.com/watch?v=BOTuN2Hps7Y)
    - oil pressure, fuel level, water temperature
    - dashboard blind with great picture - [link](https://www.wavetowave.com/home/2017/10/3/dashboard-bling-an-overview-of-marine-gauges) with [picture](https://images.squarespace-cdn.com/content/v1/596d2c30d7bdce7d9e727a92/1532739820376-BCDZHKT8KDVRV60HJI0R/Livorsi+Marine+Gauges+blue+monster.jpg?format=2500w)
      - Gauges for each engine
        - tachometer (rpm)
        - Water temp + pressure
        - Oil temp + pressure
        - Fuel level + pressure
      - 2 x battery level (volts)
      - 1 x speed (GPS)
    - cylinder head temp gauge also seen in a video on [YouTube](https://www.youtube.com/watch?v=vyhv3YSibQ0)

  - Coolant
    - coolpres - pressure

  - Boost
    - bstpres - pressure
  - engineer and transmission oil pressure + vaccuum pressure - [link](https://www.youtube.com/watch?v=AWshPMwMbHA&t)
  - fuel efficiency
