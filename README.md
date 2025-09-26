# EXPERIMENT 3B: Simulation of All Flip-Flops using Non Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **Non blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **Non blocking assignment (`<=`)** inside the `always` block.  
Non Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Non Blocking)
```verilog
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @ (posedge clk) 
begin
if (rst==1)
q <= 0;
else if(s==0 && r==0)
q <= q;
else if(s==0 && r==1)
q <= 1'b0;
else if(s==1 && r==0)
q <= 1'b1;
else
q <= 1'bx;
end
endmodule
```
### SR Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module srff_tb;
reg s,r,clk,rst;
wire q;
srff uut(s,r,clk,rst,q);
always #5 clk=~clk;
initial begin
clk=0;s=0;r=0;rst=1;
#10; 
rst=0;
#10; s=1; r=0; 
#10; s=0; r=0; 
#10; s=0; r=1; 
#10; s=1; r=1;
#10; s=1; r=0; 
#20;
$finish;
end
endmodule
```
#### SIMULATION OUTPUT

![WhatsApp Image 2025-09-24 at 13 34 06_83ad07fc](https://github.com/user-attachments/assets/dbce4d19-a231-4d89-b931-3fe69c8f9013)


---

### JK Flip-Flop (Non Blocking)
```verilog
module jkff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always @ (posedge clk) 
begin
if (rst==1)
q <= 0;
else if(j==0 && k==0)
q <= q;
else if(j==0 && k==1)
q <= 1'b0;
else if(j==1 && k==0)
q <= 1'b1;
else
q <= ~q;
end
endmodule
```
### JK Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module jkff_tb;
reg j,k,clk,rst;
wire q;
jkff uut(j,k,clk,rst,q);
always #5 clk = ~clk;
initial begin
clk = 0;
j = 0; k = 0;
rst = 1;
#10 rst = 0;
#10 j = 1; k = 0; 
#10 j = 0; k = 0; 
#10 j = 0; k = 1; 
#10 j = 1; k = 1; 
#10 j = 1; k = 0; 
#20 $finish;
end
endmodule
```
#### SIMULATION OUTPUT
![WhatsApp Image 2025-09-24 at 13 34 17_23d786aa](https://github.com/user-attachments/assets/87013a12-4b44-4c50-a97b-1963c1a611ac)

---
### D Flip-Flop (Non Blocking)
```verilog
module d_ff(D,clk,rst,Q);
input D,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==1)
    Q<=0;
else
    Q<=D;
end
endmodule
```
### D Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module d_ff_tb;
reg D,rst,clk;
wire Q;
d_ff uut(D,clk,rst,Q);
always #5 clk= ~clk;
initial
begin
D=0;clk=0;rst=1;#10;
rst=0;D=0;#10;
D=1;#20;
$finish;
end
endmodule
```

#### SIMULATION OUTPUT

![WhatsApp Image 2025-09-24 at 13 34 39_9917ff66](https://github.com/user-attachments/assets/a2fba0c2-9e01-4eed-81e9-486736b2b7c5)

---
### T Flip-Flop (Non Blocking)
```verilog
module t_ff(T,clk,rst,Q);
input T,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==1)
    Q <= 0;
else if (T==0)
    Q <= Q;
else
    Q <= ~Q;
end
endmodule
```
### T Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module t_ff_tb;
reg T,rst,clk;
wire Q;
t_ff uut(T,clk,rst,Q);
always #5 clk = ~clk;
initial
begin
T=0; clk=0; rst=1; #10;
rst=0; #10;
T=0;#10;
T=1; #10;
$finish;
end
endmodule
```

#### SIMULATION OUTPUT

![WhatsApp Image 2025-09-24 at 13 34 47_a51ad7c0](https://github.com/user-attachments/assets/085a0e99-9ac0-4e04-8289-252711127cb0)

---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
