<div align="center">

## Radix sorter


</div>

### Description

This code is the second fastest way of sorting a table of values. The only faster way found yet is a variant of this method. Umm... What can I say? It's really fast. Once you understand the concept it isn't too hard to write it in ASM either.
 
### More Info
 
A table of values. Its size could be any number of values.

It returns the values in the list, sorted in ascending order.

This sort basically Requires that you at least temporarily double the memory size of

1.) The array containing the data to be sorted

2.) Any target arrays you have that need to be sorted with it.

HINT: If you are sorting things like polygons by their Z values, it is better to leave the polygons in one array and have 2 more. One should

contain their Z values, and one should contain a pointer to the triangle that a Z value is associated with. This way you only have to move 2

arrays around ( the one with the Z value and the target) and saves a lot of wavelength.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Kevin Hall\(Silence\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/kevin-hall-silence.md)
**Level**          |Unknown
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |VB 3\.0, VB 4\.0 \(16\-bit\), VB 4\.0 \(32\-bit\), VB 5\.0, VB 6\.0, ASP \(Active Server Pages\) 
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__1-1.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/kevin-hall-silence-radix-sorter__1-3080/archive/master.zip)





### Source Code

```
'$INCLUDE: 'directqb.bi'
'Radix sorting: YAY! If you haven't heard of this before, it's
'basically the best way to sort a set of values other than the
'optimized radix sort, and I'm not handing out my code for that
''basically, for a radix sort, you need to be able to look at bits,
'and since I don't know of any vb functions to check a bit, I use
'the directQB function DQBreadbit
'For the record, DQBreadbit returns -1 if the bit is set and 0 if it is 0
'number of values to be sorted
sortnum = 100
'sort0 is the array that contains the data to be sorted. This
'is the one disadvantage to the radix sort. You need another equal
'sized array.
Dim sort0(sortnum), sort1(sortnum)
Randomize Timer: Cls
'sort0 is the array to be sorted, sort1 is to assist
'fill it with random crap
For i = 0 To sortnum
 sort0(i) = Int(Rnd * 10000)
Next i
'go through the bits from least important to most important
For Bit = 0 To 15
 'set the pointers to the start of the two arrays
 tar0 = 0: tar1 = 0
 'go through each number and if the current bit being checked is set, put it
 'in the appropriate array
 For num = 0 To sortnum
  If DQBreadBit(sort0(num), Bit) Then sort1(tar1) = sort0(num): tar1 = tar1 + 1 Else sort0(tar0) = sort0(num): tar0 = tar0 + 1
 Next num
 'get the now partially sorted data all into one array (sort0)
 For Copy = 0 To tar1 - 1
  sort0(tar0 + Copy) = sort1(Copy)
 Next Copy
Next Bit
'now sort0 contains all of the values sorted in ascending order
'if there is a positive response to this, I think I'll make an ASM
'sub to do radix sorts. Anyways, in an asm radix sort, it's not
'uncommon to be able to sort 15000 values in less than a tenth of a
'second. The trick is that the amount of time the radix sort takes
'does not increase exponentially with the number of elements in the array.
```

