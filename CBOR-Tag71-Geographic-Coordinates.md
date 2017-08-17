# CBOR Geographic Coordinates

    Tag: 71 (geographic-coordinates)
    Data Item: array
    Semantics: Geographic Coordinates
    Point of contact: Danilo Vidovic <cbor@allthingstalk.com>
    Description of semantics: https://github.com/allthingstalk/cbor/blob/master/CBOR-Tag71-Geographic-Coordinates.md

# Summary

This document specifies a tag for Geographic Coordinates.

# Rationale

[Geographic Coordinates](https://en.wikipedia.org/w/index.php?title=Geographic_coordinate_system&oldid=791574160) are used for specifying every location on Earth. The usual choice uses Latitude, Longitude and Elevation, following [ISO 6709](https://en.wikipedia.org/wiki/ISO_6709). This is what Tag 71 supports as well.

# Semantics

Tag 71 can be applied to arrays of length 2 and 3.

Latitude is represented by the first element of the array, in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees), provided in any number format available in CBOR that is precise enough to represent the needed latitude. Positive values indicate latitudes north of the equator, and negative values indicate latitudes south of the equator.

Longitude is represented by the second element of the array, provided in any number format available in CBOR that is precise enough to represent the needed longitude. Positive values indicate longitudes east of the [prime meridian](https://en.wikipedia.org/w/index.php?title=Prime_meridian&oldid=790973897), and negative values indicate longitudes west of the prime meridian.

Elevation is optionally represented by the third element of the array, provided in any number format available in CBOR that is precise enough to represent the elevation in meters.

# Example

Geographic coordinates of Belgrade, Serbia.


    D8 47                     # Geographic Coordinates - tag(71)
       83                     #                          array(3)
          FB 404664AF4F0D844D # Lat: 44.78659...° N    - primitive(463...)
          FB 403472EB1C432CA5 # Lon: 20.44890...° E    - primitive(462...)
          18 75               # Alt: 117m              - unsigned(117)

    # Diagnostic notation: 71([44.78659, 20.44890, 117])

# References

[1] C. Bormann, and P. Hoffman. "Concise Binary Object Representation (CBOR)". [RFC 7049](https://tools.ietf.org/html/rfc7049), October 2013.

[2] [Geographic coordinate system, Wikipedia](https://en.wikipedia.org/w/index.php?title=Geographic_coordinate_system&oldid=791574160)

[3] [Prime meridian, Wikipedia](https://en.wikipedia.org/w/index.php?title=Prime_meridian&oldid=790973897)

[4] [ISO 6709 - Standard representation of geographic point location by coordinates](https://en.wikipedia.org/w/index.php?title=ISO_6709&oldid=780503062)

[5] [Decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees)

# Author

Danilo Vidovic <[dv@allthingstalk.com](mailto:dv@allthingstalk.com)>
