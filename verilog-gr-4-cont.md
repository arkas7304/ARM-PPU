
1. verilog repeat . disable stamenet on block name can use for break;
2. sv:: break, continue, return irrespective of block name.
3. do..while - another c like loop structure added.
4. verilog : force overrides assign - force released assign takes over.
5. sv:: final block. - stat showing purpose.
statement_item ::= 
blocking_assignment ; 
| nonblocking_assignment ; 
| procedural_continuous_assignment ; 
| case_statement 
| conditional_statement 
| inc_or_dec_expression ; 
| subroutine_call_statement 
| disable_statement 
| event_trigger 
| loop_statement 
| jump_statement 
| par_block 
| procedural_timing_control_statement 
| seq_block 
|wait_statement 
| procedural_assertion_statement 
| clocking_drive ; 
| randsequence_statement 
| randcase_statement 
| expect_property_statement

6. assignment_operator ::= = | += | -= | *= | /= | %= | &= | |= | ^= | <<= | >>= | <<<= | >>>= 
7. unique if - exclusiveness - parallel evaulation rather than priority chain indicator.
8. priority if - forced priority.
9. warning for no else for both case. applies to full tree - same level.
10. case also priority unique.
11. unique illegal - if multiple match found.
12. inside ,  a ==?b  b includes x , z.
13. apttern matching (refer relation operator chapter).
14. do .. while. while condition evluated after the statement. as in verilog for first condition is checked then enters.
15. sv:: in place declaration accepted in init. this is automatic.multiple var can be inited , separated, multiple inc statement. all or none locally decl : init time.
16. sv:: foreach must enclose full list , with loop variables in dimensions addressed.
17. as in verilog. outer loops correspond to lower cardinality indexes.
18. When loop variables are used in expressions other than as indexes to the designated array, they are auto-cast into a type consistent with the type of index.
19. disable similar to continue when disable is performed on other block.
20. disable kills a task.
21. iff qualifies the trigger. it has pecrdence over or
