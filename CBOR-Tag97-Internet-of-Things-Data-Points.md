# CBOR Internet of Things Data Points

    Tag: 97 (iot-data-point)
    Data Item: multiple
    Semantics: Internet of Things Data Point
    Point of contact: Danilo Vidovic <cbor@allthingstalk.com>
    Description of semantics: https://github.com/allthingstalk/cbor/blob/master/CBOR-Tag97-Internet-of-Things-Data-Points.md

# Summary

This document specifies a tag for Internet of Things Data Points.

# Rationale

Internet of Things (IoT) devices are often memory and bandwidth constrained, so using CBOR to encode their sensor data is a good fit. Sensor data can vary in type, and most of the types are supported by CBOR already, or can easily be supported by defining additional tags. However, IoT sensor values are rarely useful without metadata that describes the context in which this data was obtained.

The most general metadata that can be supplied by IoT devices are the timestamp of data retrieval, and the location at which the data was retrieved. Together with sensor values, they form Internet of Things Data Points.

# Semantics

Tag 97 can be applied to all major types, but has a special meaning when applied to arrays.

When applied to non-array types, Tag 97 indicates that the provided value is an IoT Data Point, with its timestamp being the current UTC time, and its geographic coordinates undefined.

When Tag 97 is applied to an array, the first element of the array represents the value of the IoT Data Point, the second element is data point’s timestamp, represented using Tags 0, 1 or 1001, and the third element contains data point’s geographic coordinates, represented using Tag 103. Both the second and the third element are optional. Omitting geographic coordinates makes them undefined, and omitting the timestamp sets it to the current UTC time.

# Example

A weather balloon sending temperature data would encode the data as follows:


    D8 61                           # IoT Data Point       - tag(97)
       83                           #                        array(3)
          F9 4DE0                   # 23.5 (°C)            - primitive(19936)
          C1                        # Timestamp            - tag(1)
             1A 59682F00            # 2017/07/14 02:40 UTC - unsigned(1500000000)
          D8 67                     # Geographic           - tag(103)
             83                     #    Coordinates         array(3)
                FB 404664AF4F0D844D # Lat: 44.78659...° N  - primitive(463...)
                FB 403472EB1C432CA5 # Lon: 20.44890...° E  - primitive(462...)
                18 75               # Elevation: 117m      - unsigned(117)

    # Diagnostic notation: 97([23.5, 1(1500000000), 103([44.78659, 20.44890, 117])])

Notice that temperature value is sent as a single precision float. There’s nothing indicating that 23.5 is degrees Celsius. This is intentional — describing physical units should be left either to the IoT system, or to other CBOR Tags which can then be used to wrap the value.

# References

[1] C. Bormann, and P. Hoffman. "Concise Binary Object Representation (CBOR)". [RFC 7049](https://tools.ietf.org/html/rfc7049), October 2013.

# Author

Danilo Vidovic <[dv@allthingstalk.com](mailto:dv@allthingstalk.com)>
