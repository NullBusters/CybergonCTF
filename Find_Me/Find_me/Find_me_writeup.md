## title: Find Me | 50 points | MISC | 139 Solves

**Resolver:** Yxzi

## description:

Find, spot and grab the flag.

## Solution:

We get a file with .xlsx extension, char 'x' in extension means that this exel document propably contains macro but its doesn't matter in this challange.

<code>[22:53:11]:[yxzi@HACKERMAN]$ file Find_me.xlsx
Find_me.xlsx: Microsoft Excel 2007+</code>

when we open this file in hex editor on the end of file we can see that file contains some xml elements / paths to files:

<code>00002da0  72 6b 73 68 65 65 74 73  2f 73 68 65 65 74 31 2e  |rksheets/sheet1.|
00002db0  78 6d 6c 50 4b 01 02 2d  00 14 00 06 00 08 00 00  |xmlPK..-........|
00002dc0  00 21 00 94 9c 30 a7 64  07 00 00 91 32 00 00 18  |.!...0.d....2...|
00002dd0  00 00 00 00 00 00 00 00  00 00 00 00 00 f3 13 00  |................|
00002de0  00 78 6c 2f 77 6f 72 6b  73 68 65 65 74 73 2f 73  |.xl/worksheets/s|
00002df0  68 65 65 74 32 2e 78 6d  6c 50 4b 01 02 2d 00 14  |heet2.xmlPK..-..|
00002e00  00 06 00 08 00 00 00 21  00 c1 17 10 be 4e 07 00  |.......!.....N..|
00002e10  00 c6 20 00 00 13 00 00  00 00 00 00 00 00 00 00  |.. .............|
00002e20  00 00 00 8d 1b 00 00 78  6c 2f 74 68 65 6d 65 2f  |.......xl/theme/|
00002e30  74 68 65 6d 65 31 2e 78  6d 6c 50 4b 01 02 2d 00  |theme1.xmlPK..-.|
00002e40  14 00 06 00 08 00 00 00  21 00 82 45 1f b7 e1 02  |........!..E....|
00002e50  00 00 49 07 00 00 0d 00  00 00 00 00 00 00 00 00  |..I.............|
00002e60  00 00 00 00 0c 23 00 00  78 6c 2f 73 74 79 6c 65  |.....#..xl/style|
00002e70  73 2e 78 6d 6c 50 4b 01  02 2d 00 14 00 06 00 08  |s.xmlPK..-......|
00002e80  00 00 00 21 00 a0 d2 fe  c6 dc 00 00 00 1c 01 00  |...!............|
00002e90  00 14 00 00 00 00 00 00  00 00 00 00 00 00 00 18  |................|
00002ea0  26 00 00 78 6c 2f 73 68  61 72 65 64 53 74 72 69  |&..xl/sharedStri|
00002eb0  6e 67 73 2e 78 6d 6c 50  4b 01 02 2d 00 14 00 06  |ngs.xmlPK..-....|
00002ec0  00 08 00 00 00 21 00 42  c9 22 9f 4e 01 00 00 6d  |.....!.B.".N...m|
00002ed0  02 00 00 11 00 00 00 00  00 00 00 00 00 00 00 00  |................|
00002ee0  00 26 27 00 00 64 6f 63  50 72 6f 70 73 2f 63 6f  |.&'..docProps/co|
00002ef0  72 65 2e 78 6d 6c 50 4b  01 02 2d 00 14 00 06 00  |re.xmlPK..-.....|
00002f00  08 00 00 00 21 00 fe 6c  ca 5c 8d 01 00 00 2c 03  |....!..l.\....,.|
00002f10  00 00 10 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
00002f20  ab 29 00 00 64 6f 63 50  72 6f 70 73 2f 61 70 70  |.)..docProps/app|
00002f30  2e 78 6d 6c 50 4b 05 06  00 00 00 00 0b 00 0b 00  |.xmlPK..........|
00002f40  c6 02 00 00 6e 2c 00 00  00 00                    |....n,....|</code>

these paths to xml files means that this document its propably Office Open XML (OOXML) file format, and contains xml files which we can extract these by just using unzip command because OOXML are something like zip commpresed files

<code>
[22:53:11]:[yxzi@HACKERMAN]$ unzip -v Find_me.xlsx
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


with -v we can list all files that are in this document, and by using 'unzip -qq Find_me.xlsx -d output' we can extract this files to external folder

flag is hide in "xl/sharedStrings.xml" file
