(50 supreme correct any contradictory with 50)
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
31. intra assignment delay/event control is like lhs_proc_var <= (14) expression. regular (14) lhs_proc_var <= expression.

32. intra delays the assignment to lhs. but rhs evaluation before delay. regular - evaluation after the delay.
33. repeat can repeat the intraassignment delays.
34. a <= repeat(5) @(posedge clk) data;
35. block - sequential procedure begin end.
36. parallel block, fork-join. all statement concurrent in it.
37. seq block delay statement from prev statement execution time always cumulative.

38. pararllel block - delay value event counts from start of the block.

39. all variable in blocks static.

40. overlap - execution of next statement following block waits for block finish.

41. ACTIVE -> INACTIVE -> NON BLOCKING -> MONITOR -> FUTURE.

42. non blocking -> nonblocking assign event for current or future. 

43. update event. processes are sensitive to it. evaulation event evaulates it. Putting an event on queue - scheduling an event.
 
44. begin-end block - statements can be suspended but order shall not change. even non blocking same rule. only the value collected is what at trigger time event.

45. assign p = q;
initial begin
q = 1;
#1 q = 0;
$display(p);
end 
race between assign and initial 


46. another no determinism - active events taken off queue. statements without timing do not need to be executed as one.

47. suspend and schedule as pending active event in eventque. interleaving of process excetuion - no user control.

48. source elemet triggers assignment - continuous - only nets. port connection falls in this type. time 0 time also it is evaluated. 

49. procedural continuos assignment : active update event waiting to be added in event queue. deactivation removes from queue.

50. blocking w delay - rhs computed using current value - scheduled as future event. 0 delay inactive event in current time.

- next time process return (next if no delay) - completes the assignment - enables any update event. 

- process resume time values are used to determine target. not update the target wit the value itself.

51. non-blocking: updated value computed. schedules the update as nonblocking assign update vent.(0 in this timestep future event, or future). 

52.  


all construct of always block

38.  if (expr) begin end else if (expr) begin end else begin end. expr true /nonzero known value false (0,x,z)
39.  case (expr) {options: begin end ; ...} default[:] begin end endcase
40.  casex casez definitive result.
41.  bitlinegth must match - bitwise matching -  longest among expr and options wins - unsigned wins - all signed is signed.
42.   1,0,x,z separate matching by default , z becomes donot care - casez , x,z donot care -casex. in either expr or options. ? for literal number in casez case in options makes more convenient.
43.  when expression constant -option const expression/array : encoder. regular decoder.
44.  


SV updates:::

physical modelling - 
always_comb.
always latch.
always_ff


fork elevated to level of always - for ...join_any.

thread of execution concept for each initial , always fork block, 


 always_comb v/s always @*
 1. once at time 0 guranteed ; this waits.
 2. content of function updates - only arg of function.
 3. lhs inteferring prohibited. multiple process interference allowed.
 4. always_comb: blocking timing event controls, fork..join banned.

always_latch
if(ck) q <= d;

always_ff @(posedge clock iff reset == 0 or posedge reset) begin
r1 <= reset ? 0 : r2 + 1;
...
end

one event control, non blocking timing control. no interferrence.

processes - sensitive to updated events. all processes sensitive to it - but in arbitrary order.

evaluation events 

Pre-opned 
Pre-active
Active
Inactive
Pre-NBA
NBA
Post-NBA
Observed
Post-observed
Reactive
Re-inactive
Pre-postponed
Postponed (monitoring)


Observed Reactive, Re-inactive essentially new.


Pre-active-PreNBA, post NBA for PLI callbacks.

Post-observed : for PLI-callback control point.


The Active region holds current events being evaluated and can be processed in any order.


The Inactive region holds the events to be evaluated after all the active events are processed

#0 delay - process suspended - active to inactive - next inactive to active iteration enabled.

nonblocking - NBA reagion - schedule for current or late.