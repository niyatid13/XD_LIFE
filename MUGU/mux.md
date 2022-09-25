# MUX
## RTL CODE
```
module mux(
     input [15:0] din,
     input [3:0] s,
     output reg dout
     );
     always@(din or s)
     begin
         case(s)
         4'd0: dout = din[0];
         4'd1: dout = din[0];
         4'd2: dout = din[0];
         4'd3: dout = din[0];
         4'd4: dout = din[0];
         4'd5: dout = din[0];
         4'd6: dout = din[0];
         4'd7: dout = din[0];
         4'd8: dout = din[0];
         4'd9: dout = din[0];
         4'd10: dout = din[0];
         4'd11: dout = din[0];
         4'd12: dout = din[0];
         4'd13: dout = din[0];
         4'd14: dout = din[0];
         4'd15: dout = din[0];
         endcase
         end
endmodule
```

## TB CODE
```
module mux_tb();
reg [15:0] din;
reg [3:0] s;
wire dout;

mux tb(din,s,dout);

initial
begin
s=3'b0;
din=16'b0;
end

always #10 s=s+1'b1;
always #5 din=~din;
endmodule
```
