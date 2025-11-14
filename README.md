# **EXP4: 4-bit Ripple Carry Adder using Task and 4-bit Ripple Counter using Function with Testbench**

---

## **Aim**
To design, simulate, and verify a **4-bit Ripple Carry Adder** using **Task** and a **4-bit Ripple Counter** using **Function** in Verilog HDL.

---

## **Apparatus Required**
- System with **Vivado Design Suite**
---

## **Theory**
### **Ripple Carry Adder**
A 4-bit Ripple Carry Adder (RCA) adds two 4-bit binary numbers by cascading four full adders. The carry-out of each full adder acts as the carry-in for the next stage. Using a **task** in Verilog, the addition operation can be modularized for each bit.
<img width="692" height="268" alt="image" src="https://github.com/user-attachments/assets/b70c348a-049a-4462-88a4-ad6905446cf4" />


### **Ripple Counter**
A Ripple Counter is a sequential circuit that counts in binary. In a 4-bit ripple counter, the output of one flip-flop serves as the clock input for the next flip-flop. Using a **function** in Verilog allows the counting logic to be encapsulated and reused.

<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/fa8730fc-e48e-477a-b2e3-6697a95355d3" />

---

## **Program**

### **4-bit Ripple Carry Adder using Task**

```verilog
module rca4(a,b,cin,sum,cout);
input [3:0] a,b;
input cin;
output reg [3:0] sum;
output reg cout;
reg [4:0] temp;
task ripple_add;
input [3:0] x,y;
input c_in;
output [3:0] s;
output c_out;
reg [4:0] t;
begin
t = x + y + c_in; 
s = t[3:0];
c_out = t[4];
end
endtask
always @(*) begin
ripple_add(a,b,cin,sum,cout);
end
endmodule

```

### **Test bench 4-bit Ripple Carry Adder using Task**
```
`timescale 1ns/1ps 
module tb_rca4;
reg [3:0] a,b;
reg cin;
wire [3:0] sum;
wire cout;
rca4 uut(a,b,cin,sum,cout);
initial begin
$monitor("T=%0t | a=%b | b=%b | cin=%b | sum=%b | cout=%b",$time,a,b,cin,sum,cout);
a=4'b1010; b=4'b0101; cin=0;
#10;
a=4'b1111; b=4'b0001; cin=1;
#10;
a=4'b1001; b=4'b0110; cin=0;
#10;
a=4'b1110; b=4'b1111; cin=1;
#10;
end
endmodule
```
### 4-bit Ripple Carry Adder Simulation Output 

-----
-----
-----
-----
<img width="1038" height="658" alt="image" src="https://github.com/user-attachments/assets/9e9598b4-695b-4090-8be4-d6772529b648" />



### **4-bit Ripple Counter using Function**
```
module ripple_counter_4bit(clk, rst, q);
input clk, rst;
output reg [3:0] q;
function [3:0] i;
input [3:0] data;
begin
i = data + 1;
end
endfunction
always @(posedge clk or posedge rst) begin
if (rst)
q <= 4'b0000;
else
q <= i(q);
end
endmodule

```
### **Testbench for 4-bit Ripple Counter using Function**
```
`timescale 1ns / 1ps
module tb_ripple_counter_4bit;
reg clk, rst;
wire [3:0] q;
ripple_counter_4bit uut(clk, rst, q);
always #5 clk = ~clk;
initial begin
$monitor("T=%0t | rst=%b | q=%b (%0d)", $time, rst, q, q);
clk = 0;
rst = 1;  
#10 rst = 0; 
#100;
$finish;
end
endmodule

```
### 4-bit Ripple Counter Simulation output 
-----
-----
-----
-----
<img width="1038" height="656" alt="image" src="https://github.com/user-attachments/assets/8db2caa4-7934-43b9-895f-42c89d197cc1" />








### Result

The simulation of the 4-bit Ripple Carry Adder using Task and 4-bit Ripple Counter using Function was successfully carried out in Vivado Design Suite.
Both designs produced correct functional outputs as verified by waveform and console output.
