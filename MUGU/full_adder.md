# FULL ADDER
## RTL
```
`timescale 1ns / 1ps
module full_adder(
    input a_in,
    input b_in,
    input c_in,
    output sum,
    output carry
    );
    assign sum = a_in ^ b_in ^ c_in;
    assign carry = (a_in & b_in) | (c_in & (a_in ^ b_in));
endmodule
```
## TB
```
`timescale 1ns / 1ps
module full_addertb();
reg a_in, b_in, c_in;
wire sum, carry;

full_adder dut(a_in, b_in, c_in, sum, carry);

initial 
begin
a_in = 1'B0;
b_in = 1'B0;
c_in = 1'B0;
end 
always #5 c_in = ~c_in;
always #10 b_in = ~b_in;
always #15 a_in = ~a_in;
endmodule
```
