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
69. Singular type - except (unpacked struct/union/array). aggregate (unpacked struct/union/array) 
70. casting = dest_type '(expression). static cast: compatible -> regular conversion.
71. signed'(x) -- 1d packed array. real type cast is rounded to ites meaning - function is there : bit representation
72. packed struct - 1st field MS ...unpacked ordering matters - and structure. packed to packed explicit cast not required.
73. casting is compile time - so elaboration time out of bound error it can not warn. $cast for that.
74. unpacked -  bitstream  a superset of unpacked and packed - all items having bits representation, 0 first index, etc MS. but here different size compile error.
75. array - 0 to N-1 in c . each element wise access in c. verilog left-b to right-b . vector - asignment together array not.
76. verilog to sv : vector becomes packed - array becomes unpacked - all are array.
77. packed arrays - multidimensional - guranteed contiguous sets of bits. 1d packed array vector.
78. packed array -signed - single vector signed - any individual unsigned -unless the type is signed defined. part-select unsigned.  atleast 2^16 bits size in total.
79. predefined integer type can not be element type. but bit signed [10:0] allowed. unpacked this restriction removed.
80. int Array[8][32] === int Array[0:7][0:31] - only for unpacked.
81. packed unpacked both A=B, A[i:j]= B[i:j] A[X+:c] =B[X+:c], equality operations.
82. unpacked array not allowed , A = 8’b11111111 (bit-stream), A+3.
83. unpacked signed - each individual element signed.assignment same dimensional structure. - packed array - vector - dimension not important - cross dimension size less assignments ok.
84. Index belonging to dimension - 1st to refer is slowest - right  of next to name then towards right then rollover - then 1st from left before name. just before name fastest. (page 44 or 60)
85. 1st referred rest not referred means - what is left that structure comes together 
86. bit [3:0] [7:0] joe [1:10];  joe[9] = joe[8] + 1 -> 8th [3:0] [7:0] joe  gets added with 1 and put in same of 9th.  [3:0] [7:0]  is packed so they can be treated 32 bits while adding.
87. reference  starts from slowest. always.- even when partial
88. typedef bit [1:5] bsix; bsix [1:10] foo5; - same for unpacked.
89. packed dimension portion - multiple different array for declaration - bit [7:0] [31:0] foo7 [1:5] [1:10], foo8 [0:255];
90. outof bound - no op write - uninitialised value for read guranted. warning /error not mandated by LRM.
91. part select - packed array - or integer array number down to 0.
92. slice - sv - extends beyond single element- unpacked array as well - unavailable in verilog beyond single element.
93. slice or part select of packed array - packed array - same uniformity.
94. size of part-select constant position can vary.
95. slice - apply to one dimension alone.however single index free to go with it.
96. Dynamic - only unpacked - size not predefine. needs new operator. adds or shrinks. size op - current size
97. assign to unpacked - same no of dimemsion - each dsame length - elements . left most to leftmost. irrespective of index no during assignments. dynmic -tonfro - fixed same cond.
98. array to func as arg - pass by value - array assignment condition because a copy going.
99. Associative array is dict from python.  declaration is for key type instead of size.
100. wild card key/index - index any integral -evaluate the integer with zeros. nonintegral illegal. 4 state invalid. unsigned. autocast to bit vector and then representing an integer. ordering numerical lowest to highest.
101. string index - all string unique - empty string included. lexographical ordering - most like pyhton dict.
102. class index - some class only that class. order deterministic but arbitray.
103. integer index -32 bit. signed.any integral.
104. signed packed array - as key, interpreted as integer - signed - ,fit to index size. signed numerical ordering.
105. unsigned packed array - as key, interpreted as integer - signed - ,fit to index size. signed numerical ordering.
106. invalid index - raning must in sim and default value returned/ write ignored - same principle followed in elab.
107. typedef struct as key - cond. equality operator satisfiability, relationnal operator defined and fixed at least for a single run.
108. num| delete ,exists | first , last , next ,prev for some function ref is pointer.
109. associative array - assignment - same index type same size type . same for arguments in function. associative array literal - '{index:value}  syntax .
110. Queues - variable size - homogenous element - ordered collection. ordered number 0 to $.
111. 1d unpacked array increasing decreasing size.  $ in size unpacked array becomes queue.
112. all like dynamic array - diff empty queue. mostly right most or left most op.
113. diff from dynamic array - conditions b>a for Q[a:b] else {} etc. push pop methods.
114. array manipulation method - with
115. Array locator - any unpacked array - return type is queue. - search for element /element-index that satisfy a given expression. find , find_index , find_first , find_first index, find_last, find_last_index.
116. e.g.  IA.find( x ) with ( x > 5 ) . if min, max, unique, unique_index  - may not need with if  > < == defined for element type. and with clause requires the type to be valid for same by default.
117. reverse, sort (with allowed), rsort(with allowed),  shuffle  -
118. array reduction - sum product and or xor ... with item operates as needed first.
119. iterator index querying - may need actual array index - in q = arr.find with ( item == item.index );  q = mem.find( x ) with ( x > mem2[x.index(1)][x.index(2)] );
120. verilog contants - literal -genvars paramaters,localparam, specparam. variable and nets.
121. variable - is extended like wire. reg replaced by logic - the commong name for variable now.
122. static  or automatic - in entry of scope and only to that scope - that means paricular register if synth is local temp only. static over ride of a variable in a scope with default automatic.
123. non-procedural context - automatic keyword itself is invalid. var keyword only allows absence of data type for explicit list of variable. absence of const is var.
124. const lifetime {datatype|type_decl|package import decl|virtual interfaxe| list of variable decl(regular item) }   : data declaration 
125. net_type [v|c] [vectored|scalar] data_type [delay3] listofnet                  : net declaration
126. constants : parameter|localparam|specparam|const.  - eaboratiion time all const.
127.  (const/parameter passing orverrdigin block) in instantiation. or defparam using hierarchichal path. constants  [data_type] l_p(list of param) or constants type list_of_type (e.g parameter type p2 = shortint )
128.  specparam_declaration ::= 
specparam [ packed_dimension ] list_of_specparam_assignments ; data_type includes sign and packed dimensions as well. list include unpacked dimensions as well. specparam assignment is minmax expresion others constant type.  type param can not be used with defparam.
129. compatibility with verilog - when no data type -> type determined by values passed.
130. rhs type - real or integral when not explcit. logic vector becomes centre.
131. inside generate scope specific localparam - highest priority. pramaeter name may be used but it is actually localparam when used here.(page 67)
132.  $ as a parameter value -> the parameter instead of $ wherever $ can be used.
133.  list of parameter - paramemeter derived from just previoius parameter in same list.
134.
