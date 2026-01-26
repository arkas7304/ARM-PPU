1. interface bundle of net.
2. bundle of nets or variable. keeps direction inside unlike struct. can become a port item with multiple direction.

3. class which becomes port element alon with direction inside.

4. directions are seen from the module modport inside interface controls the structure.

5. interface: processes - initial/always block. continuous assignement. - protocol check provision in port itself.

6. abstract - defined in one module - export import construct. local hierarchichal for task and function. forkjoin for brodcast.

7. encapsulation of communication. modules made can become generic.

8. interface conatin interface.

9. interface identifier;
...
interface_items
...
endinterface [ : identifier ]

10. myinterface #(100) scalar1(), vector[9:0]();
An interface can be instantiated hierarchically like a module, with or without ports. For example:
myinterface #(100) scalar1(), vector[9:0]();

11. interface decl and inst within module. module neither inside interface.

12. defparam can not cross outside intereface.

13. hierarchical reference, or modport of hierarchichally referred interface - non array or gen block.

14. e.g.1 : interface_items :: logic [7:0] addr, data;
    1. assignment direction implicit - synthesizers treat them as inout initially. ref for variables.

15. instantiation: 
    e.g. 1: 
    decL : cpuMod(simple_bus b ....
    decl: memMod(simple_bus a ......

    simple_bus sb_intf(); // Instantiate the interface - cpuMod cpu(.b(sb_intf)...
    memMod mem(sb_intf ....

    - same idetifier for name in bot port , clk also same name in both port - .*
    e.g. 2: 
    decL : cpuMod(interface b ....
    decl: memMod(interface a ......

    simple_bus sb_intf(); // Instantiate the interface - cpuMod cpu(.b(sb_intf)...
    memMod mem(sb_intf ... not allowed 
    implicit port method banned for this so max one can have  - memMod mem (.*, .a(sb_intf)); // partial implicit port connections

16. common wire to all module can become anchor in interface - where interface is instantiated. and 
    simple_bus sb_intf1(clk);
    simple_bus sb_intf2(clk); // Can be shared by another interface as well.


    -> memMod mem1(.a(sb_intf1)); no need of separate clk connection.

17. Modports. 
    interface i2;
        wire a, b, c, d;
        modport master (input a, b, output c, d);
        modport slave (output a, b, input c, d);
    endinterface

18. e.g.1:
    decl: m(i2.master ia)
    decl: s(i2.slave ib)


    instantiations : i2 ik(); m u1 ( .ia (ik) ); s u2 (.ib (ik)); 

19. port to sub-module port connection - modport names and lists must be identical.

20. no reference from outside. no absent declaration especially for modport port . (a,b,c,d)

21. modport declared but not used. as usual story. inout or ref.

22. e,g. of modport to modport connection. named port bundle. generic from higher lower modport.
    
    decl : cpuMod (simple_bus.master b...
    memMod (simple_bus.slave a ....

    simple_bus sb_intf(); // Instantiate the intf
    memMod mem(.a(sb_intf)); 
    cpuMod cpu(.b(sb_intf));

23. e.g. connecting port bundle. modport from higher -lower generic
        
    decl : cpuMod (simple_bus b...
    memMod (simple_bus b ..

    simple_bus sb_intf(); // Instantiate the intf
    memMod mem(sb_intf.slave); 
    cpuMod cpu(sb_intf.master);
    
24. decl : memMod(interface a) , cpuMod(interface b);
           memMod mem(sb_intf.slave)
           cpuMod cpu(sb_intf.master);

25. modport expression:  refer 20 - however output .P(r[3:0]) instead of output r  - redefinition at port level. expression based modification.

26. interface i , map with : i1.A i1.B.

27. 