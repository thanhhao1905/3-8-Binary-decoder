```verilog
module binary_decoder_3_8 (input wire [2:0] y,
                           output reg [7:0] d);
  always@(y)begin
    d = 0;
    case(y)
      3'b000: d[0] = 1'b1;
      3'b001: d[1] = 1'b1;
      3'b010: d[2] = 1'b1;
      3'b011: d[3] = 1'b1;
      3'b100: d[4] = 1'b1;
      3'b101: d[5] = 1'b1;
      3'b110: d[6] = 1'b1;
      3'b111: d[7] = 1'b1;
      default: d = 8'bxxxxxxxx;
    endcase
  end
endmodule
      
