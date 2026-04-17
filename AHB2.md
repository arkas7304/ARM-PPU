1. AHB3/AHB-lite. Burst-length: undef,4,8,16. and single. all equations in bytes
2. HBURST - Burst type.( 0, 1: undef). Any incr - seq location. address is incr of prev.
3. incr total 1KB address boundary - no cross - 1024 bytes max. can be smaller based on starting. 

4. burst- no of beats - each beat:  (1 cycle data+ wait) : total :  no of beat + starting address phase.

5. total data = (2** HSIZE) * {no of beats = f(HBURST)}. 

6. 2**HSIZE <= DATA_width :: must. ADDR[HSIZE-1:0] == '0 . 

7. DW ={1,...,128} IN BYTES. byte lane HxDATA[FL:SL]. SL = ADDR[log2(DW)-1:0] : each lane 1 byte.

8. 

9. when 