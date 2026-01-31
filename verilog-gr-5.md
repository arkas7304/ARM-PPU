1. Now, we know the blocks and sequences how they are getting executed.
2. We know blocking assignment non blocking assignments of statements: prcoedural assignment. procedural continuous assignment assign/deassign, force release we have seen. 
3. Now lets delve deeper in assignments.
4. continuous assignment only to nets, constant bit select of net. part, indexed part. coactenation of above.
5. net declaration time assignment = lhs.
6. e.g. assign (strong1, pull0) mynet = enable ;
7. assign
data = (s == 0) ? bus0 : Zee, 
data = (s == 1) ? bus0 : Zee;

8. for teaching explain (page 70/100 of 1364-2005).
9. delay -explained : vector net can have  3 delays rhs (fallig:to zero ,turn-off: to z, rising)
10. continuous can have delay - each delta continuous gets triggered if the change happens. delta is from the change. net delay/ driver specific delay. 
11. vector delay in decl assignment only 1 delay.
12. delay delaying more than new change. rhs evaluated . rhs  value differs - crrently scheduled is descheduled  -> differ from current value  new prop event scheduled.
13. procedural assignment within procedures are triggered assignment - when the flow reaches the statement. rhs collected then.
14. variable decl assignment similar to initial.
15. cinstant number, string, paramete,(local/specify/param), non-real param bit-select, Net, Net bit-select, reg, integer, time or their part-select. real, realtime, array, non-real array bit-select, or function returns of any above type.
16. real expression not allowed: concatenate, modulus, case equality, bitwise, reduction. shift.
17. unary -> exp -> mult,div,mod -> sum,- -> shifts (3 >) -> logical compare -> logical equalities -> binary and -> binary xor xnor -> binary or -> logical and -> local or -> conditional operator -> concatenatin.
18. association left to righr " compartor only right to left.
19. higher precedence first. parenthesis changes it.
20. integer with no base - signed value of 2's complement. (tbt).
21. integer division -  min func - div 0 x - mod takes sign of first operand. (tbt)
22. power operand real - res real. verilog : undefined. first op 0 ^(-a) : (-a)^ (non integral).
23. no real - first op 0 ^(-a) :x - first op 0 ^(0) : 1
24. default unsigned : intgere, real signed. signed except real : 2's complement rep.
25. sign -> unsigned : bit storage same - interpretation diff.
26. examples (tbt).
27. relation : result scala value  0 when false - 1 if true. x,z any one -> result x
28. any 1 unsigned - small 0 extended and padded.
29. both signed - sign extended of smaller length.
30. remember elation is lower in precendence than arithmatic.
31. triple includes x and z bit wise equality. equality always bitwise.
32.  =, != , if x ,z comex result x.
33.  sogn extended when both signed. real - conversion to real.
34.  1,0,x for logical operator. intendes to work on 1,0 any intgerer is 1.
35.  bitwise again result 1,0,x for per bit. (xor,xnor, not, and, or)
36.  and, nand ,or , nor, xor,xnor reduction.
37.  >> << logical shift: vacated fill with 0.
38.  >>> <<< : left filled with 0 , right filled with sign bit if signed.
39.  op2 x or z - result knknown. it is always unsigned forced.
40.  inline conditional : 1 - expr2 0 - expr3 : x or z" : bit wise combination unknows becoming x.
41.  concatenation : unsized constant numbers shall not be allowed in concatenation.
42.  replication - this will not be lhs of any expression and not connected with output ports. replication literal only valid  interger number - can be parameterised. 0 replication alone within another concatenation  not allowed, {p{w}} replication format.
43. operand - whole, bitselect part select of vector. a function call is operand. array element is operand. array part select converted to vector. bot select x/z result x
44. real cannot have bit select.
45. big_vect[lsb_base_expr +: width_expr] downto little_vect[msb_base_expr +: width_expr]
 , vect[msb_expr:lsb_expr]
46. upto, big_vect[msb_base_expr -: width_expr] downto little_vect[lsb_base_expr -: width_expr] natural integer flow - non negative.  // variable part-select with fixed width

47. memeory- array address can be any integer expression. (the big thing - slowest refferred first. fastest last.
48. padding left for string with less data.
49. concatenation of strings hence creates problem is the string variable is padded.
50. \0 is 0 valued reg not "0".
51. (a:b:c) + (d:e:f) min : typ:max delay format.
52.  if result stores in larger reg carry bits are stored else - removed.
53.  


 mi
