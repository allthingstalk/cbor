# CBOR Geographic Coordinates

    Tag: 103 (geographic-coordinates)
    Data Item: array
    Semantics: Geographic Coordinates
    Point of contact: Danilo Vidovic <cbor@allthingstalk.com>
    Description of semantics: https://github.com/allthingstalk/cbor/blob/master/CBOR-Tag103-Geographic-Coordinates.md

# Summary

This document specifies a tag for Geographic Coordinates.

# Rationale

[Geographic Coordinates](https://en.wikipedia.org/w/index.php?title=Geographic_coordinate_system&oldid=791574160) are used for specifying every location on Earth. The usual choice uses Latitude, Longitude and Elevation, following [ISO 6709](https://en.wikipedia.org/wiki/ISO_6709). This is what Tag 103 supports as well.

Additionally supported by this tag is Location Uncertainty, as defined in [RFC 5870, 3.4.3.](https://tools.ietf.org/html/rfc5870#section-3.4.3).

# Semantics

Tag 103 can be applied to arrays of length 2, 3 and 4.

Latitude is represented by the first element of the array, in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees), provided in any number format available in CBOR that is precise enough to represent the needed latitude. Positive values indicate latitudes north of the equator, and negative values indicate latitudes south of the equator.

Longitude is represented by the second element of the array, provided in any number format available in CBOR that is precise enough to represent the needed longitude. Positive values indicate longitudes east of the [prime meridian](https://en.wikipedia.org/w/index.php?title=Prime_meridian&oldid=790973897), and negative values indicate longitudes west of the prime meridian.

Elevation is optionally represented by the third element of the array, provided in any number format available in CBOR that is precise enough to represent the elevation in meters.

Location Uncertainty is optionally represented by the fourth element of the array, provided in any number format available in CBOR that is precise enough to represent the uncertainty in meters with which the location is known.

Setting Elevation and Location Uncertainty to `null` (simple value `F6`) should be supported. The effect of setting values to `null` should be the same as omitting them.

## Coordinate reference system

The coordinate reference system (CRS) in which these values are defined is the World Geodetic System 1984 [WGS-84](http://www.unoosa.org/pdf/icg/2012/template/WGS_84.pdf). The choice of WGS-84 as the default CRS is based on the widespread availability of Global Positioning System (GPS) devices, which use the WGS-84 reference system. This is similar to 'geo' URIs described in [RFC 5870](https://tools.ietf.org/html/rfc5870). Specifying alternative coordinate reference systems is not supported.

# Examples

Geographic coordinates of Belgrade, Serbia.


    D8 67                     # Geographic Coordinates - tag(103)
       84                     #                        - array(4)
          FB 404664AF4F0D844D # Lat: 44.7866° N        - primitive(463...)
          FB 403472EB1C432CA5 # Lon: 20.4489° E        - primitive(462...)
          18 75               # Alt: 117m              - unsigned(117)
          18 05               # Uncertainty: 5m        - unsigned(5)

    # Diagnostic notation: 103([44.7866, 20.4489, 117, 5])

Geographic coordinates of Ghent, Belgium. Altitude and Uncertainty not specified. Coordinates are supplied as half precision floats.


    D8 67                     # Geographic Coordinates - tag(103)
       82                     #                        - array(2)
          F9 5262             # Lat: 51.0625° N        - primitive(21090)
          F9 4377             # Lon:  3.7324° E        - primitive(17271)

    # Diagnostic notation 103([51.0625, 3.732421875])

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
