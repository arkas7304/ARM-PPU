1. time literal - unsigned no /fp no time unit. unit -> s, ms, us, ns, ps,fs, step.
2. unsized literal - single bit owidth 1 - repeated to fill the size.
3. real literal 0 fixed point format. 1.2 and 2e10 both real literal.
4. time literal realtime:  (fp or integer literal with time unit)
5. string literal : "" enclosed - \v \f \a \x02 : sv special add. \ for any nonprintable char and specialchar.
6. string - multi line \ before new line char: new line ignore.
7. string literal ->  unpacked array of bytes - left justified. cast to array - same rule.
8. new string data type -> arbitrary length- packed array - 8's multiple bit size literal.
9. Array literal -> C initialiser - '{'{}}  ::  {{}}replicator allowed. outer of replicator is part of lietral operator in this case.
10. original '{'{4,5,4,5,4,5},'{4,5,4,5,4,5}} == '{'{3{4,5}},'{3{4,5}}}  : 4,5,4,5,4,5 replaced by 3{4,5} but existance of immediate '{} must. if already there no new req
11. '{'{3{4,5}},'{3{4,5}}} == '{2{'{3{4,5}}}} 
