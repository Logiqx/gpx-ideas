## Systems and Signals

### Introduction

#### Overview

In recent years there has been a move towards common frequency bands centered around 1,575.42 MHz + 1,207.14 MHz + 1,176.45 MHz, simplifying the design and reducing the cost of multi-GNSS receivers.

This document lists the frequency bands currently used by each GNSS, along with the carrier frequencies for the various signals. In addition to frequency information it also lists the signals that are broadcast by each system and where applicable, lists the individuals channels (e.g. data + pilot).

The information in this page is up to date at the time of writing in Dec 2023, but additions will almost certainly be required in the future. For example, [KPS](https://www.gps.gov/cgsic/meetings/2018/lee.pdf) (Korea Positioning System) is planned for 2035 and [LEO-PNT](https://www.esa.int/Applications/Navigation/ESA_plans_for_low-orbiting_navigation_satellites) is currently being planned by the European Space Agency.



#### GNSS Signals

The gpx_fix extension supports signal information in GPX files:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
  <sat>26</sat>
  <extensions>
    <gpx_fix:fix>
      <gpx_fix:gps sat="7">
        <gpx_fix:sig id="l1ca" sat="6" />
        <gpx_fix:sig id="l5" sat="3" />
      </gpx_fix:gps>
      <gpx_fix:glonass sat="6">
        <gpx_fix:sig id="l1of" sat="6" />
      </gpx_fix:glonass>
      <gpx_fix:galileo sat"5">
        <gpx_fix:sig id="e1bc" sat="4" />
        <gpx_fix:sig id="e5a" sat="2" />
      </gpx_fix:galileo>
      <gpx_fix:beidou sat="5">
        <gpx_fix:sig id="b1i" sat="5" />
      </gpx_fix:beidou>
      <gpx_fix:qzss sat="3">
        <gpx_fix:sig id="l1ca" sat="3" />
        <gpx_fix:sig id="l5" sat="2" />
      </gpx_fix:qzss>
    </gpx_fix:fix>
  </extensions>
</trkpt>
```

The `<gpx_fix:sig>` elements simply represent the number of active satellites for each of the GNSS signals. For simplicity, no distinction is made between individual channels (e.g. data and pilot). Neither is there any way to represent visible satellites, only active satellites used in the PVT solution. The example above shows 3 satellites providing L5 signals used in the PVT solution of the GNSS receiver.

The enumerated types in the gpx_fix extension use very simple names for the GNSS signals, entirely lower case and without spaces or punctuation (e.g. hyphens / pluses / slashes / brackets). So whilst different sources may refer to L2C (M), L2 CM, or L2C-M for the data channel of L2C, the gpx_fix extension simply uses "l2c". Likewise for L1 C/A which can be written either with or without a space, but gpx_fix enumerates it as "l1ca".



#### Signal Mappings

Determination of the systems and signals in use will depend on the application:

- NMEA provides [system and signal](https://gpsd.gitlab.io/gpsd/NMEA.html#_nmea_4_11_system_id_and_signal_id) information via the [GSA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gsa_gps_dop_and_active_satellites) sentence.
  - Guidance relating to the interpretation of GSA is available on another [page](https://logiqx.github.io/gps-wizard/nmea/messages/gsa.html).
- Android devices provide the constellation type and carrier frequency via the [GnssStatus](https://developer.android.com/reference/android/location/GnssStatus) class.
  - Android also provides signal information via the [GnssMeasurement](https://developer.android.com/reference/android/location/GnssMeasurement#getCodeType()) class.
- UBX provides the GNSS identifier (gnssId) and usage information (svUsed flag) in [UBX-NAV-SAT](https://content.u-blox.com/sites/default/files/documents/u-blox-F9-HPG-L1L5-1.40_InterfaceDescription_UBX-23006991.pdf)
  - Additional to satellite information, signal information (sigId) and detailed usage can be found in UBX-NAV-SIG.

There are likely to be additional ways that system and signal information can be determined on other hardware.



### GPS

#### Frequency Bands

These are the GPS signals supported by the gpx_fix extension:

| Band | Carrier Frequency |          Signals           |         GPX          |
| :--: | :---------------: | :------------------------: | :------------------: |
|  L1  |   1,575.42 MHz    | L1 C/A, L1 P(Y), L1 M, L1C | l1ca, l1py, l1m, l1c |
|  L2  |   1,227.60 MHz    |     L2 P(Y), L2 M, L2C     |    l2py, l2m, l2c    |
|  L5  |   1,176.45 MHz    |             L5             |          l5          |

Notes

- The gpx_fix extension supports all civilian and military signals, hence the inclusion of P(Y) and M codes.
- The most established GPS signals in the consumer market are L1 C/A, L2C and L5.
- The newer L1C signal will soon gain popularity and is starting to appear in modern GNSS receivers.
- The carrier frequency of L2 is unique to GPSS and QZSS, but L1 and L5 are becoming a common standard.



#### Signals + Channels

These are the mappings which need to be applied to RINEX / UBX / NMEA codes:

| Band | Channel   | Type  | RINEX | UBX  | NMEA 4.10 | NMEA 4.11 | GPX  |
| :--: | --------- | :---: | :---: | :--: | :-------: | :-------: | :--: |
|  L1  | L1 C/A    |       |   C   |  0   |     1     |     1     | l1ca |
|  L1  | L1 P(Y)   |       |   Y   |  -   |     2     |     2     | l1py |
|  L1  | L1 M      |       |   M   |  -   |     3     |     3     | l1m  |
|  L1  | L1C (D)   | data  |   S   |  -   |     -     |     -     | l1c  |
|  L1  | L1C (P)   | pilot |   L   |  -   |     -     |     -     | l1c  |
|  L1  | L1C (D+P) |       |   X   |  -   |     -     |     9     | l1c  |
|  L2  | L2 P(Y)   |       |   Y   |  -   |     4     |     4     | l2py |
|  L2  | L2 M      |       |   M   |  -   |     -     |     -     | l2m  |
|  L2  | L2C (M)   | data  |   S   |  4   |     5     |     5     | l2c  |
|  L2  | L2C (L)   | pilot |   L   |  3   |     6     |     6     | l2c  |
|  L2  | L2C (M+L) |       |   X   |  -   |     -     |     -     | l2c  |
|  L5  | L5 I      | data  |   I   |  6   |     7     |     7     |  l5  |
|  L5  | L5 Q      | pilot |   Q   |  7   |     8     |     8     |  l5  |
|  L5  | L5 I+Q    |       |   X   |  -   |     -     |     -     |  l5  |

Notes

- The L1C signal is relatively new at this time (Dec 2023), denoted by an NMEA value of "9" by Broadcom on the Pixel 7.
- RINEX attributes for z-tracking, [codeless and semi-codeless](https://gssc.esa.int/navipedia/index.php/GPS_C1,_P1_and_P2_Codes_and_Receiver_Types) tracking of the P(Y) code have been omitted.
  - n.b. Z-tracking, codeless and semi-codeless tracking of P(Y) should no [longer be required](https://www.gps.gov/technical/codeless/), due to availability of the L2C signal.

- There is no obvious need for the distinction of an [RMP](https://www.gps.gov/governance/advisory/meetings/2016-12/voce.pdf) antenna being used for the M code in the GPX extension.



### GLONASS

#### Frequency Bands

These are the GLONASS signals supported by the gpx_fix extension:

|  Band   | Carrier Frequency                        |  Signals   |    GPX     |
| :-----: | ---------------------------------------- | :--------: | :--------: |
| G1 / L1 | 1,602 MHz + k * 9 / 16  k =  -7 ... + 12 | L1OF, L1SF | l1of, l1sf |
|   G1a   | 1,600.995 MHz                            | L1OC, L1SC | l1oc, l1sc |
| G2 / L2 | 1,246 MHz + k * 7 / 16  k =  -7 ... + 12 | L2OF, L2SF | l2of, l2sf |
|   G2a   | 1,248.06 MHz                             | L2OC, L2SC | l2oc, l2sc |
| G3 / L3 | 1,202.25 MHz                             |    L3OC    |    l3oc    |

Notes

- The carrier frequencies of G1 / G1a / G2 / G2a / G3 are all unique to GLONASS.
- Different sources refer to G1 / G2 / G3 or L1 / L2 / L3. The official names are L1 / L2 / L3 but G1 / G2 / G3 are less ambiguous.
- Some sources may also refer to the L1OF and L1SF signals (official names) as L1 C/A and L1 P, likewise for L2OF and L2SF.
- The legacy FDMA signals (L1OF / L1SF / L2OF / L2SF) will eventually be superseded by the newer CDMA signals.
- L3OC is a relatively new civilian signal but was available from 47 satellites in 2022, according to the [Novatel](https://novatel.com/an-introduction-to-gnss/gnss-constellations/glonass) page.
- L1OC and L2OC signals are much newer and will be broadcast by GLONASS-K2 satellites, launched in 2023.



#### Signals + Channels

These are the mappings which need to be applied to RINEX / UBX / NMEA codes:

|  Band   | Channel    |  Type   | RINEX | UBX  | NMEA 4.10 | NMEA 4.11 | GPX  |
| :-----: | ---------- | :-----: | :---: | :--: | :-------: | :-------: | :--: |
| G1 / L1 | L1OF C/A   |         |   C   |  0   |     1     |     1     | l1of |
| G1 / L1 | L1SF P     |         |   P   |  -   |     2     |     2     | l1sf |
|   G1a   | L1OC (D)   |  data   |   A   |  -   |     -     |     -     | l1oc |
|   G1a   | L1OC (P)   |  pilot  |   B   |  -   |     -     |     -     | l1oc |
|   G1a   | L1OC (D+P) |         |   X   |  -   |     -     |     -     | l1oc |
|   G1a   | L1SC (D)   |  data   |   -   |  -   |     -     |     -     | l1sc |
|   G1a   | L1SC (P)   |  pilot  |   -   |  -   |     -     |     -     | l1sc |
|   G1a   | L1SC (D+P) |         |   -   |  -   |     -     |     -     | l1sc |
| G2 / L2 | L2OF C/A   |         |   C   |  2   |     3     |     3     | l2of |
| G2 / L2 | L2SF P     |         |   P   |  -   |     4     |     4     | l2sf |
|   G2a   | L2OC (N)   | no data |   A   |  -   |     -     |     -     | l2oc |
|   G2a   | L2OC (P)   |  pilot  |   B   |  -   |     -     |     -     | l2oc |
|   G2a   | L2OC (N+P) |         |   X   |  -   |     -     |     -     | l2oc |
|   G2a   | L2SC (D)   |  data   |   -   |  -   |     -     |     -     | l2sc |
|   G2a   | L2SC (P)   |  pilot  |   -   |  -   |     -     |     -     | l2sc |
|   G2a   | L2SC (D+P) |         |   -   |  -   |     -     |     -     | l2sc |
| G3 / L3 | L3OC I     |  data   |   I   |  -   |     -     |     -     | l3oc |
| G3 / L3 | L3OC Q     |  pilot  |   Q   |  -   |     -     |     -     | l3oc |
| G3 / L3 | L3OC I+Q   |         |   X   |  -   |     -     |     -     | l3oc |

Notes:

- The restricted L1SC and L2SC signals are due to be broadcast by GLONASS-K2 satellites, but are not included in RINEX 4.01.
- The restricted L3SC signal will also be broadcast by GLONASS-KM satellites, but is not included in RINEX 4.01.
- The future L1OCM / L3OCM / L5OCM signals are not supported by RINEX 4.01 or the GPX extension, so may need to be added in the future.



#### Future

Summary of GLONASS-KM:

- The GLONASS-KM satellites will broadcast L3SC / L1OCM / L3OCM / L5OCM but aren't due for launch until 2030, and still in the research phase.
- The GLONASS-KM satellites will add 3 frequency bands for CDMA signals, interoperable with the other GNSS frequency bands:

  - L1 @ 1,575.42 MHz
  - L2 @ 1,207.14 MHz
  - L5 @ 1,176.45 MHz
- The future L3SC / L1OCM / L3OCM / L5OCM signals are not supported by RINEX or the GPX extension, so may need to be added in the future.



### Galileo

#### Frequency Bands

These are the Galileo signals supported by the gpx_fix extension:

| Band | Carrier Frequency | Signals     | GPX       |
| :--: | :---------------: | :---------: | :-------: |
|  E1  |   1,575.42 MHz    | E1-A, E1-BC | e1a, e1bc |
| E5a  |   1,176.45 MHz    | E5a         | e5a       |
| E5b  |   1,207.14 MHz    | E5b         | e5b       |
|  E5  |   1,191.795 MHz   | E5          | e5        |
|  E6  |   1,278.75 MHz    | E6-A, E6-BC | e6a, e6bc |

Notes

- The most widely used Galileo signals are E1bc and E5a, using identical carrier frequencies to L1 and L5 of GPS.
- The carrier frequencies for E1, E5a, E5b and E5 are pretty standard for GNSS, but the frequency of E6 is only shared with QZSS.
- Galileo's E1 band is sometimes referred to as L1, although E1 is the official name.
- [PRS](https://gssc.esa.int/navipedia/index.php/Galileo_Public_Regulated_Service_(PRS)) = Public Regulated Service (channel A), [OS](https://gssc.esa.int/navipedia/index.php?title=Galileo_Open_Service_(OS)) = Open Service (channels B and C)
  - Galileo refers to the E1 PRS and E6 PRS signals as channel A.
  - Galileo refers to the data channels for E1 OS and E6 OS as channel B.
  - Galileo refers to the pilot channels for E1 OS and E6 OS as channel C.




#### Signals + Channels

These are the mappings which need to be applied to RINEX / UBX / NMEA codes:

| Band | Channel |   Type   | RINEX | UBX  | NMEA 4.10 | NMEA 4.11 | GPX  |
| :--: | ------- | :------: | :---: | :--: | :-------: | :-------: | :--: |
|  E1  | E1 A    |   PRS    |   A   |  -   |     6     |     6     | e1a  |
|  E1  | E1 B    | OS data  |   B   |  1   |     -     |     -     | e1bc |
|  E1  | E1 C    | OS pilot |   C   |  0   |     -     |     -     | e1bc |
|  E1  | E1 B+C  |          |   X   |  -   |     7     |     7     | e1bc |
| E5a  | E5a I   |   data   |   I   |  3   |     -     |     -     | e5a  |
| E5a  | E5a Q   |  pilot   |   Q   |  4   |     -     |     -     | e5a  |
| E5a  | E5a I+Q |          |   X   |  -   |     1     |     1     | e5a  |
| E5b  | E5b I   |   data   |   I   |  5   |     -     |     -     | e5b  |
| E5b  | E5b Q   |  pilot   |   Q   |  6   |     -     |     -     | e5b  |
| E5b  | E5b I+Q |          |   X   |  -   |     2     |     2     | e5b  |
|  E5  | E5 I    |   data   |   I   |  -   |     -     |     -     |  e5  |
|  E5  | E5 Q    |  pilot   |   Q   |  -   |     -     |     -     |  e5  |
|  E5  | E5 I+Q  |          |   X   |  -   |     3     |     3     |  e5  |
|  E6  | E6 A    |   PRS    |   A   |  -   |     4     |     4     | e6a  |
|  E6  | E6 B    | CS data  |   B   |  -   |     -     |     -     | e6bc |
|  E6  | E6 C    | CS pilot |   C   |  -   |     -     |     -     | e6bc |
|  E6  | E6 B+C  |          |   X   |  -   |     5     |     5     | e6bc |

Notes:

- RINEX 4.01 includes combined A+B+C channels for the E1 and E6 signals, but they have been omitted from this document.
- NMEA 4.11 does not distinguish between Galileo's data channels and pilot channels.



### BeiDou

#### Frequency Bands

These are the BeiDou / BDS signals supported by the gpx_fix extension:

| Band           | Carrier Frequency |    Signals    | GPX           |
| -------------- | :---------------: | :-----------: | :-----------: |
| B1             |   1,561.098 MHz   |   B1I, B1Q    | b1i, b1q      |
| B1C / B1A      |   1,575.42 MHz    |   B1C, B1A    | b1c, b1a      |
| B2a            |   1,176.45 MHz    |      B2a      | b2a           |
| B2 / B2b       |   1,207.14 MHz    | B2I, B2Q, B2b | b2i, b2q, b2b |
| B2 (B2a + B2b) |   1,191.795 MHz   |      B2       | b2            |
| B3             |   1,268.52 MHz    | B3I, B3Q, B3A | b3i, b3q, b3a |

Notes

- The carrier frequencies of B1C / B1A, B2a, and B2 / B2b are pretty standard for GNSS, but B1 and B3 are unique to BeiDou.
- The B1I / B2I / B3I signals are open services, whereas B1Q / B2Q / B3Q signals are restricted services.
- The most widely used BeiDou civilian signals are B1I and B2I, using carrier frequencies that are not shared with GPS.
- The newer B1C and B2a signals use the same carrier frequencies as the GPS signals in L1 and L5.



#### Signals + Channels

These are the mappings which need to be applied to RINEX / UBX / NMEA codes:

| Band           | Channel   | Type  | RINEX | UBX  | NMEA 4.10 | NMEA 4.11 | GPX  |
| -------------- | --------- | :---: | :---: | :--: | :-------: | :-------: | :--: |
| B1             | B1I       |       |   I   |  ?   |     -     |     1     | b1i  |
| B1             | B1Q       |       |   Q   |  ?   |     -     |     2     | b1q  |
| B1C            | B1C (D)   | data  |   D   |  6   |     -     |     -     | b1c  |
| B1C            | B1C (P)   | pilot |   P   |  5   |     -     |     -     | b1c  |
| B1C            | B1C (D+P) |       |   X   |  -   |     -     |     3     | b1c  |
| B1A            | B1A (D)   | data  |   S   |  -   |     -     |     -     | b1a  |
| B1A            | B1A (P)   | pilot |   L   |  -   |     -     |     -     | b1a  |
| B1A            | B1A (D+P) |       |   Z   |  -   |     -     |     4     | b1a  |
| B2a            | B2a (D)   | data  |   D   |  8   |     -     |     -     | b2a  |
| B2a            | B2a (P)   | pilot |   P   |  7   |     -     |     -     | b2a  |
| B2a            | B2a (D+P) |       |   X   |  -   |     -     |     5     | b2a  |
| B2             | B2I       |       |   I   |  ?   |     -     |     B     | b2i  |
| B2             | B2Q       |       |   Q   |  ?   |     -     |     C     | b2q  |
| B2b            | B2b (D)   | data  |   D   |  -   |     -     |     -     | b2b  |
| B2b            | B2b (P)   | pilot |   P   |  -   |     -     |     -     | b2b  |
| B2b            | B2b (D+P) |       |   Z   |  -   |     -     |     6     | b2b  |
| B2 (B2a + B2b) | B2 (D)    | data  |   D   |  -   |     -     |     -     |  b2  |
| B2 (B2a + B2b) | B2 (P)    | pilot |   P   |  -   |     -     |     -     |  b2  |
| B2 (B2a + B2b) | B2 (D+P)  |       |   X   |  -   |     -     |     7     |  b2  |
| B3             | B3I       |       |   I   |  -   |     -     |     8     | b3i  |
| B3             | B3Q       |       |   Q   |  -   |     -     |     9     | b3q  |
| B3             | B3A (D)   | pilot |   D   |  -   |     -     |     -     | b3a  |
| B3             | B3A (P)   | data  |   P   |  -   |     -     |     -     | b3a  |
| B3             | B3A (D+P) |       |   Z   |  -   |     -     |     A     | b3a  |

Notes:

- The I and Q channels of the B1 / B2 / B3 bands are different services, not a data channel and pilot channel.
  - The table above does not combine I + Q channels, so elements for each signal should be output in the GPX.

- RINEX 4.01 includes combined I+Q channels for the B1 / B2 / B3 signals, but they have been omitted from this document.
- NMEA 4.10 does not include system IDs or signal IDs for BeiDou, QZSS or NavIC.
- NMEA 4.11 does not distinguish between BeiDou's data channels and pilot channels.



### QZSS

#### Frequency Bands

These are the QZSS signals supported by the gpx_fix extension:

| Band | Carrier Frequency | Signals                        | GPX                        |
| :--: | :---------------: | :----------------------------: | :------------------------: |
|  L1  |   1,575.42 MHz    | L1 C/A, L1 C/B, L1C, L1S, L1Sb | l1ca, l1cb, l1c, l1s, l1sb |
|  L2  |   1,227.60 MHz    | L2C                            | l2c                        |
|  L5  |   1,176.45 MHz    | L5, L5S                        | l5, l5s                    |
|  L6  |   1,278.75 MHz    | L6D, L6E                       | l6d, l6e                   |

Notes

- QZSS has the highest level of interoperability with GPS, due to near-identical use of the L1, L2 and L5 bands.
- L1 / L2 / L5 use the same carrier frequencies as GPS, whilst L6 uses the same carrier frequency as E6 for Galileo.
- L1S is the Sub-meter Level Augmentation Service ([SLAS](https://qzss.go.jp/en/overview/services/sv05_slas.html)) and L1Sb is a regular [SBAS](https://qzss.go.jp/en/overview/services/sv12_sbas.html) signal.
- L5S is the positioning technology verification service.
- L6 (LEX) is the Centimeter Level Augmentation Service ([CLAS](https://qzss.go.jp/en/overview/services/sv06_clas.html)).



#### Signals + Channels

These are the mappings which need to be applied to RINEX / UBX / NMEA codes:

| Band | Channel  | Type   | RINEX | UBX | NMEA 4.10 | NMEA 4.11 |  GPX   |
| :--: | -------- | :---: | :---: | :----: | :-------: | :-------: | :----: |
|  L1  | L1 C/A   |        |   C   |   0    |     -     |     1     | l1ca |
|  L1  | L1 C/B   |       |   E   |   -    |     -     |     -     | l1cb |
|  L1  | L1C (D) | data   |   S   |   -    |     -     |     2     |  l1c   |
|  L1  | L1C (P) | pilot  |   L   |   -    |     -     |     3     |  l1c   |
|  L1  | L1C (D+P) |        |   X   |   -    |     -     |     -     |  l1c   |
|  L1  | L1S      | SLAS   |   Z   |   1    |     -     |     4     |  l1s   |
|  L1  | L1Sb     | SBAS   |   B   |   -    |     -     |     -     |  l1sb  |
|  L2  | L2C (M) | data   |   S   |   4    |     -     |     5     |  l2c   |
|  L2  | L2C (L) | pilot  |   L   |   5    |     -     |     6     |  l2c   |
|  L2  | L2C (M+L) |        |   X   |   -    |     -     |     -     |  l2c   |
|  L5  | L5 I     | data   |   I   |   8    |     -     |     7     |   l5   |
|  L5  | L5 Q     | pilot  |   Q   |   9    |     -     |     8     |   l5   |
|  L5  | L5 I + Q |        |   X   |   -    |     -     |     -     |   l5   |
|  L5  | L5S I    | data   |   D   |   -    |     -     |     -     |  l5s   |
|  L5  | L5S Q    | pilot  |   P   |   -    |     -     |     -     |  l5s   |
|  L5  | L5S I + Q |        |   Z   |   -    |     -     |     -     |  l5s   |
|  L6  | L6D      | code 1 |   S   |   -    |     -     |     9     |   l6d   |
|  L6  | L6P      | pilot  |   L   |   -    |     -     |     -     |   l6d   |
|  L6  | L6 (D+P) |        |   X   |   -    |     -     |     -     |   l6d   |
|  L6  | L6E      | code 2 |   E   |   -    |     -     |     A     |   l6e   |
|  L6  | L6 (D+E) |        |   Z   |   -    |     -     |     -     |   l6e   |

Notes

- NMEA 4.10 does not include a system ID or signal IDs for QZSS.



### NavIC

#### Frequency Bands

These are the NavIC / IRNSS signals supported by the gpx_fix extension:

| Band | Carrier Frequency |    Signals    |     GPX     |
| :--: | :---------------: | :-----------: | :---------: |
|  L1  |   1,575.42 MHz    |    L1-SPS     |    l1sps    |
|  L5  |   1,176.45 MHz    | L5-SPS, L5-RS | l5sps, l5rs |
|  S   |   2,492.028 MHz   |  S-SPS, S-RS  |  ssps, srs  |

Notes

- The L1 and L5 bands have the same carrier frequencies as GPS.
- SPS = Standard Positioning Service for civilian use
- RS = Restricted Service



#### Signals + Channels

These are the mappings which need to be applied to RINEX / UBX / NMEA codes:

| Band | Channel     | Type  | RINEX | UBX  | NMEA 4.10 | NMEA 4.11 |  GPX  |
| :--: | ----------- | :---: | ----- | :--: | :-------: | :-------: | :---: |
|  L1  | L1 Data     | data  | D     |  -   |     -     |     -     | l1sps |
|  L1  | L1 Pilot    | pilot | P     |  -   |     -     |     -     | l1sps |
|  L1  | L1          |       | X     |  -   |     -     |     5     | l1sps |
|  L5  | L5 A SPS    |       | A     |  -   |     -     |     1     | l5sps |
|  L5  | L5 B RS (D) | data  | B     |  -   |     -     |     -     | l5rs  |
|  L5  | L5 C RS (P) | pilot | C     |  -   |     -     |     -     | l5rs  |
|  L5  | L5 B+C      |       | X     |  -   |     -     |     3     | l5rs  |
|  S   | S A SPS     |       | A     |  -   |     -     |     2     | ssps  |
|  S   | S B RS (D)  | data  | B     |  -   |     -     |     -     |  srs  |
|  S   | S C RS (P)  | pilot | C     |  -   |     -     |     -     |  srs  |
|  S   | S B+C       |       | X     |  -   |     -     |     4     |  srs  |

Notes

- NMEA 4.10 does not include a system ID or signal IDs for NavIC.
- NMEA 4.11 does not distinguish between NavIC's data channels and pilot channels.



### SBAS

#### Frequency Bands

These are the SBAS signals supported by the gpx_fix extension:

| Band | Carrier Frequency | Signals | GPX  |
| :--: | :---------------: | :-----: | :--: |
|  L1  |   1,575.42 MHz    | L1 C/A  | l1ca |
|  L5  |   1,176.45 MHz    |   L5    |  l5  |

Notes

- The L1 and L5 bands have the same carrier frequencies as GPS.



#### Signals + Channels

These are the mappings which need to be applied to RINEX / UBX / NMEA codes:

| Band | Channel | Type  | RINEX | UBX  | NMEA 4.10 | NMEA 4.11 | GPX  |
| :--: | ------- | :---: | :---: | :--: | :-------: | :-------: | :--: |
|  L1  | L1 C/A  |       |   C   |  0   |     1     |     1     | l1ca |
|  L5  | L5 I    | Data  |   I   |  -   |     -     |     -     |  l5  |
|  L5  | L5 Q    | Pilot |   Q   |  -   |     -     |     -     |  l5  |

Notes:

- These signals are very similar in nature to L1 C/A and L5 of GPS.



### References

A number of sources were used to document the signal mappings in this document.

- RINEX 4.01 [specification](https://files.igs.org/pub/data/format/rinex_4.01.pdf)
- Android [location](https://developer.android.com/reference/android/location/GnssMeasurement#getCodeType()) API
- Novatel [system and signal IDs](https://docs.novatel.com/OEM7/Content/Logs/GPGRS.htm#System)
- u-blox [F9P](https://content.u-blox.com/sites/default/files/documents/u-blox-F9-HPG-L1L5-1.40_InterfaceDescription_UBX-23006991.pdf) interface specification
- QZSS interface specifications for [CLAS](https://qzss.go.jp/en/technical/download/pdf/ps-is-qzss/is-qzss-l6-005.pdf?t=1701905002874) and [MADOCA](https://qzss.go.jp/en/technical/download/pdf/ps-is-qzss/is-qzss-mdc-002.pdf?t=1701905094923)

In addition to the above, obvious sources such as the Wikipedia pages for each GNSS were also referenced.
