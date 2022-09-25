# LATCH
## RTL
```
module latch(
    input clk,
    input din,
    input reset,
    output reg dout
    );
    always @ (clk or din or reset)
    begin
    if (!reset)
    dout <= 1'b0;
    else if (clk)
    dout <= din;
    end
endmodule

```

## TB

```
module latch_tb();
reg clk,din,reset;
wire dout;
latch tb(clk,din,reset,dout);
initial
begin

clk=1'b0;
din=1'b0;
reset=1'b1;
end
always #5 clk = !clk;
always #13 din = !din;
always #200 reset = !reset;
endmodule
```
