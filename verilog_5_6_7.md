1. Namespace -2 global 1 local.
2. global - definitions and text macros.
3. definitions -- all modules and prim - module or prim can not be again used for module or prim.

4. text macro namespace - text macro - ` lead by this char.
5. subsequent text macro def overrides.
6. local name spaces - each blocks.
7. names in local are restricted to locals and sub local.  redefine attribute is legal.

8. block unction and task. - blocked name space.

9. module named space - module and primitive constructs.

10. generate block namespace

11. port name space - module, primitive function task. input output or inout.

12. specify name block space - attribute name space enclosed by * and *. only attribute name in attribute name space.

13.  f (operands, operators) is called expressions.

14. expression completes the meaning of operators. 

15. legal operand without operator also an expression.

16. constant evaulations are constant statements. canbe compiletime variable.

17. similar constant system function.

18. pure function - only input driven no side effect. constant system function can use pure functions only if any function needed.

19. operand .
    constant (inc real) ,string
    Parameter
    param (partselect -non real)
    Net , Net Partselect
    reg, integer time variable.
    reg, integer Part select.
    Array element. Array element partselect.
    real, realtime
    call to systemdefine userdefined function with return any of the above.
20. concatenation.
    Replication.
    Unary (+-)
    Arithmatic. (6) ** % is there
    
    Relational (4)
    LOGICAL (3, 4) : 4 equalit ies.
    bit wise (3, xor xnor)
    Reduction (3, 3) negation not part of any 3
    Logical shift, ARithmatic shift
    conditional ?:

21. operator allowed for real.
    unary, arithmatic(5), (% x)
    relational(4)
    logical (3)
    logical equality (2)
    conditional

22. moduls, concatenations. case equalitys, bitwise (5) reduction. shift/

23.  same row same precedence. left to right (except conditional - right to left). placement.

24. parenthese will break precendence.

25. 
    a. unary and reduction - 1, unary not and logical not
    b. power
    c. mul-div-mod
    d. +/- (binary)
    e. shifts.
    f. relational.
    g. equalities.
    h. &
    i. (xor xnor)
    j. or
    k. &&
    l. ||
    m. ?
    n. concatenations,

26. IntA = -'sd 12 / 3; // The result is -4. is different from IntA = -4'sd 12 / 3; // -4'sd12 is the negative of the 4-bit
is different from IntA = -'d 12 / 3; // The result is 1431655761.

27. signed ness changes by bit width that is the key.

28. Boolean shortin -circuting or masking concept is greater than precedence.

29. integer division - fractional towards zero truncate. div by 0 is x.

30. result of modulus - sign of first operand.

31. power operator -> real operand - real output.

32. 0** -a - undefined. -a ** b.c undefined  \0 ** 0 same.

33. power : 0** -a -> 'bx 0**0 =1.

34. c** -a becomes 0 mostly. 1 and -1 exception.

35. x or z -> result is x.

36. Arithmatic expression -> reg reg gets after full processing of expression.

39. (- 'sd 12 )  : 'sd 12 means storage is 1100 and size is 32 now interprest as signed which makes it  valued at 12.

40. shortciruiting always allowed.

41. result of expression shall be treated as unsigned unless reg is explicitly unsigned . -4'd12 doesnt mean how it is stored. 


42. - signed to unsigned reg ' 2's complement version corresponding to size and sign gets stored.

43. when expression is assigned to variable has supreme meaning 'sd denote a temp variable.

44. intA = -4'd12 / 3 is equivaluent to storing to 32 bit reg data type without sign transfer.  if size is not mentioned size will be assumed to the type that is 32.  


45. Based numbers are unsigned unless s is used. 

Expression size/sign are determined, then propagated to context-determined operands before the operator is applied (see Steps for evaluating an expression and Table 5-22 on operand sizing). That’s why the unary minus does not stay at 4 bits in these contexts.


46. need testing of verilog page 44 and 48.(tbd).

47. true:false::1:0 scalar value. unknown 1 bit x.

48. 1 unsigned  - both treated unsigned. smaller zero extended.

49. both signed - smaller sign extended.

50. 1 real - both compared as real. comparison between real.

51. arithmatic higher relational next.

52. equality lower - signed unsigned real same as above.

53. case - either 0 or 1 

54. && || logical conncectives - 1, 0 , x

55. unary logical negation - any non zero or true to 0 - 0 or false to 1.

56. bitwise - and,or shortcircuiting power -.

57. reduction operators - reduction, or, and, xor primary . iterative.

58. nand nor, xnor , reversal at the end.

59. shift op - left and right both filled by 0. arith matic shift replaced by significant sign bit - right shift.

60. right operand always unsigned. if x or z result x.

61. conditional operator - ternary operator.
conditional_expression ::=  expression1 ? { attribute_instance } expression2 : expression3

62. ? 0 or 1 evaluated expression shall be chosen - else x .

63. concatenation - unsized number not allowed.

64. replication - {4{w}}  {3{a, b}}  - if this is 0 it must not be alone in next level concatenation structure or next concatenation structure atleast 1 positive . non-negative, non-x and non-z constant expression - replucation constant

65. operand of replication shall be computed once then repeated.

66.  expressions containing replications shall not appear on the
left-hand side of an assignment and shall not be connected to output or inout ports.

67. OPERANDS:
    a. variable net or parameters. just name of it. all bits
    b. bitselect  or part-select -, reg integer, time or parameter.
    c. out of bound or undetermined bit select's op is x.
    d. msb_base_expr or lsb_base_expr + or - will follow the declared direction . big_vect[lsb_base_expr +: width_expr]
    e. integer expr. The lsb_base_expr can vary at run time. this mode has most variability. not the first form.
    f. dword[8*sel +: 8] : variable part select with fixed width is allowed.
68. Array and memory addressing.
    a. 

69. string - assignment :copy, compare : equality operators, concatenation: concatenation operators.

70. zeros resulting from padding and the original string characters (\0, ASCII NUL) : comparison treats same.

71. "" is "\0" and has a value 0.

72. (a:b:c) + (d:e:f) :  min:typ:max FOLLOWS vectors.

73. self-determined expression -

74. context-determined expression. RHS depends on itself and LHS.

75. multiplication can be least min width.

76. interim results shall take - size of the largest operand , including LHS. 

77. any operator drives the interim result.

78. input expression -> return the value of same size and value and the type.

79. expression type only on operands. No dependency LHS.

80. decimal numbers are signed. numbers alone.

81. based_numbers are unsigned except s notation. but signedness depeds on width as well(googly).

82. bitselect, part-select results are unsigned. even in case part-select refers the whole signed vectors.

83. concatenate results are unsigned. comparison. 

84. real to integer byt type cast -signed.

85. self-determined operand are determined by the operand itself. independent of remainder of expression.

86. non-self determined operand :
    a. real -> real result.
    b. unsigned -> unsigned result.
    c. all signed -> signed - specified otherwise.

87. steps .
    - expression size - first
    - then sign rule.
    (tbd)


90. Assignments -  continuous -> nets
    procedurals to variables - > variables can be reg or combinatuional instance. reg is register instance.

91. assign/deassign :: force/release - procedural but ? - in context of sim?

92. = : blocking and <= non-blocking/parallel.

93. continous assignment - model combinationallogic - without interconnection of  gate modules.

94. wire (strong1, pull0) net = enable; allowed. only once. - only one assignment as well.

95. multiple with multiple synthesis space.

96. continuous assignment - 
    assign (strong1, pull0) mynet = enable ;

    assign {carry_out, sum_out} = ina + inb + carry_in;
    
    tri
    assign  data = (s == 0) ? bus0 : Zee,
            data = (s == 1) ? bus1 : Zee,
            data = (s == 2) ? bus2 : Zee,
            data = (s == 3) ? bus3 : Zee;

97. rhs nonzero-> zero - falling delay.
    rhs  -> z : turn-off delay.
    rising delay otherwise.
    
98. delay value declared ->  net delay any assignment.

99. if it has assignment then delay is for assignment. vector - together

100.  rhs evaluated -> current schdeuled to lhs differs - current descheduled.

101. delay happens to latest rhs.

102. wire, wand, wor, tri, triand, trior, trireg, tri0, tri1.

103. 1st strength value to 1 second strength value to 0.

104. no specification - default strong1, strong0 : common sense.

105. both cant be highz.

106. always, function :: task initial. -> triggered assignment - triggers one after another.

107. variable declaration assignment. -> special procedural case -> initial value -> (verif or automation/compile time).

108. variable declaration assignment ot ayyay not allowed.

109. list_of_variable_identifiers -> 

110. gate - switch. - primitives - 14:12

111. no continuous assignment equivalent - bidir transfer gate

112. primitive keyword - drive strength - prop delay - identifier/instance name - range:array  - terminal connections.

113. and, nand, nor, or, xnor, xor

114. buf, not, buif0, bufif1, notif0, notif1, pulldown, pullup.

115. cmos, nmos, pmos, rcmos, rnmos, rpmos.

116. rtran, rtranif0, rtranif1, tran, tranif0, tranif1.

117. 113 & 114 : drive strength valid. both (strength0 , strength1)

118. pullup : strength1 , pulldown : strength0. optional

119. strength1: ( supply1, strong1, pull1, weak1) : same for 0.

120. (highz0, highz1)  - invalid.

121. 



