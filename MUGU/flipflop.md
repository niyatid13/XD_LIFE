# FLIPFLOP
## RTL
```
module ff(
input clk,rst,din,en,
output reg dout
    );
   
    always@ (posedge clk or negedge rst)
    begin
    if(!rst)
       dout<=1'b0;
    else if(en)
       dout<=din;
    end
endmodule
```

## TB
```
module ff_tb();
reg clk,rst,din,en;
wire dout;
 
ff tb(clk,rst,din,en,dout);

initial
begin
clk=1'b0;
rst=1'b0;
din=1'b0;
en=1'b0;
end

always #5 clk = ~clk;
always #7 rst = ~rst;
always #11 en = ~en;
always #17 din = ~din;
endmodule
```
