# CBOR Geographic Coordinate Reference System

    Tag: 104 (geographic-crs)
    Data Item: unsigned integer or text string
    Semantics: Geographic Coordinate Reference System (CRS)
    Point of contact: Danilo Vidovic <cbor@allthingstalk.com>
    Description of semantics: https://github.com/allthingstalk/cbor/blob/master/CBOR-Tag104-Geographic-Coordinate-Reference-System.md

# Summary

This document specifies a tag for Geographic Coordinate Reference System specification.

# Rationale

Specifying geographic coordinates for a location on Earth requires the definition of a coordinate reference system. The Earth is approximately an oblate spheroid but the surface is not completely smooth. High precision location on the surface requires better approximations of this uneven surface. In addition, there are multiple origins for these location values. A [Coordinate Reference System (CRS)](https://en.wikipedia.org/wiki/Spatial_reference_system) provides a definition for the coordinate system and a datum used to approximate the surface. This includes any applied projections to 2 dimentional space. Specifying a CRS for geographic coordinates, instead of assuming a fixed CRS, allows for precision location while minimizing the precision of the underlying numeric values.

This tag is designed for use with the Geographic Coordinates CBOR Tag 103 but may be used independently.

# Semantics

Tag 104 can be applied to a primitive positive integer or a text string.

When applied to an integer, the value specifies a European Petroleum Survey Group (EPSG) spatial reference system identifier (SRID). EPSG is one of many SRID providers but is often used as a defacto standard for CRS specification. This application of Tag 104 allows for a compact CRS specification in a manner which can be universally utilized. EPSG definitions are widely available from sources such as [1] and [2] and are often automatically understood by geographic processing tools and libraries.

When a complete CRS definition is needed, either to avoid reliance on EPSG codes or when a particular CRS is not maintained by EPSG, a text string may be utilized with Tag 104. The value should be an Open Geospatial Consortium (OGC) [4] Well-known Text (WKT) [5] CRS definition.

# Examples

CRS for EPSG:4326, the World Geodetic System 1984 horizontal coordinate system used by GPS satellites.

    D8 68      # Geographic Coordinate System - tag(104)
       19 10E6 # EPSG:4326                    - unsigned(4326)

    # Diagnostic notation: 104(4326)

CRS for WGS 84 3D EGM96 geoid height [3]

    D8 68                                   # Geographic Coordinate System - tag(104)
       79 0191                              # OGC WKT                      - text(401)
          47454F4743535B22574753203834202833442045474D39362067656F69642068656967687429222C444154554D5B22576F726C642047656F64657469632053797374656D2031393834222C53504845524F49445B22574753203834222C363337383133372E302C3239382E3235373232333536332C415554484F524954595B2245505347222C2237303330225D5D2C415554484F524954595B2245505347222C2236333236225D5D2C5052494D454D5B22477265656E77696368222C302E302C415554484F524954595B2245505347222C2238393031225D5D2C554E49545B22444D53222C302E30303030303438343831333638313130393533365D2C415849535B2247656F6465746963206C61746974756465222C4E4F5254485D2C415849535B2247656F6465746963206C6F6E676974756465222C454153545D2C415849535B22477261766974792D72656C6174656420686569676874222C55502C415554484F524954595B2245505347222C2235373733225D5D2C415554484F524954595B2245505347222C2234333239225D5D

    # Diagnostic notation: 104("GEOGCS[\"WGS 84 (3D EGM96 geoid height)\",DATUM[\"World Geodetic System 1984\",SPHEROID[\"WGS 84\",6378137.0,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0.0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"DMS\",0.00000484813681109536],AXIS[\"Geodetic latitude\",NORTH],AXIS[\"Geodetic longitude\",EAST],AXIS[\"Gravity-related height\",UP,AUTHORITY[\"EPSG\",\"5773\"]],AUTHORITY[\"EPSG\",\"4329\"]]")


# References

[1] [MapTiler EPSG Reference Website](https://epsg.io)

[2] [Spatial Reference Website](http://spatialreference.org)

[3] [SR-ORG:7428](http://spatialreference.org/ref/sr-org/7428/)

[4] [Open Geospatial Consortium](http://www.opengeospatial.org/)

[5] [OGC Well-known Text Representation of Coordinate Reference Systems](https://www.opengeospatial.org/standards/wkt-crs)

# Author

Trevor R.H. Clarke <[trevor@notcows.com](mailto:trevor@notcows.com)>
