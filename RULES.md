# NOWAE - KiCad6 Footprint Design Rules

Ispired by [KiCad Library Conventions](https://klc.kicad.org/symbol/).
This document contains our rules to design footprint symbols and is more or less the same of KiCad Conventions.

## Footprint libraries files

Footprints are grouped into directories with `.pretty` extension, based on their primary function.
Library names must be defined based on the priority list below, with each element separated by the underscore character:
* Function (e.g. Connector, Capacitor)
* Sub-function (e.g. HDMI, USB)
* Qualifier (e.g. RightAngle, SMD)
* Manufacturer name (e.g. Wurth, ST)
* Footprint series name (e.g. MicroFit)

### Connector footprint libraries

Connector is very difficult to divide _by function_.
* Connectors are grouped firstly by their primary function (e.g. USB, HDMI)
* After that they can be split by sub-function or by manufacturer
* For connectors without a specific function, then connectors are grouped by their mechanical type (e.g. DSUB, DIN, Header, Socket)
* Connector libraries can be further split by another qualifier (e.g. 2.54mm, 1.27mm)
* Connector libraries can also be split by manufacturer and series, for multi-purpose connectors.

## Footprint name

* General footprint naming conventions
  * Each footprint is a `.kicad_mod` file into a `.pretty` directory.
  * Specific package type is written first
  * Package name and number of pins are separated by a hyphen (e.g. DIP-20)
  * Packages with special pads add an identifier to the pin count field separated by a hyphen...