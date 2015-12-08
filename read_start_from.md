### Read a file starting from specific spot

[1] the file looks like this, and required to read starting from "~A"
```
TRT  .ft     1450.0000                      : Start
STOP  .ft     16893.0000                     : Stop
STEP  .ft        1.0000                      : Step increment
NULL  .       -999.2500                      : Null value
~A DEPT         GR        ROP     T-TEMP
 1450.0000     3.3844   126.1655    88.3053
 1451.0000     3.9797   138.9070    88.4021
 1452.0000     5.5436   139.5880    88.3471
 1453.0000    11.3552   139.4229    88.3471
 1454.0000    18.4241   139.3315    88.3528
```
[2] find the line number where "~A" is located:
```bash
grep -n "~A" file_name.ext |cut -f1 -d:
```
e.g.
```bash
grep -n "~A" file_name.ext |cut -f1 -d:
5
```
[3] read the file starting from the line number, came as a result from [2]
```bash
tail -n+result_line_number file_name.ext
```
e.g.
```bash
tail -n+5 file_name.ext
~A DEPT         GR        ROP     T-TEMP
 1450.0000     3.3844   126.1655    88.3053
 1451.0000     3.9797   138.9070    88.4021
 1452.0000     5.5436   139.5880    88.3471
 1453.0000    11.3552   139.4229    88.3471
 1454.0000    18.4241   139.3315    88.3528
```
[4] combine all together 
```bash
tail -n+$(grep -n "~A" file_name.ext |cut -f1 -d:) file_name.ext
```
e.g.
```bash
tail -n+$(grep -n "~A" file_name.ext |cut -f1 -d:) file_name.ext
~A DEPT         GR        ROP     T-TEMP
 1450.0000     3.3844   126.1655    88.3053
 1451.0000     3.9797   138.9070    88.4021
 1452.0000     5.5436   139.5880    88.3471
 1453.0000    11.3552   139.4229    88.3471
 1454.0000    18.4241   139.3315    88.3528
```
[5] improvement: add loop to go over than one file
