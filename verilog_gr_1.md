0x60 - ` this is not ' 
celldefine -endcelldefine -
    : PLI routines specifics - any number of pair.
    : tags modules - as cell for PLI.
    : recommended outside module def.
y

default_nettype [wire|tri|tri0|tri1|wand|triand|wor|trior|trireg|uwire|none] 

default:: y : wire : none - forces explicit wire declaration.

define undef : MACRO - name reuse - but with char - anywhere - arguments - compiler directive x - they are predefined macro. \ driven addition of newline readability.
              macroname<nospace>(arg1, arg2) 
              // is never part of replacement text
              use - required argument matching. space after name 
              scope everywhere.
              split accross string not allowed

              no repetation reduction in macro body.


compiler directive - normal keywords - identifiers - identifier being compiler diirective. - text macro ne.
text macro names reuse normal identifier - latest def only.



undef before define again - 

ifdef -else elsif endif ifndef.

resetall - not allowed within module or UDP

line - for tracking original before preprocessing. filename based - number is set following the directive. - no comment in line command. number pos int. filename full or relative path. level 0 1 2


timescale - resetall impacts - makes sim specific.+ -all modules timescale must.

time_unit - measurement / precesion rounding. smallest of all precisions described commands the sim. `timescale 1 ns / 1 ps ok . time unit actsas multiplier. `timescale 1 ns / 10 ns illegal.


unconnected_drive - nounconnected_drive : all unconnected inputs are pulled . pull1 pull0.  outside module declaration.


pragma pragma_name [expression]- talk to implementation 





include     - insert the content in the files - not linking.

filename - full or relative path - nesting level at least 15


map and configuration - 

1. config endconfig : map file.

2. no config - libraries searched - declaration order - first one wins from map file. library command.


3. CLAUSE13.2.1: ALL TOOL MUST PROVIDE MAP FILE MECHANISM. E.G. lib.map

4. CLAUSE13.2.1: all file_path_spec relative to lib.map not tool home.

5. LIBRARY IDENTIFIER file_path_spec. unmatched files with file_path_spec goes to "work" library.

6. Command line mapping overrides lib.map. explicit config.

7. cell name refound - LAST cell separate-compile model. single compile - warning.

8. include other lib.map - include purpose - insert content. e.g. vendor local map - included by user relatively.

9. cell definition : during parsing/compiling: containing files searched - mapping found - goes to library mapped.

10. configure::considered as top: binding => design statement. only one per config. binding  specific library.cell or library containing this config.(?)

11. but multiple parallel. cells themselves not config but just binding. name may match between cells and config.

11. design statement before any config rule.

12. default -  from bound top : top down all modules:: whoever doesnt have specific . only once.  
13. instance <elaborated hier name> :: expnasion clause. top defined in  10. e.g. instance bot.a1 liblist lib3;

14. cell library.cell name :: expansion clause. this exapnsion can not be generic liblist expansion when library is mentioned.

15. Cell_clause :: cell foo use gateLib.foo; selects foo from default library.

16. expnasion clause => liblist <list of lib> - cells are searched for binding with instance in instance clause or default.

17. if empty or no library list then library:: "cell instantiating the unbound instance". 

18. cell <>  use <config name>  ||  instance <> use  <config name>

19. cell <>  use <instance name> ||  instance <> use  <cell name>

20. use doesnt modify library list and depends upon. ::config is used for it if name conflicts with module name.

21. lib.cell library name missing - parent cell defines the lib.

22. use clause breaks instance's module name and actual bound cell name same requirement.

23. instance top.a1.foo use lib1.foo:config; design stament of that config foo determines actual binding. then downward that config.

24.  instance top.bot use lib1.bot:config; next instance top.bot.a1 liblist lib4 - wont be accepted because that's a different config and hierarchy.


25. config: file based - all files together . another way precompiled one by one  then referenced/elaborated.

26. model 1: cell and library mapping regardless used - binding as encountered. library objects need not persists between runs.

27. model 2. single pass - only find top(s) - go down hierarchy - binding rule first - then the files found from library linking.

28. model 3: library cells are there first - compilation pre compiled.top(s) and configurations in the second pass. 

29. config source description file on the command line : single-pass. 

30. config itself precompiled in multi pass.

31. different library both maps same file. the first mapping found for a module will use that cell.

32. instance top.a2 liblist aLib; all descendent of top will be with aLib.

33. top.a2 - work.cfg5:config where as multi switching.
34. file cannot match multiple library under multiple mapping.
 
Hierarchy:

1. Verilog HDL : higher module - instance : binds to selected cell. default binding search : instance time module name and cell name.

2. Higher level module becomes cell - may be used for another instance binding - itself becoming a lower module.

3. { attribute_instance } module <module_name>  #(parameters) (ports,);|[{(list of ports);} {port_refs;}]  endmodule

4. ordered list - ports -optional anyway - but conveys key connection like circuits.

5. ports declared - name can not be reused/redeclared.

6. top - as discussed -compilation and configuration decides - no instantiation not even implicit rejected ones.

7. instantiation - one unique occurance/placement of cell inside the whole design/top. multiple times requires multiple instantiation.

8. instantiation syntax : module_name #(param_assign) instance_name (port_assign); 

9. adv topic: ranged spec for instance_name - allows for array operation on module. one or more in single statement.

10. port_assign : list_of_port_connections : ordered method - order of declaration reigns.

11. connection - higher module side items - can be higher module's port, net, variable, or null/blank.

12. named port_assign : .port_declared_in_lower_module(connection){,.. }

13. e.g. ff2(.qbar(out2), .clear(in2), .preset(in1), .q());

14. parametere delarartion : parameter_port_list or module_item. either both , none.

15. type-range spec. 
        a.  decl:no type- no range - connection type & range.
        b.  decl:range-no type - range & unsigned - connection converts.
        c.  decl:type-no range - type & connection converts - signed param takes range of the final connection value.
        d.  decl: signed type & range - connection converts rigidly. 

16. 2 way of param connection defparam  and instantiation. defparam gets priority.

17. instantiation 2 types: ordered , by name. either method. mix banned

18. defparam within a module - no change above it. within a generate block no change outside it - lower scope/higher scope. only downward scope. not even parallel scope of same generate loop.

19. RHS - constant expression - number and reference only to other accessible parameters only. elaboration time constants.

20. defparam last assignment wins. but multiple source file behavior undefined - tool dependent.

21. defparam access - named block, task, function. second parameter updated - dependent : carries forward.

22. no skip over in order, blank possible. default value 

23. local param not overriddable, but inheritable.

24. param_assign : by name - .param_name (connection) {, .param_name (connection)}

25. parameter dependent on another -> second param update will always trigger update. no 

26. ports - only interaction of any digital design.

27. decl of ports - list of ports. 
    a. simple or escaped identifier
    b. bit-select , part select of a vector from module.
    c. concatenation - above.

28. port expression - optional - only float - restriction no repeat deinition.

29. in, out, inout - each port_identifier in a port_expr - in list of port. this part is in body.

30. only port_expr - implicit port.

31. [inout|output|input] [ net_type ] [ signed ] [ range ] list_of_port_identifiers

32. output output_var_type. or output reg : another 2 options for output.

33. net/variable type etc makes complete - no further decl allowed. so further info decl also error.

34. std-2005 min of max port no - 256.

35. verilog restriction - only vector port - no array of ports. implicit treated unsigned.

36. list_of_ports v/s list_of_port_decls : 2nd every thing at once no further decl.

35. port_reference in this style not allowed. bit-select, part-select, concatenation, split ports can not be identifiers themselves.

36. however simple vector still allowed.

37. connection - ordered list: inst_port_expr & decl_ports. ordered placement of inst_port_expr(connection).

38. .port_name (connection) {, .port_name (connection)};

39. port_expr - simple identifier valid. no mixing with prev type.

40. Multiple instance of same port not allowed. order irrelvant.

41. verilog - real type not allowed in port - $realtobits , $bitstoreal - one option.

42. ports - must result in - structural net expr.

43. input decl - but used as output tool may decide to coerce inout or warning.

44. input/input - verilog only net.

45. source -> sink. : continuous assignment type.

46. no strength reduction transistor - for inout..

47. scalar, vector, constant-bit select of vector, part-select, concatenation of above.

48. verilog restrictions : variables, any other expr as above.

49. uwire merge - warning if not merge.

50. both side - becomes same type - type by table.

51. chosen is domination, loser dominated. resulting simulated net - collapsed net.

"Internal
net"	External net								
"wire,
tri"	"wand,
triand"	"wor,
trior "	trireg 	tri0 	tri1 	uwire 	supply0 	supply1	
wire, tri 	ext 	ext 	ext 	ext 	ext 	ext 	ext 	ext 	ext
wand, triand 	int 	ext 	"ext
warn"	"ext
warn"	"ext
warn"	"ext
warn"	"ext
warn"	ext 	ext
wor, trior 	int 	"ext
warn"	ext 	"ext
warn"	"ext
warn"	"ext
warn"	"ext
warn"	ext 	ext
trireg 	int 	"ext
warn"	"ext
warn"	ext 	ext 	ext 	"ext
warn"	ext 	ext
tri0 	int 	"ext
warn"	"ext
warn"	int 	ext 	"ext
warn"	"ext
warn"	ext 	ext
tri1 	int 	"ext
warn"	"ext
warn"	int 	"ext
warn"	ext 	"ext
warn"	ext 	ext
uwire 	int 	"int
warn"	"int
warn"	"int
warn"	"int
warn"	"int
warn"	ext 	ext 	ext
supply0 	int 	int 	int 	int 	int 	int 	int 	ext 	ext warn
supply1 	int 	int 	int 	int 	int 	int 	int 	ext warn 	ext


53. if equal then external. trireg results any strength.

54. all rules same as assignment. signed key word must for declaration to be processed as signed.

55. generate block - short details - choose between multiple choice to be placed. or array of iteration of placement.

56. system verilog add nested module declaration - making the module available only locally.

57. local namespace available to nested modules.

58. system verilog adds Extern modules . just the file gets compiled separately - linkage later.

59. extern accepts .* for ports connection.

60. sv allows variable - any allowed data type , array struct , union, event, interface. keyword var as well.

61. sv:: first port no type no direction - verilog 95 style must.

62. sv:: first port kind or data type - no dir - default inout. if dir but no type - wire type. 'default_nettype.

63. sv:: further ports -  dir inherited from prev. type wire/default.output port type depens on data_type syntax.

64.  list_of_port_expr (latest) expands with assignment itself while declaration. it clarifies internal association directly.
module mymod (
output .P1(r[3:0]),
output .P2(r[7:4]),
ref .Y(x),
input bit R );
logic [7:0] r;
int x;
...
endmodule


65. positional port connections - verilog & sv. ordered.

66.  named : verilog & sv. , size mismatch must be reported.

67. sv implicit instantiation - when name and type both match remove (xx). this can be mixed with named.

68. dissimilar error - when if named its just warning.

69. implicit .* - implicit all - .* can be used for whatever port matches 67.

70. any type passthourghable goes through.

71. ref qualifier. - shared variable behavior.

72. variable declared no assignmet - illegal.  

73. inout - no variable data type.

74. wire input float z, 

75. sv:: special: unpacked array - same unpacked dim - same geometry. else error.

76. geometry may take array of sub-instance partly - but geometry must remain same over all. child c[8][4](o,i);

77. sv:: packed array - each instance part select - arranged - in each loop and order. 

78. generate constructs: parameter driven choice ability. all construct allowed. no port param declarion or specify bloc, or specparam.

79. loop generate, if-generate, case-generate. key word generate.

80. elaboration time after parameter parsing. but vanish after that. unlike actual ifelse.

81. constant expression, deterministic at elab time. must.

82. 0 or more instance of the whole block. scope - module scope. hierarchy similarly new. but has access to all available in higher module.

83. generate - block exclusive items hierarchicahly accesible in runtime/simtime.

84. generate endgenerate. no nesting of region.

85. loop - n times instantiation of the block - n genvar.

86. genvar integer - during elaboration only. vanishes after elaboration.

87. initialization and iteration assignment - same genvar must. init must not refer loop index var on rhs.

88. implicit localparam integer- same name and type for loop index variable. elaboration time loop index value.

89. two nested loop same genvar not possible - as implicit integer is having same name.

90. named block or unamed block. but hierarchy of scope guranteed. irrespective of separate begin end.

91. named - array of size of max loop count. decl of array of generate block instances. sparse array. genvar need not be contiguous.

92. even if 0 loop arrayof inst declared.

93. not named: hierarchical name outside generate block hierarchy not possible.

94. as usual no name conflict with any other decl.

95. loop must terminated. genvar can not be x or z.

96. array of instance - just after range spec. 2 const [lhi:rhi] lhi< rhi  possible. equal means 1 

97. continuous range- instance identifier must - no separate decl - just instance time put array.

98. terminal connections :
    1. port expr bit-l compared - terminal connection bitl mapped. part select mapp starting with rhi.
    2. full geometry - too many or too few total is error.

99. e.g. dffn #(M) p[1:N] ({out, t}, {t, in}, clk) ; wire [M*(N-1):1] t; MxN pipeline.
    process 

100. serial t(M*(N-1) -1 : M*(N-2)) -> P(1).


101. GENEVAR gets appended in name by begin:name end format. 

102. this is c type {} equivalent.

103. conditional generate - at most one block. can be 0.

104. one item one line begin not required.

105. same name of a constructr in same condition tree- not others(even if others not selected after elab).

106. name clashing with other decl - even not selected not allowed.

107. not named - only hierarchy within it can reach decls using hierarchichal structure.

108. condition generate block (can be one among many alternative) - only one item - and that also is a conditional generate block - also no begin/end surrounding - then not a separate scope. directly nested. same scope as outer construct - same name , and name rule clash check of outer construct.

109. if-else-if , case can be nmixed.

110. Conditional instantion of parameter - making recursion instantiation.

111. elaborator shall assign name. code can not refer this. genblk<n>.

112. each node separate scope. idetifier only once in any scope.

113. . -separator . escaped identifier followed by ws and . exceptional escaped identifer case.

114. top of hierarchy - hierarchy search algo.

115. objects - automatic tasks, func - not accessible. unnamed genblock. - downward ierarchy can access it.

116. names - instance-array (gen block or otherwise) - [constant expression after elab] - instance select 

117. multiple instance treating together -not possible when it is middle of the hierarchy - only when last possible . (sv will deviate from it bcs of struct union etc).

118. simple_identifier ::= [ a-zA-Z_ ] { [ a-zA-Z0-9_$ ] } - start alpha or _ char atleast one char - no space.

119. full hierarchichal - any level if full path is known (path resolution rule in v). this is before elaboration naming - hence implicit reference not allowed.

120. name of higher level module or its instance name.

121. task, func, named blocks - look in enclosing till root found. only enclosing module not instances.
because you do not gurantee how many insatnces
121. upward_name_reference ::=
module_identifier.item_name.

122. scope_name.item_name - instance/ gen block.
    1. resolution - search in current scope as child element - not -> look in enclosing scope ->not -> repeat. (not crossing module boundary)
    2. search in current scope - not -> look in enclosing scope -> somewhere found -> then onward downward inst ref.

    3.1 ends in not found when module outermost scope is hit. look there  
        a. found - then onward downward inst ref.
        b. else - go up the hierarchy.

123. identifier one item/scope. exceptional conditional gen construct - because it is guranted wihout/before elab.

124. non hierarchichal reference - declaration locally or higher node/module in same branch. search automatically happens upward. local name overrides because search happens locally.

125. variable search can not cross module boundary during search.

126. task,function, named block/genblock search will continue in higher module in branch until found. port crossover not necessary. 

127. instance name is given preference if name clashes at any level.

128. so for downward ref - first item must be found at same level.

129. parsing -> elab -> sim/modelsynth.

130. elab module binding, parameter dissolution generate building.

131. defparam can trigger elab rebuild and loop - hence order must be there. because defparam can be any where.

132. starting points -> below hierarchy expanded. all parameter and available defparam statements.
     2.defparam inside hierarchy below generate can not affect higher so no worry. only twist is upper defparam.

     3. revisit all generate whenever newer higher up is added and newer def param is encountered.

133. some defparam during parsing ->  In order to cause the error, there has to be a named generate block that
has the same name as one of the scopes in its full hierarchical name. Furthermore, there have to be two
instances with the same name, one in the generate block and one in the other scope with the same name as
the generate block. Then, inside these instances there have to be parameters with the same name. If this
problem occurs, it can be easily fixed by changing the name of the generate block.


 tldr - defparam statement itself getting affected due to hierarchichal param ref - revisit of hierarchy never ends.


134. sv:: compilation unit . compilation scope, $unit.

135. together or each on its own compilation unit - tool shall provide method. `include always included

136. compilation unit will grow : no incomplete decl.

137. compiler directive resets between units.

138. sv:: compilation unit is searched before instance higher hierarchy as seen in verilog.

139. $unit is like a package in that sense.

140. $root is defined top. 

141. package scope : top level module name and primitives scope.

142. no process allowed. wire aac =1; not allowed.

143. ITEM within package has no hierarchichal ref.

144. class scope direct porting - no import statement. ComplexPkg::Complex cout = ComplexPkg::mul(a, b);

145. import package_import_item { , package_import_item } ;

146. explicit illegal, if the identifier is redefined in the same scope. or imported from another.

147. wild card import - makes only visible - actual import happens when reference first time.

148. wild card clash from another package - undefined error if used. redeclaration treated as first declaration.

149. such problem doesnt happen with class style ref.

150. 
 



