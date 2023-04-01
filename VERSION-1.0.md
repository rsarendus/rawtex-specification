# [DRAFT] RAWTEX Version 1.0

Version **1.0** of the [RAWTEX](README.md) binary format.


## [DRAFT] RAWTEX Header

RAWTEX binary format header is specified in [RAWTEX Specification: RAWTEX Header](README.md#draft-rawtex-header).


## [DRAFT] RAWTEX Body version 1.0

| Offset | Octets  | Type     | Description |
| -----: | ------: | :------: | :---------- |
| 8      | 2       | packed16 | [**Image extents flags**](#image-extents-flags) |
| 10     | 1       | packed8  | [**Image data flags**](#image-data-flags) |
| 11     | 1       | packed8  | [**Compression flags**](#compression-flags) |
| 12     | 0...33  | ?        | [**Image extents**](#image-extents) |
| ?      | 3...265 | ?        | [**Image data format and length**](#image-data-format-and-length) |
| ?      | 0...265 | ?        | [**Compression format and length**](#compression-format-and-length) |
| ?      | ?       | ?        | [**Image data**](#image-data) |


### Image extents flags

The layout of **image extents flags**, packed into two consecutive octets, forming a 16-bit block:

<table>
    <tr>
        <th align="center" width="6%">15</th>
        <th align="center" width="6%">14</th>
        <th align="center" width="6%">13</th>
        <th align="center" width="6%">12</th>
        <th align="center" width="6%">11</th>
        <th align="center" width="6%">10</th>
        <th align="center" width="6%">9</th>
        <th align="center" width="6%">8</th>
        <th align="center" width="6%">7</th>
        <th align="center" width="6%">6</th>
        <th align="center" width="6%">5</th>
        <th align="center" width="6%">4</th>
        <th align="center" width="6%">3</th>
        <th align="center" width="6%">2</th>
        <th align="center" width="6%">1</th>
        <th align="center" width="6%">0</th>
    </tr>
    <tr>
        <td align="center" colspan="1"><b>Width specified</b></td>
        <td align="center" colspan="2"><b>Width size</b></td>
        <td align="center" colspan="1"><b>Height specified</b></td>
        <td align="center" colspan="2"><b>Height size</b></td>
        <td align="center" colspan="1"><b>Depth specified</b></td>
        <td align="center" colspan="2"><b>Depth size</b></td>
        <td align="center" colspan="1"><b>Layer count specified</b></td>
        <td align="center" colspan="2"><b>Layer count size</b></td>
        <td align="center" colspan="1"><b>Mipmapped</b></td>
        <td align="center" colspan="3"><b>RFU</b></td>
    </tr>
    <tr>
        <td align="center" colspan="1">{boolean}</td>
        <td align="center" colspan="2">2<sup>{uint2}</sup></td>
        <td align="center" colspan="1">{boolean}</td>
        <td align="center" colspan="2">2<sup>{uint2}</sup></td>
        <td align="center" colspan="1">{boolean}</td>
        <td align="center" colspan="2">2<sup>{uint2}</sup></td>
        <td align="center" colspan="1">{boolean}</td>
        <td align="center" colspan="2">2<sup>{uint2}</sup></td>
        <td align="center" colspan="1">{boolean}</td>
        <td align="center" colspan="3">&empty;</td>
    </tr>
</table>

In case **width specified** is `true`, **width size** shall specify the number of octets allocated to the **image width** value.
In case **width specified** is `false`, **width size** shall be equal to `0` and **image width** shall default to `1`.

In case **height specified** is `true`, **height size** shall specify the number of octets allocated to the **image height** value.
In case **height specified** is `false`, **height size** shall be equal to `0` and **image height** shall default to `1`.

In case **depth specified** is `true`, **height size** shall specify the number of octets allocated to the **image depth** value.
In case **depth specified** is `false`, **height size** shall be equal to `0` and **image depth** shall default to `1`.

In case **layer count specified** is `true`, **layer count size** shall specify the number of octets allocated to the **image layer count** value.
In case **layer count specified** is `false`, **layer count size** shall be equal to `0` and **image layer count** shall default to `1`.

In case **mipmapped** is `true`, a single octet shall be allocated to the **number of mipmap levels** value.
In case **mipmapped** is `false`, no octets shall be allocated to the **number of mipmap levels** value and **number of mipmap levels** shall default to `1`.


### Image data flags

The layout of **image data flags**, packed into a single octet, forming an 8-bit block:

<table>
    <tr>
        <th align="center" width="12%">7</th>
        <th align="center" width="12%">6</th>
        <th align="center" width="12%">5</th>
        <th align="center" width="12%">4</th>
        <th align="center" width="12%">3</th>
        <th align="center" width="12%">2</th>
        <th align="center" width="12%">1</th>
        <th align="center" width="12%">0</th>
    </tr>
    <tr>
        <td align="center" colspan="4">RFU</td>
        <td align="center" colspan="2"><b>Block size</b></td>
        <td align="center" colspan="2"><b>Block count size</b></td>
    </tr>
    <tr>
        <td align="center" colspan="4">&empty;</td>
        <td align="center" colspan="2">2<sup>{uint2}</sup></td>
        <td align="center" colspan="2">2<sup>{uint2}</sup></td>
    </tr>
</table>

**Block size** shall specify whether image data consists of single octet, 16-bit, 32-bit or 64-bit blocks.

**Block count size** shall specify the number of octets allocated to the **block count** value.


### Compression flags

The layout of **compression flags**, packed into a single octet, forming an 8-bit block:

<table>
    <tr>
        <th align="center" width="12%">7</th>
        <th align="center" width="12%">6</th>
        <th align="center" width="12%">5</th>
        <th align="center" width="12%">4</th>
        <th align="center" width="12%">3</th>
        <th align="center" width="12%">2</th>
        <th align="center" width="12%">1</th>
        <th align="center" width="12%">0</th>
    </tr>
    <tr>
        <td align="center" colspan="1"><b>Compressed</b></td>
        <td align="center" colspan="2"><b>Compression length size</b></td>
        <td align="center" colspan="5">RFU</td>
    </tr>
    <tr>
        <td align="center" colspan="1">{boolean}</td>
        <td align="center" colspan="2">2<sup>{uint2}</sup></td>
        <td align="center" colspan="5">&empty;</td>
    </tr>
</table>

In case **compressed** is `true`, **compression length size** shall specify the number of octets allocated to the **compressed image data length** value.
In case **compressed** is `false`, **compression length size** shall be equal to `0` and no **compressed image data length** value shall be present.


### Image extents

<table>
    <tr>
        <th align="center"></th>
        <th align="center">Octets</th>
        <th align="center">Type</th>
        <th align="center">Value</th>
    </tr>
    <tr>
        <td><b>Image width:</b></td>
        <td>if&nbsp;(<i>width&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;<i>width&nbsp;size</i><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;(<i>width&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint{(<i>width&nbsp;size</i>)&nbsp;&times;&nbsp;8}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td>if&nbsp;(<i>width&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&plus;&nbsp;{uint?}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;1</td>
    </tr>
    <tr>
        <td><b>Image height:</b></td>
        <td>if&nbsp;(<i>height&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;<i>height&nbsp;size</i><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;(<i>height&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint{(<i>height&nbsp;size</i>)&nbsp;&times;&nbsp;8}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td>if&nbsp;(<i>height&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&plus;&nbsp;{uint?}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;1</td>
    </tr>
    <tr>
        <td><b>Image depth:</b></td>
        <td>if&nbsp;(<i>depth&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;<i>depth&nbsp;size</i><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;(<i>depth&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint{(<i>depth&nbsp;size</i>)&nbsp;&times;&nbsp;8}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td>if&nbsp;(<i>depth&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&plus;&nbsp;{uint?}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;1</td>
    </tr>
    <tr>
        <td><b>Image layer count:</b></td>
        <td>if&nbsp;(<i>layers&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;<i>layer&nbsp;count&nbsp;size</i><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;(<i>layers&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint{(<i>layer&nbsp;count&nbsp;size</i>)&nbsp;&times;&nbsp;8}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td>if&nbsp;(<i>layers&nbsp;specified</i>)&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&plus;&nbsp;{uint?}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;1</td>
    </tr>
    <tr>
        <td><b>Number of mipmap levels:</b></td>
        <td>if&nbsp;<i>mipmapped</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;1<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;0</td>
        <td>if&nbsp;<i>mipmapped</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;uint8<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;&empty;</td>
        <td>if&nbsp;<i>mipmapped</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&plus;&nbsp;{uint8}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;1</td>
    </tr>
</table>


### Image data format and length

<table>
    <tr>
        <th align="center"></th>
        <th align="center">Octets</th>
        <th align="center">Type</th>
        <th align="center">Value</th>
    </tr>
    <tr>
        <td><b>Image data format indicator length:</b></td>
        <td align="right">1</td>
        <td align="center">uint8</td>
        <td align="center">1&nbsp;&plus;&nbsp;{uint8}</td>
    </tr>
    <tr>
        <td><b>Image data format indicator:</b></td>
        <td align="right"><i>image&nbsp;data&nbsp;format&nbsp;indicator&nbsp;length</i></td>
        <td align="center">octet&nbsp;string</td>
        <td align="center">{octet&nbsp;string}</td>
    </tr>
    <tr>
        <td><b>Image data block count:</b></td>
        <td align="right"><i>block&nbsp;count&nbsp;size</i></td>
        <td align="center">uint{(<i>block&nbsp;count&nbsp;size</i>)&nbsp;&times&nbsp;8}</td>
        <td align="center">1&nbsp;&plus;&nbsp;{uint?}</td>
    </tr>
</table>


### Compression format and length

<table>
    <tr>
        <th align="center"></th>
        <th align="center">Octets</th>
        <th align="center">Type</th>
        <th align="center">Value</th>
    </tr>
    <tr>
        <td><b>Compression format indicator length:</b></td>
        <td align="right">1</td>
        <td align="center">uint8</td>
        <td align="center">1&nbsp;&plus;&nbsp;{uint8}</td>
    </tr>
    <tr>
        <td><b>Compression format indicator:</b></td>
        <td align="right"><i>compression&nbsp;format&nbsp;indicator&nbsp;length</i></td>
        <td align="center">octet&nbsp;string</td>
        <td align="center">{octet&nbsp;string}</td>
    </tr>
    <tr>
        <td><b>Compressed image data length:</b></td>
        <td align="right"><i>compression&nbsp;length&nbsp;size</i></td>
        <td align="center">uint{(<i>compression&nbsp;length&nbsp;size</i>)&nbsp;&times;&nbsp;8}</td>
        <td align="center">1&nbsp;&plus;&nbsp;{uint?}</td>
    </tr>
</table>


### Image data

<table>
    <tr>
        <th align="center">Octets</th>
        <th align="center">Type</th>
        <th align="center">Value</th>
    </tr>
    <tr>
        <td>if&nbsp;<i>compressed</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;<i>compressed&nbsp;image&nbsp;data&nbsp;length</i><br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;(<i>block&nbsp;count</i>)&nbsp;&times;&nbsp;(<i>block&nbsp;size</i>)</td>
        <td>if&nbsp;<i>compressed</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;octet string<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;block{(<i>block&nbsp;size</i>)&nbsp;&times;&nbsp;8} string</td>
        <td>if&nbsp;<i>compressed</i>&nbsp;then:<br>&nbsp;&nbsp;&nbsp;&nbsp;{octet string}<br>else:<br>&nbsp;&nbsp;&nbsp;&nbsp;{block? string}</td>
    </tr>
</table>
