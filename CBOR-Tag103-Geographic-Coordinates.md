# CBOR Geographic Coordinates

    Tag: 103 (geographic-coordinates)
    Data Item: array
    Semantics: Geographic Coordinates
    Point of contact: Danilo Vidovic <cbor@allthingstalk.com>
    Description of semantics: https://github.com/allthingstalk/cbor/blob/master/CBOR-Tag103-Geographic-Coordinates.md

# Summary

This document specifies a tag for Geographic Coordinates.

# Rationale

[Geographic Coordinates](https://en.wikipedia.org/w/index.php?title=Geographic_coordinate_system&oldid=791574160) are used for specifying every location on Earth. Tag 103 can be used to specify Latitude, Longitude, Elevation and Location Uncertainty, or related coordinates based on a defined Coordinate Reference System (CRS), following [ISO 6709](https://en.wikipedia.org/wiki/ISO_6709) and [RFC 5870](https://tools.ietf.org/html/rfc5870).

# Semantics

Tag 103 can be applied to arrays of length 2 through 6.


Latitude is represented by the first, provided in any number format available in CBOR that is precise enough to represent the needed latitude. Positive values indicate latitudes north of the equator, and negative values indicate latitudes south of the equator unless otherwise specified in the CRS.

Longitude is represented by the second, provided in any number format available in CBOR that is precise enough to represent the needed longitude. Positive values indicate longitudes east of the prime meridian, and negative values indicate longitudes west of the prime meridian unless otherwise specified in the CRS.

Elevation is optionally represented by the third, provided in any number format available in CBOR that is precise enough to represent the elevation in meters unless otherwise specified in the CRS.

Location Uncertainty is optionally represented by the fourth and/or fifth elements of the array. A single location uncertainty shall represent the uncertainty in meters in both the location and elevation. If two uncertainty elements are present, the first shall be specify the horizontal uncertainty in terms of 90% circular error (CE90) and the second shall specify the vertical uncertainty in terms of 90% linear error (LE90). In all cases, any number format available in CBOR that is precise enough to represent the location uncertainty shall be used.

If the final element of the array contains data tagged with CBOR Tag 104-Geographic Coordinate Reference System data that CRS shall be applied to coordinates in this array. If no CRS data is specified, a default CRS shall be assumed. For backward compatibility with an earlier release of this document, the default CRS is EPSG:4326 (WGS84 geographic 3D). An implementation may allow changing of this default CRS by, for example, allowing a naked CBOR tag 104 datum which indicates a change of default CRS. Latitude and logitude are used throughout the rest of this document but they may be substituted for easting and northing or other appropriate terms based on specified CRS.

Setting optional elements to `null` (simple value `F6`) shall be supported. The effect of setting values to `null` shall be the same as omitting them.

# Examples

Geographic coordinates of Belgrade, Serbia.


    D8 67                     # Geographic Coordinates - tag(103)
       84                     #                        - array(4)
          FB 404664AF4F0D844D # Lat: 44.78659° N       - primitive(463...)
          FB 403472EB1C432CA5 # Lon: 20.44890° E       - primitive(462...)
          18 75               # Alt: 117m              - unsigned(117)
          18 05               # Uncertainty: 5m        - unsigned(5)

    # Diagnostic notation: 103([44.78659, 20.44890, 117, 5])

Geographic coordinates of Ghent, Belgium. Altitude and Uncertainty not specified. Coordinates are supplied as half precision floats.


    D8 67                     # Geographic Coordinates - tag(103)
       82                     #                        - array(2)
          F9 5262             # Lat: 51.0625° N        - primitive(21090)
          F9 4377             # Lon:  3.7324° E        - primitive(17271)

    # Diagnostic notation 103([51.0625, 3.732421875])

UTM coordinates of Russian River Brewing, Santa Rosa, California. CRS and uncertainty specified.

    D8 67                     # Geographic Coordinates              - tag(103)
       86                     #                                     - array(6)
          FB 412006D46147AE14 # Easting:  525162.19 m               - primitive(4692758320954977812)
          FB 41503B271A3D70A4 # Northing: 4254876.41 m              - primitive(4706326649732165796)
          FB 4049800000000000 # Alt:      51.0 m                    - primitive(4632374429215621120)
          FB 3FF0000000000000 # CE90:     1.0 m                     - primitive(4607182418800017408)
          FB 4008000000000000 # LE90:     3.0 m                     - primitive(4613937818241073152)
          D8 68               # CRS                                 - tag(104)
             19 7FC6          # EPSG:32710 (UTM zone 10S / WGS 84)  - unsigned(32710)

    # Diagnostic notation 103([525162.19, 4254876.41, 51.0, 1.0, 3.0, 104(32710)])

# References

[1] C. Bormann, and P. Hoffman. "Concise Binary Object Representation (CBOR)". [RFC 7049](https://tools.ietf.org/html/rfc7049), October 2013.

[2] [Geographic coordinate system, Wikipedia](https://en.wikipedia.org/w/index.php?title=Geographic_coordinate_system&oldid=791574160)

[3] [Prime meridian, Wikipedia](https://en.wikipedia.org/w/index.php?title=Prime_meridian&oldid=790973897)

[4] "Standard representation of geographic point location by coordinates". [ISO 6709](https://en.wikipedia.org/w/index.php?title=ISO_6709&oldid=780503062)

[5] [Decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees): In this document, "decimal" is used to describe a system that's an alternative to representing angles in degrees, minutes and seconds.

[6] "A Uniform Resource Identifier for Geographic Locations ('geo' URI)". [RFC 5870](https://tools.ietf.org/html/rfc5870)

[7] "World Geodetic System 1984". [WGS-84](http://www.unoosa.org/pdf/icg/2012/template/WGS_84.pdf)

# Author

Danilo Vidovic <[dv@allthingstalk.com](mailto:dv@allthingstalk.com)>
