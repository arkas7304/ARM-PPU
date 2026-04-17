1.  AHB3/AHB-lite. Burst-length: undef,4,8,16. and single.
2.  HBURST - Burst type.( 0, 1: undef). Any incr - seq location. address is incr of prev.
3. incr total 1KB address boundary - no cross
4. burst- no of beats - each beat:  (1 cycle data+ wait) : total :  no of beat + starting address phase.

5. total data = 2**(3 + HSIZE) * {no of beats = f(HBURST)}

6. 2**(3 + HSIZE) <= DATA_width :: must.

7. for byte : 2**(HSIZE) = BYTES.

8. ADDR[HSIZE-1:0] = '0

9. when 