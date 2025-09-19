1. SOURCE FILES -> stream of lexical tokens.
2. free format -> spaces and new line significance -  nothing other than token separators. 
    a. Exceptions -> escaped identifiers.
3. C O W S K I N 
4. Comment Operator Whitespace String Keywords Identifier Number
5. WS - Spaces/ Tabs/ newlines/formfeeds - ignored other than token separator.
6. blanks & tabs - significant characters in strings.

7. Operators -> 1,2,3 character sequences -> 




7. one-line comment -> //  -> block comment -> /* */. no nested block comment. one-line comment within any comment -> no meaning.

8. Unary operator - left to operand , binary - in between, conditional : two seprating three.

9. number ::= decimal|octal|binary|hex|real
   real ::= unsigned_number.unsigned_number | unsigned_number[.unsigned_number ] exp [sign] unsigned_number , exp ::= e|E

10. decimal_number ::= unsigned_number| [size] decimal_base unsigned_number|  [ size ] decimal_base x_digit { _ }| [ size ] decimal_base z_digit { _ }


11. all regular rest - [size] base value
    
    - binary_value ::= binary_digit { _ | binary_digit }
    - binary_base ::= '[s|S]b | '[s|S]B :: 
      SIGN : ' is (ASCII 0X27) :BASE FORMAT CHARACTER
    - no space in these
    : octal hex decimal 
    - sign ::= + | -
    - size ::= non_zero_unsigned_number

12. integer constant - binary decimal hexa octal constant.
13. size - exact no of bits after compile
14. second token base, 3rd token value-unsigned number
15. regular decimal number - compiled as signed integer.
16. base format : unsigned till s is declared.
17. +/- preceding - signed number.
18.  -4'df - stored as 10001 (2's complement, signed format) : 4'shf stored as 1111 but while reading or storing to other it becomes 10001.
19. x, unknown - z floating.  matches the size meant.
20. unsigned < size - left padding to 0.
21. leftmost bit (even x or z) left padding 
22. unsigned >size - truncated from left. (rollover)
23. unsized number atleast 32. MSB is extended. signed MSB repeated.
24. decimal either all x,z or it will not be present.
25. underscore _ for readability  anywhere in number/value other than first character. ignored in compilation.
26. 754-1985. IEEE real number. decimal atleast one digit each side.
27. real -> integer : nearest integer not truncation. rounded away from 0.
28. sequence of characters enclosed by "", contained on single line - no multi line. storing - sequence of unsigned integer connstants :: 8 bit AScii for each.
29. String variable - reg : width char count * 8 - same manipulation as unsigned 8 bits array.
30. width mismtahc - left most 0 padding - or left most truncated. left to right in sentence - left to right store.
31. \n - newline; \t, \\, \", \ddd character specifed in octal digits?
32. identifier - object name - simple name. - simple identifier - letter digits, dollar sign, _ .
32. 1st char not digit or $. case sensitive.
33. max length >=1024. error on exceeding max.
34. start \ : end white space (sp, tab newline) :: start and end not part of it. only as means of extending letters digit ...to any printable ascii.
35. Keywords - always lower - case sensitive. escape character makes it identifier.
36. COWSKIN - other than that $ starting system tasks - A feature for compiler -compiler must do. again not escaped.
37. Directive - clause 19 + vendor implementation. (` ASCI 0X60 ) starts directive. immidiate impact - always counter impact also immidiate.
38. Directives file crossing. Directives define compiler behavior.
39. Atrributes define tool behavior. more like compilers interpretation specific to the item.
40. Attribute_instance ::= (*attr_spec {,..} *)   attr_spec ::= attr_name [= constant_expression] attr_name::= identifier.
41. last attribute - for more than once.


42. variable = instance.
43. net data types - can means physical connection
44. net does not store a value - example trireg net - rather driver at the instant. - no driver connected - Z
45. trireg - previously driven value - meaning .
46. a name - delcared as a net, parameter or variable can not be redeclared.
47. language wise variable is storage it store one element to another. real wise store or not is different matter.
48. reg, time, integer data types - real and realtime init value 0.0
49. vectors - multibit - MSbit left most lsbit rightmost - indexing order immaterial.
50. max length of a vector >= 65536 .
51. modulo-2 arithmatic 2**n.
52. signed can be added. 

53. vectored or scalered : scalaered means bit select part select permitted/ vectored may allow. - may not.

54. Strength - Charge strength (trireg), Drive Strength .

55. Charge strength - trireg - small medium large.

56. Implicit declarations - 
    a. identifier - port expression - defalut net type assumed.
    b. scalar net of defalut net type - if in terminal list.
    c. continuous assignment - scalar net of default type should be assumed.
    d. tied to scope - shouldnt be declared already. 

57. Net types - wire, wand, wor, tri, triand, trior, tri0, tri1, trireg, supply0, supply1, uwire.

58. tri explores possibility of multiple drivers. same strength multiple source simulated as x. z weakest.

59. wor,wand/trior-trinad : previous but 0,1 forces as per the case.

60. tri reg :: driven state - 1,0,x any driver. capacitve - all driver z - capacitive strength small medium large.
- driving strength supply strong pull weak.

61. <skipped> tri-reg theories

62. reg - procedural assignment only. flipflop , reset-set and transparent latches. reg can definitely be combinational as well

63.  type ::= variable_identifier { dimension }| variable_identifier = constant_expression
dimension ::= (From A.2.5)
[ dimension_constant_expression : dimension_constant_expression ]

64. integer generally general-purpose variable - not hw reg unless used as such.

65. time - only timing implementations. $time system function.

66. time 64 , integer 32 atleast. lsb -bit 0 -unsigned. integer signed. 2's coplement results.

67. bit-select and part sleect allowed.

68. real exceptions - few operators, usage in range declaration - unavailable - initial must be 0.

69. realtime synonymous with real just used for time.

70. many operator on real number single-bit scalar. edge descriptors , bit-select, and usage as index during reference of other vectors.

71. real -> integer : rounding away from 0. -> real x,z treated as 0.

72.  registers -middle one [type range element]. the element can be reg or indexable but element is expandable.

73. in between is the registers' dimension. end ones are loose array.
74. group - elements of declared element type - multidimensional objects.
 delcared identifer -> after that -> element address range
75. each dimension one address range. -> expression :: indices of array -> constant integer expression.
76. 2**24 ELEMENT is minimum guranteed.
77. memory - one dimensional array of reg. remember array.

78. PARAMETERS : localparam - parameter :param.
79. "param" ::= parameter ([signed][range]/paramater_type) list_of_param assignments. 
80. Parameter_type ::= integer|real|realtime|time.
81. list_of_param_assignments - comma separated list, RHS constant expression. constant number or previous defined parameters.
82. module_items or module_parameter_port_list. port_list may never be overridden locally.
83. compilation time overiddable. different from default declaration permitted.
84. modification - defparam statement or instantiation value passing.
85. type and range - final value  passed overrides this always if nothing specified.
86. range spec - no type spec- declaration range unsigned. no overide.
87. type spec - no range spec - follows type spec for range - signed parameter range of final value overrides.
88. both specified - no override possible.
89. parameter no range spec - and either signed type or no type - implied range - lsb_c_ep equal to 0 msb_c_ep 1 less size of final paramter. (just fit).

90. if final param is unsized as well atleast 31 msb_c_ep. example parameter newconst = 4;

91. localparam - no defparam direct modification. or module instance.
92. localparam can inherit indirect pass throughs through expression and main parameters.
93. bit-Seletcs and part selects of localparam (not of type real) allowed.
94. Specify PARAMETERS - specparam -timing and delay values only
95. specify block - main module block.
96. specparam_assignment ::= specparam_identifier = constant_mintypmax_expression | pulse_control_specparam
97. pulse_control_specparam ::=
PATHPULSE$ = ( reject_limit_value [ , error_limit_value ] ) | PATHPULSE$specify_input_terminal_descriptor$specify_output_terminal_descriptor = ( reject_limit_value [ , error_limit_value ] )
limit_value = constant_mintypmax_expression 


98. specparam outside specify block - declared before reference.
99. constant expression any.
100. a specify parameter cannot be modified by code/language - but can be modified by SDF annotation.

101. speparam -> module param - not allowed.
102. range: no overridable - no range: overriddable.

103. Bit-select part-selet : allowed.

