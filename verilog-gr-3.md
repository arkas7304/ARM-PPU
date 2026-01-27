1. atomic module - called primitives - directly mapped to synth library/ tech library etc.
2. A code-base with only modules, hierarchies and then primitives called netlists.
3. Netlists can be taken directly for fabrication geometry design tool along with electrical models like udf sdc etc.
4. we know always and processes are like molecule. they can not be called inside a function or task.
5. now behavorial actual design.
6. Lowest conceptual element always, procedure. can have multiple nested function/task. but that's all. function and task in return can not have always procedure, module neither.

7. So function and task akin to electron/proton. No individual identity from physical sense. but gives individual or unique meaning to interactions/ properties.
8. func:
9. one sim time unit - one cloud in synth.
10. can not enable a task - task can enable a func.
11. atleast one input, no output or input allowed.
12. returns a value/expression/data type. single value lement - may be array.
13. function [ automatic ] [ function_range_or_type ] function_identifier ; function_item_declaration function_statement  endfunction
14. function [ automatic ] [ function_range_or_type ] function_identifier (function_port_list)  ; function_statement  endfunction
15. function_range_or_type : default scalar - real, integer, time, realtime, vector [signed optional]. type of the return value.
16. automatic - local item -no hierarchichal access in code from other scope- each call is new. invoked by use of hierarchical name alone.
17. begin and end block within function for better segregation.
18. implcicit return variable. i bit reg default.
19. definition - inits -> function result - return to internal var with same name as func.
20. no re-decl as usual. scope rules.
21. any expression which gets  to implicit or explicit rhs of an equal-to (implicit or explicit).
22. banned : #, @, or wait. - no task enablement - one input atleast - no output or inout. nonblocking assignment , procedural continuous assignment banned - event triggers banned.
23. In short pure K-MAP.
24. constant func - only elab time evaluation.
25.  const func - argument: elabed const expression. 
26.  no hierarchichal ref.
    -  nested func - all must be const func.   
    -  any system func allowed in const_expr. others banned.
    -  system tasks ignored.
    -  parameter used inside must be defined  before the use of invoking constant call.
    -  then all other idetifiers locally defined. - defparam impact is undefined. error permissible by tool.
    -  no const func in gen block.
    -  no const func used in const expression internally (const expression not assignment).

27. sv allows output input ref in arguments. default input: without mentioning first one direction defaults. but lates no mention means last one duplicated.

28. default type logic, array (non-vector) allowed as argument in sv.

29. modified func argument not allowed in event expr call.

30. default arg value.

30. begin end can be omitted in sv. return statement overrides name idetifier based assignment. return has expression

31. sv:: new return type void - void func are statements no expression. void'() on func call is discarded.- warning mr

32. sv:: return can be struct or union. function_name.identifier_name is member of this return value.

33. sv:: const func may call any system func  - may refer package scope parameters or $unit.

34. sv:: not allowed import DPI , arg as non-input, void func not allowed. default arg value must be const.

35. v:: arguements: by name, by position code writing - known till now.  both of these style is pass by value.

36. sv::default value new to sv. new by reference. by value still default mechanism. Copying arg in sbrouting area - automatic means local copy in each stack.

37. sv & v :: sub routine changes this local copy - not visible outside. if same arguments to multiple loss big time in sim - not much in synth.

38. sv:: by reference. pointer type - match must by same data type - no implicit conversion/ Casting.

39. sv:: ( ref byte packet [1000:1] ); - ref keyword for passing. for static func it becomes illegal.

40. sv:: any changes in this by one reflects in all - only variable can have this. 

41. sv:: situation of outdated reference may happen. array deleted the intended ref still working. no change visible outside.

42. sv :: ref dir - illegal. const ref - makes it read only.(error otherwise).

43. sv :: module level passing of ref is similar to inout.

44. a ref of an object handle :: changes to the object handle (for example,assigning a new object) &  modification of the contents of the object:: allowed.

45. sv:: default value - (int j = 0, int k, int data = 1);

46. absence of default value - input can not be blank for function.

47. taking in from left by default, skip requires ,, 

48. no arg , () is optional . 

49. illegal to omit the parenthesis in a directly recursive nonvoid function method call that is not hierarchically qualified.

50. sv:: import export from c code. (advance topic).

51. verilog only again. tasks default static -  task. task not called but enabled. task enabling statement passes arg.

52. verilog arg argument goes both way. any expression.

53. task return execution passes the value to output and inout argument.

54. task has events and control signals.

55. input, output, and inout type argument retain value between calls. output and inout must be valid lhs type of any procedural assignment.

56. static scope is limited to module - across module's different instance it becomes automatic.
57. staticness - all local variables.

58. task enablement : more than once. automatic tasks - non blocking assignment or procedural continuous statements variables not allowed. procedural continuous - or procedural force not allowed.

59. disable task: by its any hierarchichal name. 

60. disable task - all downward chain stops.

61. more than once enabled all activations of task disables.

62. self disablement of blocks. named block.

63. disable of loop block breaks - whatever the procedural block it gets disabled.

64. sv:: task default direction of arg input.  local variables within static be declared automatic. or static within automatic.

65. sv:: return added for task as well.