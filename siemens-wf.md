1. vlog, vcom, vmap, vlib - common comiler and library maker.
2. qverify - tool - elaborator and primary netlist builder.
3. find nets {.*\.u0\..*} -hierarchy -regexp
   - hierarchy means searching in- fifo_0_h.u0.Rclk fifo_0_h.u0.Ren fifo_0_h.u0.Wadd fifo_0_h.u0.Wclk
   - the hierarchichal (verilog std-2005) naming of any element/SCOPE.
   - regexp means instead of wildcard *.u0.* 
   - netlist targets -group <groupname>
4. assertion compile exclude find nets - etc common netlist usage directives.
5. constraints.tcl - gcdc setup -d <top> -> gcdc_constraints.tcl -> gcdc run -d <top> 
6. netlist load lib - liberty files can be loaded. sdc load - sdc file.
7. gcdc generate directives <RTL constraints > -output_file <outputs>
8. gcdc namemap -rtl_module_transform_prefix <prefix for multi tool support>/ -file
9. cdc same methodology and goal principle.
    - static cdc analysis.
    - assertion based verif with CDC protocol checker.
    - metastability infusion with CDC-FX
11. modeling the random /metastability -
     pseudo random delay.
     clock jitter,
12. metastability injector over cdc cross point.
13. 


