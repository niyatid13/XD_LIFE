# MUX
## RTL CODE
```
module mux(
input [15:0]din,
input [3:0]sel,
output reg dout
    );
   
    always@(din or sel)
    begin
    case(sel)
    4'b0000: dout<=din[0];
    4'b0001: dout<=din[1];
    4'b0010: dout<=din[2];
    4'b0011: dout<=din[3];
    4'b0100: dout<=din[4];
    4'b0101: dout<=din[5];
    4'b0110: dout<=din[6];
    4'b0111: dout<=din[7];
    4'b1000: dout<=din[8];
    4'b1001: dout<=din[9];
    4'b1010: dout<=din[10];
    4'b1011: dout<=din[11];
    4'b1100: dout<=din[12];
    4'b1101: dout<=din[13];
    4'b1110: dout<=din[14];
    4'b1111: dout<=din[15];
    endcase
    end
endmodule
```

## TB CODE
```
module Mux_tb();
reg [15:0]din;
reg [3:0]sel;
wire dout;

mux tb(din,sel,dout);

initial
begin
sel=3'b0;
din=16'b0;
end

always #10 sel=sel+1'b1;
always #5 din=~din;
endmodule
```
