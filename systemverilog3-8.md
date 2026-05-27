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
42. enum for a new type with a custom range of universe :  a set of integral named constants.  - encoding will be done by synthesizer. reference enumareted names not value (value can be encodedl later.
43. set of integral named constants - strongly typed - default encoding type int.
44. enum {....} variable; or typedef enum {} new_type;
45. enum integer {} .. is explicit and x,z allowed inside. and all assigned must leftmost one can be implicit.
46. leftmost assignment assumed 0 or explicit. increment then onward or explicit again.
47. whenever assumed, previous +1 value.
