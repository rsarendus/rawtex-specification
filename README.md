# [DRAFT] RAWTEX Specification

A binary format for storing image data flexibly with minimal load-time overhead.

The format comes in two flavors: big-endian and little-endian. This enables to serialize image data in an optimal format for different platforms. However, implementations are encouraged to be able to handle non-native endianness and/or support conversion to/from desired endianness, unless doing so would be unreasonable or impractical.


## [DRAFT] RAWTEX Header

| Offset | Octets | Type         | Description |
| ------ | ------ | ------------ | ----------- |
| 0      | 6      | ascii string | Either of the two **format indicator**s:<br><ul><li>`RAWTEX` (<code>52<sub>h</sub> 41<sub>h</sub> 57<sub>h</sub> 54<sub>h</sub> 45<sub>h</sub> 58<sub>h</sub></code>)</li><li>`rawtex` (<code>72<sub>h</sub> 61<sub>h</sub> 77<sub>h</sub> 74<sub>h</sub> 65<sub>h</sub> 78<sub>h</sub></code>)</li></ul> |
| 6      | 1      | uint8        | **Major version number** |
| 7      | 1      | uint8        | **Minor version number** |

* `RAWTEX` - big-endian (BE) flavor of the format
* `rawtex` - little-endian (LE) flavor of the format


## [DRAFT] RAWTEX Body
