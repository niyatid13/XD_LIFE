# ALL GATES
## RTL
```
`timescale 1ns / 1ps
module all_gates(
    input a_in,
    input b_in,
    output y_not,
    output y_and,
    output y_or,
    output y_xor,
    output y_nand,
    output y_nor,
    output y_xnor
    );
    assign y_not = ~a_in;
    assign y_and = a_in & b_in;
    assign y_or = a_in | b_in;
    assign y_xor = a_in ^ b_in;
    assign y_nand = ~a_in | ~b_in;
    assign y_nor = ~a_in & ~b_in;
    assign y_xnor = a_in ~^ b_in;
endmodule
```

## TB
```
`timescale 1ns / 1ps
module all_gatestb();
reg a_in, b_in;
wire y_not, y_and, y_or, y_xor, y_nand, y_nor, y_xnor;

all_gates dut(a_in, b_in,y_not, y_and, y_or, y_xor, y_nand, y_nor, y_xnor);

initial 
begin
a_in = 1'B0;
b_in = 1'B0;
end

always #5 b_in = ~b_in;
always #10 a_in = ~a_in;
endmodule
```
