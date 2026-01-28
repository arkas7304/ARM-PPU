1. function task we can call within processes.
2. initial and alwasy activity start point.
3. all initials and always block concurrent to each other.
4. time zero starts all flow independently.

5. timing control creates delay once.

6. always construct restarts immidiately after completing the steps in next delta.
7. all line in always constructs happen sequentially blocking next statement/ not blocking next stament but in same delta.
8. procedural assignments - values to variable. triggered event like. flow within delta triggers.
9. reg, integer, time, real, realtime. : not whenever input operand changes value , but takes the value of input operand when flow reach there.
10. rhs expression evaluates to value. lhs receievs the value.
11. concatenation or nested part in lhs as well. whenever such partition possible on the lhs value.
12. blocking procedural assignments: blocks the next statement depending upon it.
13. blocking procedural assignments: does not prevent any statement that depends on it in a prallel block.
14. #delay, #(mintypmax), @hierachichal_even_identifier, @*, @ (pos/neg)edge expression, @ (expresssion or expression or...) :: or can be replaced with ,
15. 14 can be used as  lhs_proc_var = (14) expression. (dont confuse with cont and proc cont assignments)
16. This is the basic event control mechanism procedural non blocking statment with control.
17. non dependency - safe to use nonblocking - dependency shall be ignored.
18. actual procedural even schedule later. but think like this - at every trigger the value is collected.
19. lhs_proc_var evaulation :: in blocking happens at control time: in non-blocking happens with rhs time. order of evale between lhs and rhs without timing control is undefined.
20.  lhs_proc_var <= (14) expression. in an if scope alone <= is required.
21.  the non blocking: next statement event is not a build up from current statement's event but only on when then next-one itself ended last time.
22.  non-blocks -evaluates an schedules it for the end of delta - by this it achieves 21.
23.  however at the end of delta - the evaulated results will follow the order of the statements.
24.  initial begin
a <= #4 0;
a <= #4 1;
end
25. two different procedural block : same variable : blocking statement non-blockign statement - both inderminate order if collides in same delta.
26.  proc cont assign: assign forces final value at each delta. deassign removes that.
27.  proc cont assign: force almost same - difference  : nets as well variables: except part-select of vector variable/array. expression triggered force allowed.
28. #,@,wait 3 types. implicit @ (regular event). or explicit named event triggered from procedure. 
29. #: high impdence delay expr :0 neg: 2's complement large delay. specify parameters can come here. SDF can override these.
30. x,z treated as middle between 0,1 : x->z and viceversa no trigger.
31.
32.
33.
34.
35.
36.
37.
38.  if (expr) begin end else if (expr) begin end else begin end. expr true /nonzero known value false (0,x,z)
39.  case (expr) {options: begin end ; ...} default[:] begin end endcase
40.  casex casez definitive result.
41.  bitlinegth must match - bitwise matching -  longest among expr and options wins - unsigned wins - all signed is signed.
42.   1,0,x,z separate matching by default , z becomes donot care - casez , x,z donot care -casex. in either expr or options. ? for literal number in casez case in options makes more convenient.
43.  when expression constant -option const expression/array : encoder. regular decoder.
44.  
