we - got blocks and assignments - now data types.

1. COWSKIN.
2. comment - // Or /**/
3. /**/ not to be nested. // withn /**/ no special meaning.
4. ' ascii 0x27.
5. form 1 regular number. signed integer deafault.
6. form 2 -  l'[s|S]d|h|o|bxxxx - default unsigned integer
7. form 2 - l nonzero unsigned decimal - total bit count.
8. no white space inbetween 
9. s - lets bit pattern be stored as it is - just inter pretation changes.

10. unary + or minus.

11. \n \t \\ \" \ddd

12. identifier  $, _ alphanemueric. $ digit as first cannot be. case sensitive.

13. real to integer - nearest.

interesting - 

// Testbench
module test;

  reg        clk_read;
  reg  [4:0] address_write;
  reg  [3:0] test_1 = -4'b0011;
  integer test_2 = -4'b0011;

  reg  [3:0] test_3 = -4'sd3;
  integer test_4 = -4'sd3;

  // in memory none of them differs: s doesnt alter 1st operand mem storage; and - does the job as. 1,2,3,4 all same
  
  // 
  integer test_5 = 4'd1;
  integer test_6 = -4'sd1;
  //test_5 test_6 coming same.
  integer test_7 = test_5+ test_6;
  
  reg  [3:0] test_8 = test_5 + (4'sd1); // coming as 2 ???? very fshy.
  initial  begin
    // Dump waves
   #10     $display("data1.");
    $display("data[%0h]: %0h",
      test_1, test_2);
    
    #10 $display("data2.");
    $display("data[%0h]: %0h",
      test_3, test_4);
    
   #10 $display("data1.");
    $display("data[%0d]: %0d %0d",
      test_5, test_6, test_8);
 
       #10 $display("data1.");
    $display("data[%0h]: %0h",
      test_7, test_7);

  end

endmodule
