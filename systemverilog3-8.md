1. time literal - unsigned no /fp no time unit. unit -> s, ms, us, ns, ps,fs, step.
2. unsized literal - single bit owidth 1 - repeated to fill the size.
3. real literal 0 fixed point format. 1.2 and 2e10 both real literal.
4. time literal realtime:  (fp or integer literal with time unit)
5. string literal : "" enclosed - \v \f \a \x02 : sv special add. \ for any nonprintable char and specialchar.
6. string - multi line \ before new line char: new line ignore.
7. string literal ->  unpacked array of bytes - left justified. cast to array - same rule.
8. new string data type -> arbitrary length- packed array - 8's multiple bit size literal.
9. Array literal -> C initialiser - '{'{}}  ::  {{}}replicator allowed. outer of replicator is part of lietral operator in this case.
10. original '{'{4,5,4,5,4,5},'{4,5,4,5,4,5}} == '{'{3{4,5}},'{3{4,5}}}  : 4,5,4,5,4,5 replaced by 3{4,5} but existance of immediate '{} must. if already there no new req
11. '{'{3{4,5}},'{3{4,5}}} == '{2{'{3{4,5}}}}
12. no of different dimension = no of ' -
  a.   innermost elements - fastest dimension count. outer most slowest dimension count.
  b.   outermost single ', next no of ' =  count of slowest dimensions-> then next faster so on - till repatation allowed or last but one(fastest) dimension.
14. literal must have constant expression. must have type. prefix or casting/assignment. context only.
15.  array lietral may be dict as well. index or type as key.
16.  c data types but c: 4 bytes longint 8 bytes. float -> shortreal
17.  type system extension -> object and data type separated. data type used to form more data type - and  more .
18.  4 state data type logic. traditional but name and separated from object. 
19.  string, chandle, class - event entended.
20.  bit data types with 2 states. data types can be parameters to modules. 
21. shortint(2 byte), int(4 byte), longint(8 byte),byte: signed 2 state int, byte ascii, bit (user defined vector size, 1 bit each ).
22. reg, integer, time - as earlier. logic new - more generic. reg logic just academic difference.
23. integral:: integer types , packed array, packed struct, packed union, enum, time.
24. simple bit vector : 1-d packed bits array . integral but no structure , no multidimensional. but packed structure and multidimensional has equivalency and direct conversion mapping.
25. 4 state -> 2 state : 0 default. truncation MSBs - extension : MSbit dupplication.
26. signed- byte, shortint, int, integer, and longint. unsigned - bit, reg, logic.
27. void: new :: for function no return value.
28. Chandle for DPI (4.6)
29. string type : new - earlier only literal assigned to reg packed array of byte. includes old meaning as well.
30. string data type arbitray length -no truncation . 0 to N-1 numbering - 0 is first left most.. [0:N-1] mode. "" special.empty as well. indexing empty out-of-bound error.
31. string assignment to integral as earlier. integral to string requires cast. integral made length multiple of 8 by 0 padding to mSbits. then assigned.
32. string -> string : \0 ignored . empty or remaining literal.
33. ==,!= : string equality . but by bit eqality. (comparison) - {str1,str2,str3} , {n{str}} - no chacter literal because no dimension here just pure replication.
34. str[index] - earlier . str.method - any method which operates on it.
35. str.len() - length null 0 , str.putc(i,c) ith char replaced by c i<N only. getc. 
36. str.Toupper, str.Tolower|  Compare - Icompare(case insensitiv) | Substr (i,j) ith and jth included. i<j
37. atoi, atohex,atobin,atooct -written conversion to integer or else best effort stops when faulty.
38. Atoreal, itoa,hextoa,octtoa,bintoa,realtoa.
39. typedef (type) new_type_name.  (type) is an enumeration of new_type_name.
40. user defined type identifier same scoping rule - except hierarchical reference to type identifier not allowed. so interface through port need recalling of definition.
41. typedef enum/struct/union/class new_type_name:.
42. enum : subset range of universe :  a set of integral named constants. universe default integer  - encoding will be done by synthesizer. elements of unniverse : reference enumareted name, not value (value can be encoded later or assigned directly). code can use enumereted name.
43. set of integral named constants - strongly typed - default encoding type int.
44. enum {....} variable; or typedef enum {} new_type;
45. enum integer {} .. is explicit-type and x,z allowed inside. and all assigned must leftmost one can be implicit.
46. leftmost assignment assumed 0 or explicit. increment then onward or explicit again.
47. whenever assumed, previous +1 value. implicit integer canbe overridden by explicit.
48. enum [type] {}  the encoded value < max value for type (implicit or explicit).
49. subset element declaration option and its encoding meaning:
      a. sx; sx = C; sx[C]: shorthand for sx[0],sx[1]..sx[C-1]; sx[C:D] : same as before but starts with C and D inclusive, C<D;  sx[C]= A or s[C:D]=A : same as earlier only sx[0] or sx[C] gets value A and  continues.
     b. interstingly in same enume declaration {sx[C-1], sx[C:D]} is valid because first one sx[0] to sx[C-1] second on sx[C] to SX[D]. start value can be different.
50. value assignment increments till redefinition or reassignment and continues.
51. enum expanding its set - strongly typed - outside set must be converted to acceptable range by cast - or member of union.
52. the enumeration names themselves : used as constant thorughout the scope. encoded values transfer in elaboration time. All constant usage allowed. ALL MEANS ALL.
53. uniqueness, integral constant value explicit or elaboration dependent, auto incremented. all one to one mapping.
54. usage casting - first auto cast to base of the type (implicit int or explicit) - sx = Colors'(sx+1); int I I=C+sx;
55.  first,last, next(int unsigned N),prev(N) : returns enum Name(value elaboration time).
56.  operates on variable with the enum-ed type : variable current enumname/value marker. num: total number of the enum set. Name - enum name of the  variable's current enum name.
57.  struct/union [tagged]   [packed]. eg struct { bit [7:0] opcode; bit [23:0] addr; }IR;
58.  initialisation within struct:  during struct declaration typedef,  or the variable declarion time by '{'{}} type assignment. individual elements -initialised. variable assignment overrides.
59.  unpacked structure : member union and packed struct : individual initial values not allowed.
60.  packed struct whole arithmatic if possible. 1st member most significant. any member 4 state - full 4state.
61. packed structure - implicit array referencing - [N-1:0] . but real shorteal not allowed in packed struct union. neither unpacked arrays because they break the beauty of packedness.
62. packed union : packed array - integer data types.  all member same size must. multidimansion c style unified 1 d style. same 4 state overrides 2state.
63. so that referencing out of bound one member falls into next member automatically. byte ordering of machine independent. cstyle unified.
64. signed unsigned whole:  packed union or struct only.
65. tagged union - strong type checking. (32-35 page revisit )
66. class : expansion of union to packaging. inside elements class properties. can contain function which are method.
67. 
68. Unpacked struct or union can not be signed. 
69. singular type - except (unpacked struct/union/array). aggregate (unpacked struct/union/array) 
