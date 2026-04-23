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

24. SPLIT/RETRY: master retry in next grant-slave requesting grant on behalf of master(?)/ master keeps on retrying.

25. two cycle response.: 1st ERROR cycle: HRESP = ERROR, HREADY = 0
2nd ERROR cycle: HRESP = ERROR, HREADY = 1 

26. meaning clear if you think response is a state for the data line. and two times to prepare the master to cancel 1 stage pipeline.

27. Hready first sampled by master at cycle 2 end.

28. retry - arbiter continues normal priority scheme - split frees for all - but slave must tell back when data is available. master both same.

29. HMASTKLOCK - breaks pipeline for atomic processing. second phase same address - then idle

30. busy+nonseq or idle at end of bus.: only for undefined  incr. everything else seq must end.single-busy not allowed. idle or nonseq with non single hburst must before busy.

31. start end implicit - so type alone can determine. error response - master termination allowed, no termination also allowed. no rebuild required. slave design should be termination tolerant.

32. wait -> idle to non seq allowed. wait issued in response to previous nonseq or seq. but onlce nonseq within wait - must hold.

33. wait busy -> seq allowed : busy wait issued in response to previous nonseq or seq. once seq back - must hold. fixed length.

34. wait busy -> anytype allowed : busy wait issued in response to previous nonseq or seq. once anytime back on nowait - must hold.termination or continuation of burst.

35. idle to nonseq - during wait new addr - addr holds.

36. error - 2 cycle error - 2nd cycle begining new address can be put.

37. address deconding - HSEL to each servant based on address space.non existant address- default slave - nonseq/seq error response. idle/busy ok response.

38. HRESP 1 - error - must be two type of Hready - wait and then 1.
39. reccommendation max 16 wait states.  1 error sampling by master is enough to terminate by an idle transaction.
40. HADDR[K] -> SELECTOR 0 -> K-1 : 2**K diffterrent address means 2 **K bytes -> more widers K..N address works as selector. narrow slave on wide bus. - latch selector address with HREADY as enable.
- kinde of lane selection - and reverse lane selection.

  AHB3 lite  -> 2015 version B ->

1. HPROT[3] : Cacheable -> Modifiable.
    New signal/interface items
    HPROT[6:4]
    HNONSEC
    HEXCL
    HMASTER[3:0]
    HEXOKAY
    clarified HPROT[3:0]

New protocol/property items
    Extended_Memory_Types
    Secure_Transfers
    Endian
    Stable_Between_Clock
    Exclusive_Transfers

Atomicity, including single-copy atomicity size and multi-copy atomicity
    New interconnect/transfer guidance
    extra HMASTLOCK/IDLE detail
    Multiple Slave Select
    New extensibility mechanism
    User Signaling


2. locked transfer - after that idle recommendated - during idle last of lock will happen.

3. MPMC requires LOck. locked  transfer sequence - idle at start or end not recommended but permitted.

4.locked same slave address region. (issue B)

5. memory type table -
    HPROT[6:2] 
    0 - Device-nE
    1 - Device-E
    2 - Normal Non-cacheable Non-shareable
    18 - normal no cache shareable

    6 or 14 - write-thru no share.
    7 or 15 - write-back no share
    23 or 31 -  write-back share
    22 or 30 -  write-thru share.


Device memories - 
    Read data from final dest.
    no split transfers or merging of transfers.
    no prefetch or speculative read.
    writes no merge.
    same -master-slave pair : order read & write.
    HSIZE always same. 

    bursts broken into smaller bursts by idle/busy. but total number of SEQ+NONSEQ remains same between them.

    HPROT[2] can be toggled. Device-nE to Device-E and vice versa.

Device-nE specific  - write response must from final dest.

Device -E specific - write response from intermediary but observation by all masters 