1. AHB3/AHB-lite. Burst-length: undef,4,8,16. and single. all equations in bytes. no of beats - each beat:  (1 cycle data+ wait) - ALWAYS 1 LEVEL PIPELINE. BEAT LENGTH BL= 2*(2**HBURST [2:1]) for >1 = (2 ** (HBURST [2:1]+1)) for >1 = (1<< (HBURST [2:1]))<<(|HBURST[2:1])

2.  INCR = HBURST[0] , WRAP = !HBURST[0]. for beat_length 1 and INCR beath length shall be ignored

3. Burst total :  no of beat + starting address phase.

4. data/beat = (2** HSIZE) = (1<<HSIZE) //  2**HSIZE <= DATA_width must for data

5. total data TD = (1<<HSIZE) * BL. IN BL>1  case:  (1<<(HSIZE+HBURST [2:1]+1))

6. total length/no of cycle = 1 start + wait_states/idle/busy_states+no of beats (N)

7. Addr incr total 1KB address boundary - no cross - 1024 bytes max. can be smaller based on starting. 

8. start_addr[31:10] == end_addr[31:10] in a burst. for incr (start_addr[9:0] + TD - 1) <= 10'h3FF
   min address space for a slave 1 KB. ADDR[0][HSIZE-1:0] == '0 . must meet for start. for HSIZE>0. 

9. address[n] = address[n-1] + (1<<HSIZE) 
  

10. DW ={1,...,128} IN BYTES. byte lane HxDATA[FL:SL]. SL = ADDR[n][log2(DW)-1:0] : each lane 1 byte. fl = SL + (1<<HSIZE) -1  for all/any n

11. AHB2 - ERROR : 2 BIT : OKAY, ERROR, RETRY SPLIT.

12. preemption when extreme latency - re arbitration for pending.

13. wait state - extends the same-time address phase of next transfer.

14. HBURST - Burst type.( 0, 1: undef). Any incr - seq location. address is incr of prev.
    idle -1 addr phase - data from prev can continue no impact - okay response -0 wait must.

15. busy type - idle may come. busy type address -control of next already. transfer ignored by slave - okay response -0 wait must.

16. NONSEQ type - first transfer of bus or single transfer unrelated to previous tranfer. - 

17. SEQ: Addr determined by prev. eq.8 is valid from 2nd beat's address. control remains same throughout. 

18. SEQ:WRAP: WB= N * (1<<HSIZE) ; wrap_base = floor(start_addr / WB) * WB .. from 0 to WB-1 wrapping. 

    inc_address[n] = address[n-1] + (1<<HSIZE)    
    addr[n] = wrap_base + (inc_address- wrap_base) % WB
    start_addr unrestricted.

19. multi master case: if burst termination forced - rebuild of burst at next point onward after reacquire - this requirement not there in ahb-lite AMBA 3 but there in AHB2.

20. HPROT : 3-cacheable 2- bufferable 1-priviledged 0: data/op.

21. HTRANS impact: non existant address = default slave :idle/busy type -OKAY response. rest ERROR response. 

22. Bus master in either AHB-lite or aAMBA2 AHB never cancels a transaction that has started. 

23. ERROR example : write to read only location; access to secure space in nonsecure mode.

24. SPLIT/RETRY: 