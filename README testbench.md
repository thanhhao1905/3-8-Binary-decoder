```verilog
`timescale 1ps/1ps
module tb_binary_decoder_3_8;
  
  reg [2:0] y;
  wire [7:0] d;
  reg [7:0] exp_d;
  integer i,j, err =0;
  
  binary_decoder_3_8 DUT (y, d);
  
  initial begin
    $monitor("time=%0t, y=%b ,d=%b, exp_d=%b",$time, y, d, exp_d);
    
    for(i=0; i<8; i=i+1)begin
      y = i ;
      exp_d = 8'b1 << i;
    #5;
      check(d,exp_d);
    end
    
    if(err==0) begin
      $display("---------");
      $display("Test Pass");
      $display("---------");
    end else begin
      $display("---------");
      $display("Test Fail with %d error",err);
      $display("---------");
    end
    
    $finish;
  end
  
  task check (input d, input exp_d);
    begin
    if(d!==exp_d) begin
      $display("[CHECK] ERROR");
      err= err+1;
    end else begin
      $display("[CHECK] MATCHING");
    end
   end
  endtask
  
  initial begin
    $dumpfile("dump.vcd");
    $dumpvars;
  end
endmodule
