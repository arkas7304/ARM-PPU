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
25. 
