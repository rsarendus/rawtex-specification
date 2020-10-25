# [DRAFT] RAWTEX Specification

A binary format for storing image data flexibly with minimal load-time overhead (e.g. loading image data directly to graphics memory).
The format comes in two flavors: big-endian and little-endian.


## [DRAFT] Header

| Offset | Octets | Type         | Description |
| ------ | ------ | ------------ | ----------- |
| 0      | 6      | ascii string | Either of the two format indicators:<br><ul><li>`RAWTEX` (`52 41 57 54 45 58`)</li><li>`rawtex` (`72 61 77 74 65 78`)</li></ul> |
| 6      | 1      | uint8        | Major version number |
| 7      | 1      | uint8        | Minor version number |

* `RAWTEX` - big-endian (BE) flavor of the format
* `rawtex` - little-endian (LE) flavor of the format


## [DRAFT] Body

### [DRAFT] Version 0

Custom image format.


#### [DRAFT] Version 0.0

<table>
    <tr>
        <th>Offset</th>
        <th>Octets</th>
        <th>Type</th>
        <th colspan="16">Description</th>
    </tr>
    <tr>
        <td rowspan="3">8</td>
        <td rowspan="3">1</td>
        <td rowspan="3">packed8</td>
        <td colspan="16"><b>Image data format configuration</b></td>
    </tr>
    <tr>
        <th colspan="2">Bit 7</th>
        <th colspan="2">Bit 6</th>
        <th colspan="2">Bit 5</th>
        <th colspan="2">Bit 4</th>
        <th colspan="2">Bit 3</th>
        <th colspan="2">Bit 2</th>
        <th colspan="2">Bit 1</th>
        <th colspan="2">Bit 0</th>
    </tr>
    <tr>
        <td colspan="8">RFU</td>
        <td colspan="4">block size</td>
        <td colspan="4">block count size</td>
    </tr>
    <tr>
        <td rowspan="1">9</td>
        <td rowspan="1">1</td>
        <td rowspan="1">uint8</td>
        <td colspan="16"><b>Image format indicator size</b></td>
    </tr>
    <tr>
        <td rowspan="3">10</td>
        <td rowspan="3">2</td>
        <td rowspan="3">packed16</td>
        <td colspan="16"><b>Resolution and compression configuration</b></td>
    </tr>
    <tr>
        <th>Bit 15</th>
        <th>Bit 14</th>
        <th>Bit 13</th>
        <th>Bit 12</th>
        <th>Bit 11</th>
        <th>Bit 10</th>
        <th>Bit 9</th>
        <th>Bit 8</th>
        <th>Bit 7</th>
        <th>Bit 6</th>
        <th>Bit 5</th>
        <th>Bit 4</th>
        <th>Bit 3</th>
        <th>Bit 2</th>
        <th>Bit 1</th>
        <th>Bit 0</th>
    </tr>
    <tr>
        <td>width specified</td>
        <td colspan="2">width size</td>
        <td>height specified</td>
        <td colspan="2">height size</td>
        <td>depth specified</td>
        <td colspan="2">depth size</td>
        <td>layers specified</td>
        <td colspan="2">layers size</td>
        <td>mipmapped</td>
        <td>compressed</td>
        <td colspan="2">compression length size</td>
    </tr>
    <tr>
        <td>12</td>
        <td>1&nbsp;+&nbsp;(<i>image&nbsp;format&nbsp;indicator&nbsp;size</i>)</td>
        <td>octet string</td>
        <td colspan="16"><b>Image format indicator</b></td>
    </tr>
    <tr>
        <td>?</td>
        <td>2<sup>(<i>block&nbsp;count&nbsp;size</i>)</sup></td>
        <td>uint{2<sup>(<i>block&nbsp;count&nbsp;size</i>)</sup>&nbsp;*&nbsp;8}</td>
        <td colspan="16"><b>Block count</b></td>
    </tr>
    <tr>
        <td>?</td>
        <td>if&nbsp;(<i>width&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;2<sup>(<i>width&nbsp;size</i>)</sup><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;(<i>width&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint{2<sup>(<i>width&nbsp;size</i>)</sup>&nbsp;*&nbsp;8}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td colspan="16"><b>Image width</b></td>
    </tr>
    <tr>
        <td>?</td>
        <td>if&nbsp;(<i>height&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;2<sup>(<i>height&nbsp;size</i>)</sup><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;(<i>height&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint{2<sup>(<i>height&nbsp;size</i>)</sup>&nbsp;*&nbsp;8}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td colspan="16"><b>Image height</b></td>
    </tr>
    <tr>
        <td>?</td>
        <td>if&nbsp;(<i>depth&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;2<sup>(<i>depth&nbsp;size</i>)</sup><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;(<i>depth&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint{2<sup>(<i>depth&nbsp;size</i>)</sup>&nbsp;*&nbsp;8}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td colspan="16"><b>Image depth</b></td>
    </tr>
    <tr>
        <td>?</td>
        <td>if&nbsp;(<i>layers&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;2<sup>(<i>layers&nbsp;size</i>)</sup><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;(<i>layers&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint{2<sup>(<i>layers&nbsp;size</i>)</sup>&nbsp;*&nbsp;8}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td colspan="16"><b>Number of layers</b></td>
    </tr>
    <tr>
        <td>?</td>
        <td>if&nbsp;<i>mipmapped</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;1<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;<i>mipmapped</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint8<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td colspan="16"><b>Number of mipmap levels</b></td>
    </tr>
    <tr>
        <td>?</td>
        <td>if&nbsp;<i>compressed</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;2<sup>(<i>compression&nbsp;length&nbsp;size</i>)</sup><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;<i>compressed</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint{2<sup>(<i>compression&nbsp;length&nbsp;size</i>)</sup>&nbsp;*&nbsp;8}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td colspan="16"><b>Compressed data length</b></td>
    </tr>
    <tr>
        <td>?</td>
        <td>if&nbsp;<i>compressed</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;1<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;<i>compressed</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint8<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td colspan="16"><b>Compression format indicator string length</b></td>
    </tr>
    <tr>
        <td>?</td>
        <td>if&nbsp;<i>compressed</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;+&nbsp;(<i>compression&nbsp;format&nbsp;indicator&nbsp;string&nbsp;length</i>)</sup><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;<i>compressed</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;utf-8 string<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td colspan="16"><b>UTF-8 encoded compression format indicator string</b></td>
    </tr>
    <tr>
        <td>?</td>
    <td>if&nbsp;<i>compressed</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;+&nbsp;(<i>compressed&nbsp;data&nbsp;length</i>)<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;2<sup>(<i>block&nbsp;size</i>)</sup>&nbsp;*&nbsp;(1&nbsp;+&nbsp;(<i>block&nbsp;count</i>))</td>
        <td>octet string</td>
        <td colspan="16"><b>Binary image data</b></td>
    </tr>
</table>

**Actual image data block size:**
<pre>2<sup>(<i>block size</i>)</sup></pre>

**Actual image data block count:**
<pre>1 + (<i>block count</i>)</pre>

**Actual image width:**
<pre>
if (<i>width specified</i>) then:
    1 + (<i>image width</i>)
else:
    1
</pre>

**Actual image height:**
<pre>
if (<i>height specified</i>) then:
    1 + (<i>image height</i>)
else:
    1
</pre>

**Actual image depth:**
<pre>
if (<i>depth specified</i>) then:
    1 + (<i>image depth</i>)
else:
    1
</pre>

**Actual number of image layers:**
<pre>
if (<i>layers specified</i>) then:
    1 + (<i>number of layers</i>)
else:
    1
</pre>

**Actual number of mipmap levels:**
<pre>
if <i>mipmapped</i> then:
    1 + (<i>number of mipmap levels</i>)
else:
    1
</pre>


### [DRAFT] Version 1

Custom pixel format.


#### [DRAFT] Version 1.0

<table>
    <tr>
        <th>Offset</th>
        <th>Octets</th>
        <th>Type</th>
        <th colspan="16">Description</th>
    </tr>
    <tr>
        <td rowspan="3">8</td>
        <td rowspan="3">1</td>
        <td rowspan="3">packed8</td>
        <td colspan="16"><b>Image data format configuration</b></td>
    </tr>
    <tr>
        <th colspan="2">Bit 7</th>
        <th colspan="2">Bit 6</th>
        <th colspan="2">Bit 5</th>
        <th colspan="2">Bit 4</th>
        <th colspan="2">Bit 3</th>
        <th colspan="2">Bit 2</th>
        <th colspan="2">Bit 1</th>
        <th colspan="2">Bit 0</th>
    </tr>
    <tr>
        <td colspan="4">RFU</td>
        <td colspan="4">block size <sup>s</sup></td>
        <td colspan="4">RFU</td>
        <td colspan="4">blocks per pixel <sup>m</sup></td>
    </tr>
    <tr>
        <td rowspan="1">9</td>
        <td rowspan="1">1</td>
        <td rowspan="1">uint8</td>
        <td colspan="16"><b>Image format indicator size <sup>m</sup></b></td>
    </tr>
    <tr>
        <td rowspan="3">10</td>
        <td rowspan="3">2</td>
        <td rowspan="3">packed16</td>
        <td colspan="16"><b>Resolution and compression configuration</b></td>
    </tr>
    <tr>
        <th>Bit 15</th>
        <th>Bit 14</th>
        <th>Bit 13</th>
        <th>Bit 12</th>
        <th>Bit 11</th>
        <th>Bit 10</th>
        <th>Bit 9</th>
        <th>Bit 8</th>
        <th>Bit 7</th>
        <th>Bit 6</th>
        <th>Bit 5</th>
        <th>Bit 4</th>
        <th>Bit 3</th>
        <th>Bit 2</th>
        <th>Bit 1</th>
        <th>Bit 0</th>
    </tr>
    <tr>
        <td>width specified</td>
        <td colspan="2">width size <sup>s</sup></td>
        <td>height specified</td>
        <td colspan="2">height size <sup>s</sup></td>
        <td>depth specified</td>
        <td colspan="2">depth size <sup>s</sup></td>
        <td>layers specified</td>
        <td colspan="2">layers size <sup>s</sup></td>
        <td>mipmapped</td>
        <td>compressed</td>
        <td colspan="2">compression length size <sup>s</sup></td>
    </tr>
    <tr>
        <td>12</td>
        <td>1-256</td>
        <td>octet string</td>
        <td colspan="16"><b>Image format indicator</b></td>
    </tr>
    <tr>
        <td rowspan="3">?</td>
        <td rowspan="3">0/1/2/4/8</td>
        <td rowspan="3">uint8/16/32/64</td>
        <td colspan="16"><b>Image width <sup>m</sup></b></td>
    </tr>
    <tr>
        <th colspan="8">(width specified) == 0</th>
        <th colspan="8">(width specified) == 1</th>
    </tr>
    <tr>
        <td colspan="8"><code>1</code></td>
        <td colspan="8"><code><i>value</i> + 1</code></td>
    </tr>
    <tr>
        <td rowspan="3">?</td>
        <td rowspan="3">0/1/2/4/8</td>
        <td rowspan="3">uint8/16/32/64</td>
        <td colspan="16"><b>Image height <sup>m</sup></b></td>
    </tr>
    <tr>
        <th colspan="8">(height specified) == 0</th>
        <th colspan="8">(height specified) == 1</th>
    </tr>
    <tr>
        <td colspan="8"><code>1</code></td>
        <td colspan="8"><code><i>value</i> + 1</code></td>
    </tr>
    <tr>
        <td rowspan="3">?</td>
        <td rowspan="3">0/1/2/4/8</td>
        <td rowspan="3">uint8/16/32/64</td>
        <td colspan="16"><b>Image depth <sup>m</sup></b></td>
    </tr>
    <tr>
        <th colspan="8">(depth specified) == 0</th>
        <th colspan="8">(depth specified) == 1</th>
    </tr>
    <tr>
        <td colspan="8"><code>1</code></td>
        <td colspan="8"><code><i>value</i> + 1</code></td>
    </tr>
    <tr>
        <td rowspan="3">?</td>
        <td rowspan="3">0/1/2/4/8</td>
        <td rowspan="3">uint8/16/32/64</td>
        <td colspan="16"><b>Number of layers <sup>m</sup></b></td>
    </tr>
    <tr>
        <th colspan="8">(layers specified) == 0</th>
        <th colspan="8">(layers specified) == 1</th>
    </tr>
    <tr>
        <td colspan="8"><code>1</code></td>
        <td colspan="8"><code><i>value</i> + 1</code></td>
    </tr>
    <tr>
        <td rowspan="3">?</td>
        <td rowspan="3">0/1</td>
        <td rowspan="3">uint8</td>
        <td colspan="16"><b>Number of mipmap levels <sup>m</sup></b></td>
    </tr>
    <tr>
        <th colspan="8">mipmapped == 0</th>
        <th colspan="8">mipmapped == 1</th>
    </tr>
    <tr>
        <td colspan="8"><code>1</code></td>
        <td colspan="8"><code><i>value</i> + 1</code></td>
    </tr>
    <tr>
        <td rowspan="3">?</td>
        <td rowspan="3">0/1/2/4/8</td>
        <td rowspan="3">uint8/16/32/64</td>
        <td colspan="16"><b>Compressed data length <sup>m</sup></b></td>
    </tr>
    <tr>
        <th colspan="8">compressed == 0</th>
        <th colspan="8">compressed == 1</th>
    </tr>
    <tr>
        <td colspan="8">&ltno compression&gt</td>
        <td colspan="8"><code><i>value</i> + 1</code></td>
    </tr>
    <tr>
        <td rowspan="3">?</td>
        <td rowspan="3">0/1</td>
        <td rowspan="3">uint8</td>
        <td colspan="16"><b>Compression format indicator string length <sup>m</sup></b></td>
    </tr>
    <tr>
        <th colspan="8">compressed == 0</th>
        <th colspan="8">compressed == 1</th>
    </tr>
    <tr>
        <td colspan="8"><code>0</code></td>
        <td colspan="8"><code><i>value</i> + 1</code></td>
    </tr>
    <tr>
        <td>?</td>
        <td>0-256</td>
        <td>utf-8 string</td>
        <td colspan="16"><b>UTF-8 encoded compression format indicator string</b></td>
    </tr>
    <tr>
        <td>?</td>
        <td>?</td>
        <td>octet string</td>
        <td colspan="16"><b>Binary image data</b></td>
    </tr>
</table>

**<sup>m</sup>** a magnitude (length, count, extent), calculated as <code>*value* + 1</code>

**<sup>s</sup>** size of a value, type or block in octets, calculated as <code>2<sup>*value*</sup></code>; in case of specifying a sized type, e.g. **uint*N*** or **packed*N***, then <code>*N* = 2<sup>*value*</sup> * 8</code>
