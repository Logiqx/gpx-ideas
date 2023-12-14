## GPX Extensions

### Fix Type - gpx_fix

#### Background

The existing `<fix>` element within GPX files supports the following fix types:

| Value | Description                                                  |
| ----- | ------------------------------------------------------------ |
| none  | No GPS fix - e.g. interpolation or just dead-reckoning       |
| 2d    | 2D fix - 3 satellites only, or a fixed altitude solution     |
| 3d    | 3D fix - 4 satellites or more, not a fixed altitude solution |
| dgps  | Differential GPS / GNSS corrections applied                  |
| pps   | Precise Positioning Service - military users and authorised civilian users |

These details can be obtained from [GSA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gsa_gps_dop_and_active_satellites) and [GGA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gga_global_positioning_system_fix_data) sentences, but it should be noted that 2D / 3D, DGPS and PPS are independent.

- 2D and 3D fixes can both utilise DGPS / DGNSS corrections
- PPS solutions can be either 2D or 3D and they can also utilise DGPS / DGNSS corrections

To avoid confusion, 2D / 3D / DGPS should be used for the [Standard Positioning Service](https://gssc.esa.int/navipedia/index.php?title=GPS_Services#Standard_Positioning_Service), and only use PPS for the [Precise Positioning Service](https://gssc.esa.int/navipedia/index.php?title=GPS_Services#Precise_Positioning_Service).

GNSS technology has advanced significantly in the past 20 years so there are several additional fix types to be considered. These include RTK (plus PPK), PPP (plus variations), dead reckoning (with or without a GNSS fix), multi-GNSS solutions, dual-frequency solutions, etc.

This proposal describes a gpx_fix extension that has been designed around the technologies of today and provides extensibility for the technologies of tomorrow. The gpx_fix extension will not completely replace the `<fix>` element, which should still be included in GPX files for backwards compatibility.



### Basic Proposal

The `<gpx_fix:fix>` element has a number of independent attributes. They can all be considered mandatory, but default values within the schema will help to ensure that GPX files do not become unnecessarily bloated / cluttered.

The table below is a summary of the attributes, each of which will be described in more detail later in this proposal.

| Attribute | Possible Values                                              | Default | Description       |
| --------- | ------------------------------------------------------------ | ------- | ----------------- |
| mode      | none \| 2d \| 3d                                             | 3d      | GNSS fix mode     |
| aug       | none \| dgnss \|<br />rtk-float \| rtk-fixed \|<br />ppk-float \| ppk-fixed \|<br />ppp \| ppp-ar \| ppp-rtk | none    | GNSS augmentation |
| dr        | no \| yes                                                    | no      | Dead reckoning    |
| man       | no \| yes                                                    | no      | Manual input      |
| sim       | no \| yes                                                    | no      | Simulation        |
| valid     | no \| yes                                                    | yes     | Data validity     |

The following example illustrates a fixed RTK solution, which can be thought of as a high-precision version of DGPS / DGNSS:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
  <extensions>
    <gpx_fix:fix aug="rtk-fixed" />
  </extensions>
</trkpt>
```

The remainder of this document will describe the various attributes of the `<gpx_fix:fix>` element in much greater detail.



#### Mode (mode)

The fix mode is independent of PPS, augmentation, dead reckoning, multi-GNSS, multi-band, etc.

| Value        | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| none         | Satellite system not used in position fix, or fix not valid  |
| 2d           | 2D fix - 3 satellites only, or an "altitude hold" solution   |
| 3d (default) | 3D fix - 4 satellites or more, and not an "altitude hold" solution |

The fix mode can be found in the [GSA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gsa_gps_dop_and_active_satellites) sentence (1 = none, 2 = 2D fix, 3 = 3D fix).

Example of a 2D standard positioning solution, which is no different to an existing GPX file:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>2d</fix>
</trkpt>
```

Example of a 2D precise positioning solution, which requires a `<gpx_fix:fix>` element:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>pps</fix>
  <extensions>
    <gpx_fix:fix mode="2d" />
  </extensions>
</trkpt>
```

Note: The mode should be "none" to represent no position fix, fix is not valid, or manual input.



#### Augmentation (aug)

[Augmentation](https://gssc.esa.int/navipedia/index.php/GNSS_Augmentation) of a global navigation satellite system (GNSS) is a method of improving – “augmenting” - the navigation system's [performance](https://gssc.esa.int/navipedia/index.php?title=GNSS_Performances).

DGPS / DGNSS has always been common in consumer devices but RTK / PPK and PPP / PPP-AR / PPP-RTK have all been gaining popularity in recent years.

Further details about the different types of augmentation are available later in this document.

| Value          | Description                         |
| -------------- | ----------------------------------- |
| none (default) | Autonomous GPS / GNSS solution      |
| dgnss          | Differential GPS / GNSS corrections |
| ppk-fixed      | PPK fixed solution                  |
| ppk-float      | PPK floating solution               |
| ppp            | Precise Point Positioning (PPP)     |
| ppp-ar         | PPP with ambiguity resolution       |
| ppp-rtk        | PPP-AR with assisted convergence    |
| rtk-fixed      | RTK fixed solution                  |
| rtk-float      | RTK floating solution               |

A regular DGPS / DGNSS solution using SBAS corrections (WAAS, EGNOS, MSAS, GAGAN) only requires the traditional `<fix>` element:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
</trkpt>
```

Augmentations such as PPP-AR will also require the `<gpx_fix:fix>` element.

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
  <extensions>
    <gpx_fix:fix aug="ppp-ar" />
  </extensions>
</trkpt>
```

Background information for all of the different augmentation systems will be included towards the end of this document.



#### Dead Reckoning (dr)

A dead reckoning solution may use dead reckoning only, or combined GPS / GNSS + dead reckoning. Dead reckoning may use the last known GNSS position and velocity, wheel sensors, inertial sensors, or map matching. Dead reckoning is sometimes referred to as an estimated solution.

| Value        | Description                                       |
| ------------ | ------------------------------------------------- |
| no (default) | Solution without the use of dead reckoning        |
| yes          | Dead reckoning solution, with or without GNSS fix |

A solution that only uses dead reckoning may be determined using the quality indicator in [GGA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gga_global_positioning_system_fix_data) (value = 6), or the mode indicator of [GLL](https://gpsd.gitlab.io/gpsd/NMEA.html#_gll_geographic_position_latitudelongitude), [VTG](https://gpsd.gitlab.io/gpsd/NMEA.html#_vtg_track_made_good_and_ground_speed), [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) and [GNS](https://gpsd.gitlab.io/gpsd/NMEA.html#_gns_fix_data) (value = "E"). To identify a combined GPS / GNSS + dead reckoning solution typically requires the binary outputs of the GPS / GNSS chip.

This first example shows a dead reckoning only solution:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>none</fix>
  <extensions>
    <gpx_fix:fix dr="yes" />
  </extensions>
</trkpt>
```

This second example shows a combined GPS / GNSS + dead reckoning solution, also utilising DGPS / DGNSS corrections:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
  <extensions>
    <gpx_fix:fix dr="yes" />
  </extensions>
</trkpt>
```



#### Manual Input (man)

Manual input is fairly self-explanatory. The position is not derived from a GPS / GNSS solution.

| Value        | Description                       |
| ------------ | --------------------------------- |
| no (default) | Position is not from manual input |
| yes          | Manual input                      |

Manual input may be determined by the quality indicator in [GGA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gga_global_positioning_system_fix_data) (value = 7), or the mode indicator of [GLL](https://gpsd.gitlab.io/gpsd/NMEA.html#_gll_geographic_position_latitudelongitude), [VTG](https://gpsd.gitlab.io/gpsd/NMEA.html#_vtg_track_made_good_and_ground_speed), [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) and [GNS](https://gpsd.gitlab.io/gpsd/NMEA.html#_gns_fix_data) (value = "M").

Example of 2D manual input:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>2d</fix>
  <extensions>
    <gpx_fix:fix man="yes" />
  </extensions>
</trkpt>
```



#### Simulation (sim)

A simulation is also fairly self-explanatory, but will primarily be used by researchers and GNSS engineers.

| Value        | Description                  |
| ------------ | ---------------------------- |
| no (default) | Position is not a simulation |
| yes          | Simulation mode              |

Simulations may be determined by the quality indicator in [GGA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gga_global_positioning_system_fix_data) (value = 8), or the mode indicator of [GLL](https://gpsd.gitlab.io/gpsd/NMEA.html#_gll_geographic_position_latitudelongitude), [VTG](https://gpsd.gitlab.io/gpsd/NMEA.html#_vtg_track_made_good_and_ground_speed), [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) and [GNS](https://gpsd.gitlab.io/gpsd/NMEA.html#_gns_fix_data) (value = "S").

Example of a GPS / GNSS + DGPS / DGNSS simulation:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
  <extensions>
    <gpx_fix:fix sim="yes" />
  </extensions>
</trkpt>
```



#### Validity (valid)

A solution may be deemed invalid either because a GNSS fix is unavailable, or because user limits have been exceeded (e.g. DOP, elevation mask, dynamic model, etc).

| Value         | Description     |
| ------------- | --------------- |
| no            | Data is invalid |
| yes (default) | Data is valid   |

Validity can be reliably determined from the status in [GLL](https://gpsd.gitlab.io/gpsd/NMEA.html#_gll_geographic_position_latitudelongitude) or [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) ("A" = valid, "V" = invalid).

It is not safe to use the quality indicator in [GGA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gga_global_positioning_system_fix_data) (value = 0), or mode indicator of [GLL](https://gpsd.gitlab.io/gpsd/NMEA.html#_gll_geographic_position_latitudelongitude), [VTG](https://gpsd.gitlab.io/gpsd/NMEA.html#_vtg_track_made_good_and_ground_speed), [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) and [GNS](https://gpsd.gitlab.io/gpsd/NMEA.html#_gns_fix_data) (value = "N") as a proxy for validity when dead reckoning is in operation. These sentences will typically report dead reckoning, regardless of whether the user limits have been exceeded.

Example of a dead reckoning only solution (without GNSS), where user limits have been exceeded:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>none</fix>
  <extensions>
    <gpx_fix:fix dr="yes" valid="no" />
  </extensions>
</trkpt>
```

Example of a regular GNSS solution, where user limits have been exceeded:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>none</fix>
  <extensions>
    <gpx_fix:fix valid="no" />
  </extensions>
</trkpt>
```

Note: The above examples have been inspired by the u-blox documentation for NMEA position fix flags.



### Representation of Fix Types

The elements `<fix>`  and `<gpx_fix:fix>` complement one other, so neither duplication nor ambiguities should be evident in GPX files. For clarity and backwards compatibility, an appropriate `<fix>`  element should always be included in the GPX file when `<gpx_fix:fix>`  is included.

Earlier in this document it was mentioned that 2D / 3D, DGPS and PPS are all independent, so there are 8 possible combinations. When deciding how to represent these fix types in a GPX file, one must decide which feature is the most pertinent and use that in the traditional `<fix>` element.

In this first example, 2D is deemed the most significant feature and should be used in the `<fix>` element:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>2d</fix>
  <extensions>
    <gpx_fix:fix aug="dgnss" />
  </extensions>
</trkpt>
```

In this second example, PPS is be deemed most significant feature and should be used in the `<fix>` element:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>pps</fix>
  <extensions>
    <gpx_fix:fix aug="dgnss" />
  </extensions>
</trkpt>
```



#### Precise Positioning System

[Precise Positioning System](https://gssc.esa.int/navipedia/index.php?title=GPS_Performances) (PPS) refers to the military GPS positioning, velocity and timing service broadcasted on the GPS L1 and L2 frequencies. This system has never been affected by deliberate degradation (such as Selective Availability) and uses a higher resolution ranging code (P-code) to compute the positional solution. Despite the similarity in names, PPS should not be confused with [Precise Point Positioning](https://novatel.com/an-introduction-to-gnss/resolving-errors/ppp) (PPP).

The P(Y) code (encrypted P code) is broadcast on the GPS L1 and L2 bands with a chipping rate of 10.23 MHz. Although some modern-day signals such as GPS L5, Galileo E5, Galileo E6 PRS, and QZSS L5 also have a chipping rate of 10.23 MHz they should not be referred to as PPS. The phrase Precise Positioning System (PPS) should only be used for the military P(Y) codes broadcast on the GPS L1 and L2 frequencies.

To avoid the potential for confusion in GPX files, `<fix>pps</fix>` should be used solely for GNSS solutions based on the military P(Y) codes.

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>pps</fix>
  <extensions>
    <gpx_fix:fix mode="2d" aug="dgnss" />
  </extensions>
</trkpt>
```

Use of PPS can be determined from the quality indicator of [GGA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gga_global_positioning_system_fix_data) (value = 3) and the mode indicator of [GNS](https://gpsd.gitlab.io/gpsd/NMEA.html#_gns_fix_data) (value = "P"). Some of the other messages such as [GLL](https://gpsd.gitlab.io/gpsd/NMEA.html#_gll_geographic_position_latitudelongitude), [VTG](https://gpsd.gitlab.io/gpsd/NMEA.html#_vtg_track_made_good_and_ground_speed), and [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) also contain a status field (aka [FAA indicator](https://gpsd.gitlab.io/gpsd/NMEA.html#_error_status_indications)) but they don't always mention PPS.



### Interpretation of Fix Types

GPX readers that support the `<gpx_fix:fix>` element should interpret the traditional `<fix>` element as follows:

| `<fix>` | mode | aug    | dr   | man  | sim  | valid |
| ------- | ---- | ------ | ---- | ---- | ---- | ----- |
| none    | none | (none) | (no) | (no) | (no) | (yes) |
| 2d      | 2d   | (none) | (no) | (no) | (no) | (yes) |
| 3d      | 3d   | (none) | (no) | (no) | (no) | (yes) |
| dgps    | (3d) | dgnss  | (no) | (no) | (no) | (yes) |
| pps     | (3d) | (none) | (no) | (no) | (no) | (yes) |

Note that the default values for `<gpx_fix:fix>` have been indicated using brackets.

GPX readers may use the following pseudocode to determine fix mode, augmentation, dead reckoning, manual, simulation and status:

1. Assume defaults
   - mode = "3d"
   - aug = "none"
   - dr = "no"
   - man = "no"
   - sim = "no"
   - valid= "yes"
2. Interpret `<fix>`
   - if fix in ["none", "2d", "3d"] then mode = fix
   - elif fix == "dgps" then aug = "dgnss"
3. Interpret `<gpx_fix:fix>`
   - if has_attribute("mode") then mode = get_attribute("mode")
   - if has_attribute("aug") then aug = get_attribute("aug")
   - if has_attribute("dr") then dr = get_attribute("dr")
   - if has_attribute("man") then man = get_attribute("man")
   - if has_attribute("sim") then sim = get_attribute("sim")
   - if has_attribute("valid") then valid = get_attribute("valid")

GPX readers are free to use whatever logical constructs they wish, so long as the final outcome matches the pseudocode above.



#### Handling Ambiguities

In the event of a GPX file containing an ambiguity the `<gpx_fix:fix>` element should be used in preference to `<fix>`. The pseudocode above describes a strict order for the evaluation of default values, `<fix>` and `<gpx_fix:fix>`, so the expected behavior is completely unambiguous.

This first example is not actually an ambiguity, simply stating the specific type of GNSS augmentation:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
  <extensions>
    <gpx_fix:fix aug="rtk-fixed" />
  </extensions>
</trkpt>
```

This second example contains a contradiction, but the mode in `<gpx_fix:fix>` should take precedence over `<fix>`:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>2d</fix>
  <extensions>
    <gpx_fix:fix mode="3d" />
  </extensions>
</trkpt>
```



#### Forwards Compatibility

GPX readers should be coded such that they can tolerate future additions within the gpx_fix extension:

- Unrecognised elements should be ignored
- Unrecognised attributes should be ignored
- Unrecognised values should be regarded as the default
  - e.g. An unrecognised value in "aug" should be regarded as "dgnss" (default value)



### GNSS Augmentation

#### DGPS / DGNSS

The simplest and most common type of [differential GPS / GNSS](https://gssc.esa.int/navipedia/index.php?title=Differential_GNSS#Differential_GNSS) is known as DGPS / DGNSS. In essence, ground-based reference stations are able to calculate the errors affecting the [pseudorange](https://gssc.esa.int/navipedia/index.php/GNSS_Basic_Observables#Pseudorange) observables, which can then be used by other receivers to calculate more accurate solutions. DGPS / DGNSS may refer to [GBAS](https://gssc.esa.int/navipedia/index.php?title=Ground-Based_Augmentation_System_(GBAS)) or [SBAS](https://gssc.esa.int/navipedia/index.php?title=SBAS_Fundamentals) solutions.

Some examples of satellite based DGNSS:

- SBAS which includes WAAS, EGNOS, MSAS, GAGAN, BDSBAS, etc.
- QZSS Sub-meter Level Augmentation Service ([SLAS](https://qzss.go.jp/en/overview/services/sv05_slas.html)) which is compatible with DGPS code phase positioning.

The best way to indicate that DGPS / DGNSS / SBAS / SLAS is being used is via the original `<fix>` element:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
</trkpt>
```

It would be equally valid to represent DGPS / DGNSS as shown below, but the simpler approach of `<fix>dgps</fix>` is recommended:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>3d</fix>
  <extensions>
    <gpx_fix:fix aug="dgnss" />
  </extensions>
</trkpt>
```

Use of DGPS can be determined by the quality indicator in [GGA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gga_global_positioning_system_fix_data) (value = 2) and the mode indicator / navigation status of [GNS](https://gpsd.gitlab.io/gpsd/NMEA.html#_gns_fix_data), [GLL](https://gpsd.gitlab.io/gpsd/NMEA.html#_gll_geographic_position_latitudelongitude), [VTG](https://gpsd.gitlab.io/gpsd/NMEA.html#_vtg_track_made_good_and_ground_speed), and [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) (value = "D").



#### RTK and PPK

[Real-Time Kinematic](https://gssc.esa.int/navipedia/index.php?title=GNSS_Augmentation#Real_Time_Kinematic_(RTK)) (RTK) and Post-Processed Kinematic (PPK) are high-precision differential solutions. In essence, ground-based reference stations broadcast information that enables other receivers to calculate very precise solutions using the carrier phase observables.

Positions are calculated relative to one or more reference stations which have precisely known positions, thus providing a very precise position for the receiver. RTK can produce either float solutions or fixed solutions, and PPK has the exact equivalents.

Much like DGNSS / SBAS / GBAS, no distinction is proposed for RTK, Network RTK ([NRTK](https://gssc.esa.int/navipedia/index.php?title=RTK_Systems#RTK_Networks) or NTK) or Wide-Area RTK ([WARTK](https://gssc.esa.int/navipedia/index.php?title=Wide_Area_RTK_(WARTK))).

| Augmentation | Description                                  |
| ------------ | -------------------------------------------- |
| ppk-fixed    | Post-Processed Kinematic - fixed solution    |
| ppk-float    | Post-Processed Kinematic - floating solution |
| rtk-fixed    | Real-Time Kinematic - fixed solution         |
| rtk-float    | Real-Time Kinematic - floating solution      |

To avoid possible confusion with PPS, RTK and PPK solutions should be described as `<fix>dgps</fix>`, not `<fix>pps</fix>`.

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
  <extensions>
    <gpx_fix:fix aug="ppk-fixed" />
  </extensions>
</trkpt>
```

Use of RTK (fixed or float) can be determined by the quality indicator in [GGA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gga_global_positioning_system_fix_data) (value = 4 or 5) and the mode indicator / navigation status of [GNS](https://gpsd.gitlab.io/gpsd/NMEA.html#_gns_fix_data), [GLL](https://gpsd.gitlab.io/gpsd/NMEA.html#_gll_geographic_position_latitudelongitude), [VTG](https://gpsd.gitlab.io/gpsd/NMEA.html#_vtg_track_made_good_and_ground_speed), and [RMC](https://gpsd.gitlab.io/gpsd/NMEA.html#_rmc_recommended_minimum_navigation_information) (value = "R" or "F"). PPK implementations will also describe solutions as fixed or float in their output.



#### PPP

[Precise Point Positioning](https://novatel.com/an-introduction-to-gnss/resolving-errors/ppp) (PPP) solutions are high-precision solutions that typically utilise the carrier phase observables and can produce results approaching the accuracy of RTK, without the dependency on concurrent data from nearby reference stations.

All three PPP techniques are supported by the GPX fix extension; PPP, PPP-AR and PPP-RTK. An insight into the differences between these different techniques can be gleaned by reading the definitions in section 2.2 of [PPP/PPP-RTK open formats](https://onlinelibrary.wiley.com/doi/full/10.1002/navi.452).

The GPX fix extension makes no distinction between converging and converged solutions, which is typically based on a user-specified threshold. Once a suitable GPX extension exists, horizontal / vertical accuracy estimates will be the best way to represent the accuracy of a PPP solution.

| Augmentation | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| ppp          | PPP provides a centimeter-to-decimeter level positioning solution by compensating for the satellite SIS errors such as orbit, clock, and signal code bias. |
| ppp-ar       | PPP with phase ambiguity resolution. PPP-AR provides a centimeter level positioning solution by correcting signal phase bias to resolve the integer ambiguity of the carrier phase. Convergence time can be up to 30 minutes. |
| ppp-rtk      | PPP with accuracy close to RTK. PPP-RTK is able to provide position solutions at centimeter level with convergence times similar to RTK using atmospheric corrections. Convergence time can be as little as 1 minute. |

Examples of PPP capabilities for GNSS / RNSS:

- QZSS [MADOCA](https://qzss.go.jp/en/overview/services/sv13_madoca.html) enables PPP / PPP-AR.
- QZSS [CLAS](https://qzss.go.jp/en/overview/services/sv06_clas.html) and Galileo [HAS](https://www.euspa.europa.eu/european-space/galileo/services/galileo-high-accuracy-service-has) enables PPP-RTK.

To avoid possible confusion with PPS, PPP solutions should be described as `<fix>dgps</fix>`, not `<fix>pps</fix>`.

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
  <extensions>
    <gpx_fix:fix aug="ppp-rtk" />
  </extensions>
</trkpt>
```

Use of PPP may be determined from the correction source (e.g. corrSource) in binary messages such as UBX-NAV-SIG.



### GNSS Constellations

This section describes how the number of active GNSS satellites may be recorded using the gpx_fix extension. The number of satellites for each constellation can be represented in the GPX file, both overall and also broken down by signal type.

The elements described in this section are to be used in addition to the existing `<sat>` element, which should still be included in GPX files for backwards compatibility.

#### Multi-GNSS

Multi-GNSS solutions may use several of the global systems (GPS, GLONASS, Galileo and BeiDou / BDS) and regional systems (QZSS and NavIC / IRNSS). The use of multiple constellations increases the accuracy of GNSS solutions, such that they exceed DGPS and the military PPS.

Representing the number of active satellites for each system is desirable, and even the specific signals on dual-band receivers. This proposal uses a dedicated XML element for each constellation, so that specifics such as the different signals can be enumerated in the gpx_fix schema.

This example describes the number of satellites used in the PVT solution, essentially providing a breakdown for the `<sat>` element:

```xml
<trkpt lat="50.5710623" lon="-2.4563484">
  <ele>7.90</ele>
  <time>2022-04-11T10:16:01Z</time>
  <fix>dgps</fix>
  <sat>26</sat>
  <extensions>
    <gpx_fix:fix>
      <gpx_fix:gps sat="7" />
      <gpx_fix:glonass sat="6" />
      <gpx_fix:galileo sat="5" />
      <gpx_fix:beidou sat="5" />
      <gpx_fix:qzss sat="3" />
    </gpx_fix:fix>
  </extensions>
</trkpt>
```

Notes:

- Determining the number of active satellites for each system is possible using GSA sentences, or binary payloads such UBX-NAV-SAT.
  - Further information about the GSA sentence and how it may be interpreted can be found on another [page](https://logiqx.github.io/gps-wizard/nmea/messages/gsa.html).




#### Multi-Band

Multi-band receivers have started to become widely available in the past few years which is another way that the accuracy of GNSS solutions can be improved. The use of multiple frequencies allows the ionospheric errors to be modelled and removed, thus increasing positional accuracy. Some frequencies also include signals with chipping rates matching the military PPS signals (10.23 MHz).

Each of the global and regional constellations have their own frequency bands and signals. Including signal details in a GPX file is probably quite niche, but the information is readily available from [NMEA](https://gpsd.gitlab.io/gpsd/NMEA.html#_nmea_4_11_system_id_and_signal_id) sentences, binary formats such as UBX and the Android [Location](https://developer.android.com/reference/android/location/GnssMeasurement#getCodeType()) API.

The example below shows how the fix of a multi-band GNSS receiver may be represented:

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
      <gpx_fix:galileo sat="5">
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

Notes:

- Determination of systems and signals can be done using [GSA](https://gpsd.gitlab.io/gpsd/NMEA.html#_gsa_gps_dop_and_active_satellites) sentences, or [UBX](https://portal.u-blox.com/s/question/0D52p0000A8lz6oCQA/is-there-a-way-of-knowing-which-satellites-an-f9p-module-is-using-in-an-rtk-solution) payloads such UBX-NAV-SAT or UBX-NAV-SIG.
  - Detailed explanations of GSA sentence and how it may be interpreted can be found on another [page](https://logiqx.github.io/gps-wizard/nmea/messages/gsa.html).
- Android provides satellite and signal information via the [GnssStatus](https://developer.android.com/reference/android/location/GnssStatus) and [GnssMeasurement](https://developer.android.com/reference/android/location/GnssMeasurement#getCodeType()) classes.
- Ordering of `<gpx_fix:sig>` elements cannot be enforced by the XSD, but they should match the order within the enumerated type.
- Full details about the different GNSS signals and the relevant mappings are also described on another [page](systems.md).



### Omissions

The following topics have not been included in this proposal:

- DGPS / DGNSS technology
  - Differentiation between SBAS, SLAS, GBAS and ABAS
  
- SBAS in use - WAAS, EGNOS, MSAS, GAGAN, BDSBAS, etc - see [Navipedia](https://gssc.esa.int/navipedia/index.php/SBAS_Systems)
  - The latest list of systems can be found in the [L1 C/A](https://www.gps.gov/technical/prn-codes/) PRN code assignments
- RTK technology
  - Differentiation between RTK, Network RTK ([NRTK](https://gssc.esa.int/navipedia/index.php?title=RTK_Systems#RTK_Networks)) and Wide-Area RTK ([WARTK](https://gssc.esa.int/navipedia/index.php?title=Wide_Area_RTK_(WARTK))).

- QZSS Indoor Messaging System ([IMES](https://www.unoosa.org/documents/pdf/icg/activities/2008/icg3/32.pdf)) which does not appear to be widely adopted
  - Articles dating from 2009 to 2014 - [Inside GNSS](https://insidegnss.com/qzsss-indoor-messaging-system/) + [GPS World](https://www.gpsworld.com/wirelessindoor-positioningopening-up-indoors-11603/) + [GPS World](https://www.gpsworld.com/danger-will-robinson-beware-the-imes-of-japan/)
- Navigation status from the GNS sentence, and extended FAA mode indicator
  - S = Safe, C = Caution, U = Unsafe, V = Not valid for navigation
- Assisted GPS / GNSS, commonly referred to as A-GPS / A-GNSS
  - This only provides faster time to first fix (TTFF) and initial accuracy
- Super correlation / SGPS - [article](https://www.gpsworld.com/supercorrelation-enhancing-accuracy-sensitivity-of-commercial-receivers/)
  - Perhaps this aspect of the GNSS chip should be mentioned once within the track?



### Schema

The latest provisional schema 0.3 (XSD), plus examples (GPX) reflecting this proposal are available:

- [gpx_fix.xsd](0/3/gpx_fix.xsd)
- [examples.gpx](0/3/examples.gpx)



### References

Some useful links that relate to some of the topics in this document:

- DGPS
  - [RTK, PPK and Autonomous](https://gnss.store/blog/post/rtk-ppp-and-autonomous.html)
- PPP
  - [Precise Point Positioning with Ambiguity Resolution (PPP-AR) Working Group](https://igs.org/wg/ppp-ar/)
  - [PPP/PPP-RTK open formats: Overview, comparison, and proposal for an interoperable message](https://onlinelibrary.wiley.com/doi/full/10.1002/navi.452)
  - [GNSS observable-specific phase biases for all-frequency PPP ambiguity resolution](https://link.springer.com/article/10.1007/s00190-022-01602-3)
  - [Assessment of the performance of GPS/Galileo PPP-RTK convergence using ionospheric corrections from networks with different scales](https://earth-planets-space.springeropen.com/articles/10.1186/s40623-022-01602-9)
  - [PPP–RTK functional models formulated with undifferenced and uncombined GNSS observations](https://satellite-navigation.springeropen.com/articles/10.1186/s43020-022-00064-4)
- Signals
  - Signal plans on ESA Navipedia - [GPS](https://gssc.esa.int/navipedia/index.php?title=GPS_Signal_Plan), [GLONASS](https://gssc.esa.int/navipedia/index.php?title=GLONASS_Signal_Plan), [Galileo](https://gssc.esa.int/navipedia/index.php/Galileo_Signal_Plan#Galileo_E1_Band), [BeiDou](https://gssc.esa.int/navipedia/index.php?title=BeiDou_Signal_Plan) (BDS), [QZSS](https://gssc.esa.int/navipedia/index.php?title=QZSS_Signal_Plan), [IRNSS](https://gssc.esa.int/navipedia/index.php?title=IRNSS_Signal_Plan) (NavIC)
  - [Everything RF](https://www.everythingrf.com/community/navigating-the-l1-l2-and-l5-band-options-for-gnss) - overview of the various frequency bands
  - GPSTest by Barbeau - [description](https://github.com/barbeau/gpstest/blob/221e46cb30612021bc4804adee53af9754dddc39/fastlane/metadata/android/en-US/full_description.txt#L4) + [code](https://github.com/barbeau/gpstest/blob/221e46cb30612021bc4804adee53af9754dddc39/library/src/main/java/com/android/gpstest/library/util/CarrierFreqUtils.java)
