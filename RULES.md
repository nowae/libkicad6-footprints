# NOWAE - KiCad6 Footprint Design Rules

Ispired by [KiCad Library Conventions](https://klc.kicad.org/footprint/).
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
* After that they can be split:
  *  by sub-function or by manufacturer;
  *  for connectors without a specific function, the connectors are grouped by their mechanical type (e.g. DSUB, DIN, Header, Socket). In this case, connector libraries must be split by another qualifier (e.g. 2.54mm, 1.27mm)
* Connector libraries can also be split by manufacturer and series, for multi-purpose connectors.

## Footprint name

* General footprint naming conventions
  * Each footprint is a `.kicad_mod` file into a `.pretty` directory.
  * Specific package type is written first.
  * Package name and number of pins are separated by a hyphen (e.g. DIP-20).
  * Packages with special pads add an identifier to the pin count field separated by a hyphen.
    * The field includes the count of uniquely numbered pads of this type.
    * For exposed pads (large copper pad below the part) `[count]EP`.
    * For shield pads `[count]SH` (Unless such a pin is already expected for the part. An example would be a HDMI connector.).
    * For pads connecting pure mechanical mounting leads `[count]MP`.
  * Unique fields (parameters) in the footprint name are separated by _ character.
  * Package dimensions are specified as length x width (and optionally height).
  * Pin layout (e.g. 1x10, 2x15).
  * Orientation (e.g. Horizontal, Vertical).
  * Technology (e.g. THT, SMT).
  
  Not all of the fields defined above are strictly required for a particular footprint.
  For a product series, footprint name is manufacturer code (e.g. Wurth code).

* Footprint naming field prefixes
  * A footprint name has to convey a lot of information to clearly specify the purpose and parameters of the footprint. Some fields in footprint names are common to many footprints and can be shortened using special abbreviations.
  * Not all footprints will require the use of these abbreviations - they are provided as a method of standardising the manner in which footprint parameters are called out when encountered.
  * In many cases, the major dimensions (x/y/z) of a footprint may be specified without a prefix, as the body dimensions are assumed to have the greatest priority in the footprint name.
  * In cases where potential conflicts exist, however, the body dimensions must be explicitly named with the prefix B. Refer to the list below for accepted prefix abbreviations.
    * B: body dimensions
      * Body size (XxYxZ)
      * Height parameter Z may be omitted
      * Prefix B may be omitted if the body size is the major dimension used to define the footprint
    * D: diameter
      * Diameter of major axis for cylindrical component (e.g. D10mm - 10mm diameter)
    * H: height
      * Height of component measured from PCB
      * Body size B should be used in preference, where possible (e.g. H1.1mm - component measures 1.1mm above PCB)
    * L: lenght
      * Length along major axis of component
      * Body size B should be used in preference, where possible (e.g. L15.3mm - 15mm length)
    * W: width
      * Width along minor axis of component
      * Body size B should be used in preference, where possible (e.g. W4.75mm - 4.75mm width)
    * EP: exposed pad dimensions
      * Packages that include a single exposed pad include the size of this pad (e.g. EP2.4x3.6mm - for a single 2.4mm x 3.6mm pad
    * P: pad pitch
      * Pitch (distance) between pins, pads or leads (e.g. P0.63mm - 0.63mm pitch between pads)
    * T: thickness
      * Component thickness, where appropriate

* Footprint naming for non-standard pin numbering
  * In the majority of cases, the pin quantity is self explanatory and is sufficient to describe the number of pins on the symbol.
  * However there may be cases where this numbering is insufficient. Where the number of footprint pins does not match the number of package pins, exceptions must be made.
  * Exception: the numbers for the missing pins are skipped and the normal pin numbers are assigned to the remaining pins. To indicate this, the footprint should be named as PKG-<xx>-<yy> where:
    * xx = number of remaining pins
    * yy = number of remaining pins + number of removed pins

## Layer Requirements

* Silkscreen layer requirements:
  * Reference Designator must be drawn on `F.SilkS` layer, with text size equal to `0.8mm` and text thickness equal to `0.15mm`
  * Silkscreen line width is `0.15mm`
  * Silkscreen must not be placed over pads or areas of exposed copper
  * For SMD footprints, silkscreen must be fully visible after boards assembly
  * Pin-1 designator is provided on the `F.SilkS` layer and must be visible after board assembly

* Fabrication layer requirements:
  * The fabrication layers are used to display the simplified mechanical outline of components on the PCB.
  * Simplified component outline must be provided on `F.Fab` layer, utline line width must be `0.15mm`, but for very small component can be `0.10mm`.
  * Component value (footprint name) must be displayed on the `F.Fab` layer, but it is set _not visible_. Text size must be equal to `0.8mm` and text thickness must be equal to `0.15mm`.
  * A second copy of the reference designator (RefDes) must be provided on the `F.Fab` layer, by using `%R` on the field value. With text size must be equal to `0.8mm` and text thickness must be equal to `0.15mm`.

* Courtyard layer requirements:
  * The component courtyard is defined as the smallest rectangular area that provides a minimum electrical and mechanical clearance around the combined component body and land pattern boundaries.
  * Courtyard uses `0.05mm` line width.
  * All courtyard line elements are placed on a `0.05mm` grid.
  * Unless otherwise specified, clearance is `0.25mm`.
  * Components smaller than `0603` should have a clearance of `0.15mm`.
  * Connectors should have a clearance of `0.5mm`.
  * Crystals should have a clearance of `0.5mm`.
  * BGA devices should have a clearance of `1.0mm` (A middle way of IPC-7351B).
