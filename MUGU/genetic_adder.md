# Generic Adder
## RTL CODE
```
module bit4_adder(Ain, Bin, Cin, sum, carry);
    parameter width = 24;
    //parameter width = 25;
input[width - 1:0] Ain, Bin;
input Cin;
output [width - 1:0] sum;
output carry;
wire [width : 0] C;
genvar i;
        assign C[0] = Cin;
    generate
        for( i=0; i < width; i=i+1)
        begin : Adder_gen
            full_adder dut(Ain[i], Bin[i], C[i], sum[i], C[i +1]);
        end
     endgenerate
        assign carry = C[width];
//full_adder dut1 (Ain[0], Bin[0], Cin, sum[0], C[0]);
//full_adder dut2 (Ain[1], Bin[1], C[0], sum[1], C[1]);
//full_adder dut3 (Ain[2], Bin[2], C[1], sum[2], C[2]);
//full_adder dut4 (Ain[3], Bin[3], C[2], sum[3], carry);

endmodule
```
## TB

```
module generic_testbench();
    parameter width = 24;
    reg [width-1 : 0] Ain, Bin;
    reg Cin;
    wire [width-1 : 0] sum;
    wire carry;
    bit4_adder tb(Ain, Bin, Cin, sum, carry);
    initial
    begin
    Ain = 24'd0;
    Bin = 24'd0;
Cin = 1'd0;
    #100;
    end
    
    always #20 Ain = Ain + 1'b1;
    always #10 Bin = Bin + 1'b1;    
    always #5 Cin = -Cin;
endmodule

```
