{toc}

## Basic Operation
* 5 * 2 + 4 =>  20 - Right to left
* \v => to check variable names
## Atoms - singluar entity
* It has a specific data type - this could be integer, float, character, symbol, etc.
* To force the type, we specify the type as a single letter after the atom. Lke a:1 (no forced type. 64 bit long)
a:5f. 
* type 5f => -7h => - tells atom, 7 for float

char | rep | num rep  | name | size (byte) | example 
---- | --- | ---      | ---  |  ---        |   ---
b |1 |boolean |1 |1b
g |2 |guid |16 |
x |4 |byte |1| 0x01
h |5 |short| 2 |32h
i |6 |int |4 | 12i
j |7 |long |8 |22
e |8 |real |4 |3.1e
f |9 |float |8 |1.234
c |10 |char | 1 |“c”
s |11 |symbol | *| \`a
p |12 |timestamp| 8 |2013.06.04D16:10:31.795334000
m |13 |month |4| 2012.03m
d |14 |date |4 |2011.01.01
z |15 |datetime | 8 |2013.06.04T16:11:24.635
n |16 |timespan |8 |13:12:15.012365478
u |17 |minute |4 |12:30
v |18 |second |4| 11:12:30
t |19| time| |4| 11:20:30.123

* .z.d => current date .z.t => current time
*  date stored as 4 byte signed integer and is denoted by yyyy.mm.dd
``` q)2000.01.01=0 => 1b ```
* Implicit type promotion: ```3i+3h => 6i /- promote short to int``` or ```3e+3f => 6f /- real to float ```
* Implicit bool promotion: ``` q) if[count (); show "some text"] /- counts() is count empty list => 0 ```
* Changing types of items - casting **($)**
  - new type $ object to change
    - `int$5h =>5i /- named rep or 6$5h =>5i /- number rep or "i"$5h => 5i /- char rep 
    - "I" $ "4" /- from a string
  - To cast to a string, we use the keyword string
    - string `text => "text" or string 1234 => "1234"
 
## List - collection of atoms
```
q) l1:til 5 => 0 1 2 3 4 
q) l1 * 5 => 0 5 10 15 20
q) l1 > 3 => 00011b
q) type l1 => 7h (note it is +ve denoting list)
q) type each l1 => -6 -6 -6 -6 -6h
==
q) emptyList:() => type emptyList => 0h
q) emptyListWithType:`int$() => type emptyListWithType => 6h
==
q) mixedTypeList: (100i;200h;300j;400e) => 0h | type each mixedTypeList => -6 -5 -7h -8h
== Equal and matches ==
q) l1: (100i;200i;300i;400i) | l2: (100i;200h;300j;400e)
q) l1 ~ l1 => 0h (matches => no)
q) l1 = l2 => 1111h (NOTE: = considers just the value not datatype)
== Singleton list ==
q) enlist 100i => ,100
q)type enlist 100i => 6h
q)type each enlist 100i => ,-6h
== Nested list - depth level of 2 or more ==
q)(1;2;(3;4))
1
2
3 4
q)type (1;2;(3;4)) => 0h
== Use index ===
q) l1: 1 2 3 4 5 6 => l1[0] = 1 => l1[0, 3, 1] => 1 4 2
== Matrix ==
q)mm:(1 2 3;4 5 6;7 8 9)
q)mm
1 2 3
4 5 6
7 8 9
==Indexing at depth===
q)mm[0;] /take all from first row
    1 2 3
q)mm[;0] /take first item from all rows
    1 4 7
q)mm[1;1] /take second item from second row
     5
q)mm[2;10]  /returns null of proper type as column
     0N /index is out of range
q)mm[0;1]:12
q)mm
      1 12 3
      4 5 6
      7 8 9
```      
