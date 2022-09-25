# MAC UNIT
## RTL
```
module mac(
input [11:0] in_1,in_2,
input clk,rst,
output [24:0]out
);

wire carry;
wire C_in;
reg [24:0] sum_reg;
assign C_in=1'b0;
wire [23:0] mul_out;
wire [24:0] add_out;
wire [24:0] sum_out;

multiplier dut(in_1,in_2,mul_out);
bit_4_adder_generate dut1(mul_out,sum_out,C_in,add_out[23:0],add_out[24]);

   always @(posedge clk)
      if (rst) begin
         sum_reg <= 24'd0;
      end else begin
         sum_reg <= add_out;
      end
     
 assign out=sum_reg;
 assign sum_out=sum_reg;
     
endmodule
```

## TB
```
module mac_tb();
reg clk,rst;
reg [11:0]  in_1,in_2;
wire [24:0] out;
mac tb(in_1,in_2,clk,rst,out);

initial
begin
clk=1'b0;
rst=1'b1;
in_1=11'd0;
in_2=11'd0;
end

always #5 clk=~clk;

always #30 in_1=in_1+1'b1;
always #(2**12*30) in_2=in_2+1'b1;
always #1555 rst=~rst;

endmodule

```
