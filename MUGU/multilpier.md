# MULTIPLIER
## RTL CODE
```
module multiplier(multiplier, multiplicand, product);
    parameter width = 12;
    input[width-1 : 0] multiplier,multiplicand;
    output[2*width-1 : 0] product;
    assign product = multiplier * multiplicand;
    
endmodule
```

## TB
```
module multiplier_testbench();
parameter width = 12;
reg[width-1 : 0] multiplier, multiplicand;
wire[width-1 : 0] product;
multiplier dut(multiplier, multiplicand, product);

initial
 begin
   multiplier = 12'd0;
   multiplicand = 12'd0;
   end
   
always #((2**width)*2) multiplier = multiplier + 1'b1;
always #2 multiplicand = multiplicand + 1'b1;
endmodule

```
