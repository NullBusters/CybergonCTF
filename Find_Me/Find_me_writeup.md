## title: Find Me | 50 points | MISC | 139 Solves

**Resolver:** Yxzi

## description:

Find, spot and grab the flag.

## Solution:

We get a file with .xlsx extension, char 'x' in extension means that this exel document propably contains macro but its doesn't matter in this challange.

[22:53:11]:[yxzi@HACKERMAN]$ file Find_me.xlsx

Find_me.xlsx: Microsoft Excel 2007+

when we open this file in hex editor on the end of file we can see that file contains some xml elements / paths to files:

<p align="center">
    <img src="screenshoots/hex_view.png">
</p>

these paths to xml files means that this document its propably Office Open XML (OOXML) file format, and contains xml files which we can extract these by just using unzip command because OOXML are something like zip commpresed files

<code>
unzip -v Find_me.xlsx 
Archive:  Find_me.xlsx
 Length   Method    Size  Cmpr    Date    Time   CRC-32   Name
--------  ------  ------- ---- ---------- ----- --------  ----
    1304  Defl:S      356  73% 1980-01-01 00:00 ddde1812  [Content_Types].xml
     588  Defl:S      244  59% 1980-01-01 00:00 233055b5  _rels/.rels
    2294  Defl:S      903  61% 1980-01-01 00:00 13dae91c  xl/workbook.xml
     839  Defl:S      250  70% 1980-01-01 00:00 61a6a94a  xl/_rels/workbook.xml.rels
   12538  Defl:S     1805  86% 1980-01-01 00:00 6ce2ecbc  xl/worksheets/sheet1.xml
   12945  Defl:S     1892  85% 1980-01-01 00:00 a7309c94  xl/worksheets/sheet2.xml
    8390  Defl:S     1870  78% 1980-01-01 00:00 be1017c1  xl/theme/theme1.xml
    1865  Defl:S      737  61% 1980-01-01 00:00 b71f4582  xl/styles.xml
     284  Defl:S      220  23% 1980-01-01 00:00 c6fed2a0  xl/sharedStrings.xml
     621  Defl:S      334  46% 1980-01-01 00:00 9f22c942  docProps/core.xml
     812  Defl:S      397  51% 1980-01-01 00:00 5cca6cfe  docProps/app.xml
--------          -------  ---                            -------
   42480             9008  79%                            11 files
</code>

