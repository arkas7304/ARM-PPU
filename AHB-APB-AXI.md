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
31. SA[HSIZE-1:0] == '0 . must meet for start. BYTE HSIZE 0 anyway by default byte. 1KB boundary also.
32. each address 1 byte - ARM life. address_n = address_n-1 + (1<<HSIZE).
33. INCR = HBURST[0] , WRAP = !HBURST[0] when HBURST[2:1] !=0 , SINGLE= ~(|(HBURST[2:0])) 
34. total data TD = (1<<HSIZE) * BL. IN BL>1  = (1<<(HSIZE+HBURST [2:1]+1)).
35. start_addr[31:10] == end_addr[31:10] in a burst. for incr (start_addr[9:0] + TD - 1) <= 10'h3FF
36. SEQ:WRAP: 
    WB=TD =(1<<(HSIZE+HBURST [2:1]+1)) - DEFINITELY some 2's power  so N=LOG2(TD)  . eg 16 byte -> N = 4 (ARM life)
    N-1 = HSIZE+HBURST [2:1] e.g. 3 
    wrap_base = SA - (SA%WB) = FLOOR[SA/WB] = SA &(SA[N-1:0]=0)
    addr[0]= SA
    inc_address_n = address[n-1] + (1<<HSIZE)    for all n < (1<<(HBURST [2:1]+1))
    addr[n] =  { SA[M:N],  inc_address_n[N-1:0]}  EQUIVALENT TO    addr[n] = wrap_base + (inc_address_n- wrap_base) % WB  
    where M is the highest bit.    
37. incr burst 1KB boundary must honor. min address space for a slave 1 KB. ADDR[0][HSIZE-1:0] == '0 . must meet for start. for HSIZE>0.
38. ERROR - can cel or continue. if cancel - no rebuild requirement.
39. Master cannot terminate burst request early - but slave must be tolerant. because interconnect can terminate for multimaster.
40. During Wait Master can introduce IDLE TO NONSEQ if IDLE is allowed as per sequence. so at earliest first one idle because hready starts with data phase of previous. thenONWARDS nonseq CONSTANT Till HReady rising. 
41. SEQ-DATPHASE-HREADYDOWN BUSYUP THEN SEQ may come - then constant till HREADY high. for fixed length case
42. incr- last seq -data hready- then busy put and change to NONSEQ for new type - it must hold same TRANS.
43. address  for idle can change others must hold during wait. error during wait last cycle - master permitted to change adress even as low.
44. PROTS added from APB -2 sifted to 0 0 to 1. then 2 non/bufferable 3 non/cacheable.
45. DEFAULT SLAVE with blank address space - address space no overlap. SEQ/NONSEQ ERROR. IDLE/BUSY OKAY. ERROR RESPONSE TIED TO DATA PHASE. MAY BE in wait state.
46. HREADYOUT from each SLAVE- Muxed HREADY to master and back to slave in for monitoring.
47. HRESP:HREADY :: 00 REGULAR PENDING 01 TRANSFER SUCCESSFUL DATA PHASE 10 ERROR RESPONSE CYCLE 1 11 ERROR RESPONSE CYCLE 2. REMEMBER HAPPENS IN DATA STAGE PIPELINE always maintained.
48. 1,2,4,8,16,32,64,128 BYTES only so bytes are 2**k - k 0 to 7 .  (1<<HSIZE) : TS <= DW/8 (data_width IN BYTE) ; SA[HSIZE-1:0] == '0
    Q1: SA falls for full bus - by D=DW/8 in bytes - then (SA%D)==0 -> SA[k-1:0] = 0 - thats for start align - we know 
    Q2: NOW , think they are not -> always condition HSIZE <= k : no_of_narrow transaction or lanegroup: 2^(k - HSIZE)  and lanegroup no = floor((SA % D) / TS) = ADDRESS[k-1:HSIZE] lane
    Q3. HENCE , starting BYTE LANE segment - m=ADDRESS[k-1:0] determines which no .so WD [(m+(1<<HSIZE))*8-1 :m*8]

49. for big endian - g=((1<<k)/(1<<HSIZE)) -1 - ADDRESS [K-1:HSIZE] lanegroup no. m=ADDRESS[k-1:0] 
                     WD [ ((1<<K)-m)*8-1   :((1<<K)-(m+(1<<HSIZE)))*8]
    
HADDR[K] -> SELECTOR 0 -> K-1 : 2**K differrent address means 2 **K bytes -> more widers K..N address works as selector. narrow slave on wide bus. - latch selector address with HREADY as enable.
- kind of lane selection - and reverse lane selection.

AXI- 
VERSION A: 
1. decoupling of pipeline of address phase and data phase. KEEP on dumping Starting address and size (equivalent of HBURST) data will keep on coming out. So for each data individual address need not toggle. less switching of address bus.
2. out of order support- Slaves can return out of order data (e.g. by availability)
3. out of order support. ID Tag- same ID tag must follow the order - interconnect buffering fast slaves to allow priority transaction. - (INTERCONNECT ALSO must ensure same ID same order ?).
4. Master overrides outof order by same ID - simple slave can ignore outoforder anyway.
5. out of order - every channel own separate ready,valid,id.
6. ARValid sampled high to RLAST going high - a SLAVE's limit assuming RREADY always. say that L no clock cycle.  it takes L*T sec time for 1 address - so in 1 hour there would be 3600/(L * T) no of address dump. LAST is for smart routing less thread tracker per ID. Interconnect can operate out of ordering independently of master so without last it would balloon up.
7. same AWVALID going down to wlast going up (wvalid wready tango).
8. for decoupling ready two way and also for address data separately and source also delay by valid. - pipeline register insertion to fix timing handshake - combi logic path at master from Hready- NO WAIT for READY for valid assertion. - symmetrical flow control.
9.  B channel solves write data completion status/error - master can proceed with other slaves/out of order write/ intermediatory hand-offs - more control over latency and signaling to first source system wide/ read after write hazards.
10. HBURST-split into LEN and BURST.
11. wstrb[k]==1 means WDATA[ 8*K+7 : 8 * K] - 32 bit DATA bus fixed.
12. LOCK(2), CACHE(4) separate, PROT same as  APB4. RESP (B,R) same with two added value EXOKAY,DECERR.
13. CSYSREQ,CSYSACK,CACTIVE (Qchannel like but not yet).
14. 























13.  for beat_length 1 and INCR beath length shall be ignored

14. Burst total :  no of beat + starting address phase.

15. data/beat = (2** HSIZE) = (1<<HSIZE) //  2**HSIZE <= DATA_width must for data

16. 
17. total length/no of cycle = 1 start + wait_states/idle/busy_states+no of beats (N)

18. Addr incr total 1KB address boundary - no cross - 1024 bytes max. can be smaller based on starting. 

19. 
20. 
21. AHB2 - ERROR : 2 BIT : OKAY, ERROR, RETRY SPLIT.

22. preemption when extreme latency - re arbitration for pending.

23. wait state - extends the same-time address phase of next transfer.

24. HBURST - Burst type.( 0, 1: undef). Any incr - seq location. address is incr of prev.
    idle -1 addr phase - data from prev can continue no impact - okay response -0 wait must.

25. busy type - idle may come. busy type address -control of next already. transfer ignored by slave - okay response -0 wait must.

26. NONSEQ type - first transfer of bus or single transfer unrelated to previous tranfer. - 

27. SEQ: Addr determined by prev. eq.8 is valid from 2nd beat's address. control remains same throughout. 

28. 
29. multi master case: if burst termination forced - rebuild of burst at next point onward after reacquire - this requirement not there in ahb-lite AMBA 3 but there in AHB2.

30. HPROT : 3-cacheable 2- bufferable 1-priviledged 0: data/op.

31. HTRANS impact: non existant address = default slave :idle/busy type -OKAY response. rest ERROR response. 

32. Bus master in either AHB-lite or aAMBA2 AHB never cancels a transaction that has started. 

33. ERROR example : write to read only location; access to secure space in nonsecure mode.

34. SPLIT/RETRY: master retry in next grant-slave requesting grant on behalf of master(?)/ master keeps on retrying.

35. two cycle response.: 1st ERROR cycle: HRESP = ERROR, HREADY = 0
2nd ERROR cycle: HRESP = ERROR, HREADY = 1 

36. meaning clear if you think response is a state for the data line. and two times to prepare the master to cancel 1 stage pipeline.

37. Hready first sampled by master at cycle 2 end.

38. retry - arbiter continues normal priority scheme - split frees for all - but slave must tell back when data is available. master both same.

39. HMASTKLOCK - breaks pipeline for atomic processing. second phase same address - then idle

40. busy+nonseq or idle at end of bus.: only for undefined  incr. everything else seq must end.single-busy not allowed. idle or nonseq with non single hburst must before busy.

41. start end implicit - so type alone can determine. error response - master termination allowed, no termination also allowed. no rebuild required. slave design should be termination tolerant.

42. wait -> idle to non seq allowed. wait issued in response to previous nonseq or seq. but onlce nonseq within wait - must hold.

43. wait busy -> seq allowed : busy wait issued in response to previous nonseq or seq. once seq back - must hold. fixed length.

44. wait busy -> anytype allowed : busy wait issued in response to previous nonseq or seq. once anytime back on nowait - must hold.termination or continuation of burst.

45. idle to nonseq - during wait new addr - addr holds.

46. error - 2 cycle error - 2nd cycle begining new address can be put.

47. address deconding - HSEL to each servant based on address space.non existant address- default slave - nonseq/seq error response. idle/busy ok response.

48. HRESP 1 - error - must be two type of Hready - wait and then 1.
49. reccommendation max 16 wait states.  1 error sampling by master is enough to terminate by an idle transaction.
50. 

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
