# LATCH
## RTL
```
module latch(
input din,clk,
output reg dout
    );
   
    always@(clk or din)
    begin
    if(clk)
     dout<=din;
    end
endmodule
```
