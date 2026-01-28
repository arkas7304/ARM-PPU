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
19. lhs_proc_var evaulation : in blocking happens at control time. in non-blocking happens with rhs time. order of evale between lhs and rhs without timing control is undefined.
20.  lhs_proc_var <= (14) expression. in an if scope alone <= is required.
21.  
