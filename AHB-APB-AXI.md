1.  APB2: P:CLK-RESETn-ADDR(MAX32)-SELx-EN-WR-WDATA(8/16/32)-RDATA(8/16/32)
2.  APB3(OO): P READY-extension. SLVERR 
3.  APB4(O): PPROT , PSTRB :: APB5 (C): PNSE PWAKEUP PAUSER PWUSER PRUSER PBUSER
4. APB2 : Write -> pos_edge: master ->sel l2h :en low: (addr,write,wdata valid already or next edge). next edge same with en l2h - next edge end sampled high but falls write happens. everyone falls.
5. APB3 pready if h2l in 2nd edge sampled low in 3rd stage enh2l doesnt happen till both en and pready == high.
6. APB2:READ -> same pwrite low this time but again maintains with addr and sel, end goes l2h in second edge. ideally data and ready goes valid and high and sampled in 3rd edge. APB3: READ ->   however if master sees in 3rd edge en==1 but ready==0 then continues till ready==1 also sampled and at that edge latch the valid data.
7. APB3: 3rd edge : SELx neednt go low if another transfer starts but then en must go low.
8. APB3:SLVERR: RECEIVED BY MASTER: SAMPLED ONLY IN 3RD EDGE.(no rigid restriction of data validity by spec). (optional but master must tie low in absence)
9. APB3 : ERR -> AXI RRESP BRESP :: AHB:HRESP.
10. APB4: for PSTRB[n]==1 PWDATA[(8n + 7):(8n)] valid :: read PSTRB[n]=0. completer input to be tied high when mismatch.(write)
11. APB4: PROT(0):: 0-normal/priviledge. PROT(1):: 0-secure/1-nonsecure. PROT(2):0-data/1-instr.
12. completer/slave with PROT may be incompitable for mismatched master.
13. APB5: NSE==1 SECURE BECOMES root and non-secure become realm. (property based)
14. requester with NSE incomplatible with mismatched master. reverse just tie low.
15. completer permitted wait for WAKEUP before ready - interface risk deadlock.
16. pwakeup if high already must not change between sel to ready high. sync to PCLK from reg..
17. APB master slave clock gating together cdc behind slave is just a recommendation.
18. PSEL,PWAKEUP- always valid. PREADY only valid - SEL & EN high. rdata,slverr,r/buser must give back valid in data phase.

19. Now - AHB3 AHBlite - en-sel vanishes - 1 stage pipeline - we have option now for burst - addressline folllow same 1 stage pipelining in burst sequence. so during data address can be next address.
20. HWRITE is tied to the address phase HREADy now for each data phase.
21. HREADY extension - 1 stage pipeline freezes - so next address phase extends as well.
22. HTRANS - 00: NO DATAPHASE- BUT ANYWAY invalid ADDRESS COMES - previous DATA appears - next cycle it sticks  - okay RESPONSE must from slave.
23. HTRANS - 01: Busy - only undef/INCR HBURST last transfer can be busy then idle or nonseq may follow - busy after atleast first NONSEQ  - next addr comes. and it will repeat address and other control will just repeat - that next one data (corresponding to present busy) is invalid. others : only between seq hence during wait when busy to seq then seq must be holding till hready edge happen. 
24. HTRANS - 01: Busy - INCR during wait - busy to any type allowed even new. 
25. 10,11 : NONSEQ-SEQ -- single/first transfer,consecutive transfer in a burst- everyaddress one trans value.NONSEQ -- ADDRESS/CTRLS unrelated to previous ; seq-related - addr[n] = addr[n-1]+ transfer size n>0  
26. nonseq: next one any hready will delay. doesnt matter nextone idle or not.
27. HSIZE and HBURST. HBURST>1 case now.
28. HMASTLOCK -HIGH - ONLY FOR MPMC - ENSURES ORDER OF READ WRITE MUST-IDLE must follow.
29. TFS= (2** HSIZE) = (1<<HSIZE) measured in bytes NOT BITS .TFS <= length (HWDATA)
30. HBURST[2:1] !=0 &&  BL = (2 ** (HBURST [2:1]+1)) = NO OF BEATS/ADDRESS CHANGE.
31. SA[HSIZE-1:0] == '0 . must meet for start. BYTE HSIZE 0 anyway by default byte
32. each address 1 byte - ARM life. address_n = address_n-1 + (1<<HSIZE).
33. INCR = HBURST[0] , WRAP = !HBURST[0] when HBURST[2:1] !=0 , SINGLE= ~(|(HBURST[2:0])) 
34. total data TD = (1<<HSIZE) * BL. IN BL>1  = (1<<(HSIZE+HBURST [2:1]+1)).
35. start_addr[31:10] == end_addr[31:10] in a burst. for incr (start_addr[9:0] + TD - 1) <= 10'h3FF
36. SEQ:WRAP:
    TD - DEFINITELY some 2's power  so N=LOG2(TD) . eg 16 byte -> N = 4
    so N-1 = HSIZE+HBURST [2:1] e.g. 3 
    wrap_base = SA &(SA[N-1:0]=0)
    inc_address[n] = address[n-1] + (1<<HSIZE)    
    addr[n] =  { SA[M:N],  inc_address[N-1:0]}  EQUIVALENT TO    addr[n] = wrap_base + (inc_address- wrap_base) % WB  
    
38.
39.
40. min address space for a slave 1 KB. ADDR[0][HSIZE-1:0] == '0 . must meet for start. for HSIZE>0. 

30. 
  

    
   































2.  for beat_length 1 and INCR beath length shall be ignored

3. Burst total :  no of beat + starting address phase.

4. data/beat = (2** HSIZE) = (1<<HSIZE) //  2**HSIZE <= DATA_width must for data

5. 
6. total length/no of cycle = 1 start + wait_states/idle/busy_states+no of beats (N)

7. Addr incr total 1KB address boundary - no cross - 1024 bytes max. can be smaller based on starting. 

8. 
10. 
11. AHB2 - ERROR : 2 BIT : OKAY, ERROR, RETRY SPLIT.

12. preemption when extreme latency - re arbitration for pending.

13. wait state - extends the same-time address phase of next transfer.

14. HBURST - Burst type.( 0, 1: undef). Any incr - seq location. address is incr of prev.
    idle -1 addr phase - data from prev can continue no impact - okay response -0 wait must.

15. busy type - idle may come. busy type address -control of next already. transfer ignored by slave - okay response -0 wait must.

16. NONSEQ type - first transfer of bus or single transfer unrelated to previous tranfer. - 

17. SEQ: Addr determined by prev. eq.8 is valid from 2nd beat's address. control remains same throughout. 

18. 
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
