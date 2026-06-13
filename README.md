# Verilog-Practice-

 //Alwaysblock1
module top_module(
    input a, 
    input b,
    output wire out_assign,
    output reg out_alwaysblock
);
assign out_assign=a&b;
always @(*) out_alwaysblock=a&b;
endmodule

//Alwaysblock2
module top_module(
    input clk,
    input a,
    input b,
    output wire out_assign,
    output reg out_always_comb,
    output reg out_always_ff   );
assign out_assign=a^b;
    always@(*) out_always_comb=a^b;
    always@(posedge clk) begin 
        out_always_ff=a^b; 
    end
endmodule

//Vivado 32 bit synchronous counter 

//main code

module a(input clk,r,d ,output reg [31:0] count);
always @(posedge clk) begin 
if (r) 
count <=32'b0;
else 
count=count+1;
end 
endmodule

//testbench 

module as;
reg clk,r,d;
wire [31:0] count; 
a uut(
.clk(clk),
.r(r),
.d(d),
.count(count)
);
initial clk = 0;
always #5 clk = ~clk;
initial begin
r=1; #100;
r=0; #100;
d=32'b0;
end
endmodule

