---
layout: project
type: project
image: img/ALU/alu_symbol.jpg
title: "Arithmetic Logic Unit (ALU)"
date: 2024
published: true
labels:
  - Verilog
  - FPGA
summary: "I developed a simple Arithmetic Logic Unit (ALU) as the final project of ECE 260"
---

Arithmetic Logic Units (ALUs) are a fundamental component of a computer’s central processing unit (CPU). They are responsible for performing arithmetic and logical operations such as addition, subtraction, and multiplication. ECE 260 is a course on digital logic and design and the final project required us to design and verify an ALU that operated on two 4-bit inputs. This project served as the culmination of the semester’s work, combining truth table design, K-map simplification, logic gate simulation, and hardware implementation.

For this project, I was responsible for the entire design and implementation process. I first constructed the truth tables for each operation and simplified them using K-maps. Next, I simulated the logic circuits for each module in the Falstad digital simulator and combined them into submodules, producing a complete ALU simulation file (`ALU.txt`). Finally, I wrote the Verilog description (`alu.v`) of the ALU and programmed it onto an FPGA to verify that the hardware implementation matched the expected results.

The requirements of the ALU can be found from the following:
<div style="text-align:center;">
  <img src="{{ '/img/ALU/Table.png' | relative_url }}" alt="ALU table" class="d-block mx-auto">
  <img src="{{ '/img/ALU/Schematic.png' | relative_url }}" alt="ALU schematic" class="d-block mx-auto">
</div>

### Inputs
**A** and **B** were 4-bit inputs for the ALU, **S** was the 3-bit operation code specifier, and **XIN** was the carry-in bit.

### Outputs
**F** was the 4-bit output that resulted from the operation. **Z** was the flag to indicate that **F** was zero, **V** was the flag to indicate whether there was an overflow, and **C** was the carry/borrow flag used in addition and subtraction.

### Results
This project was both challenging and rewarding because it brought together all of the skills I had developed throughout the course. I gained practical experience in digital design by moving from abstract truth tables to working circuits and real hardware. I also reinforced my understanding of K-maps, logic simplification, and simulation workflows, and I saw firsthand how these concepts translate into Verilog and FPGA programming. Completing the entire project independently was a satisfying demonstration of the knowledge and problem-solving strategies I had built during the semester.

A pdf showing the work that I did for this project can be found <a href="{{ '/downloads/ALU/Final Project.pdf' | relative_url }}" download> here </a>.

In addition you can simulate the final result by visiting [Falstad](https://www.falstad.com/circuit/) and `file` -> `Import From Text` -> <a href="{{ '/downloads/ALU/ALU.txt' | relative_url }}" download>copy and paste this file</a>.



The verilog code for `alu.v` can be found below: 
```verilog
module ALU( 
  input [2:0] S, 
  input [3:0] A,
  input [3:0] B,
  output Z, 
  output V, 
  output C,
  output [3:0] F 
           );
  
  reg [7:0] out;
  
  always @* 
    begin
  	case(S)
      3'b000: // 2 x A
      	out = 2 * A;
      3'b001: // A / 2
        out = A / 2;
      3'b010: // A x B
      	out = A * B;
      3'b011: // A + B
      	out = A + B;
      3'b100: // A - B
      	out = A - B;
      3'b101: // B - A
        out = B - A;
      3'b110: // A XOR B
        out = A ^ B;
      3'b111: // A < B
        out = (A < B) ? 1:0;  
      default: out = 0;
    endcase
  end
  
  assign Z = ( out == 4'b0000 );
  assign V = (|out[7:4]);
  assign C = (S == 3'b011 && (out[4] | (A[3] & B[3]))) || 
             (S == 3'b100 && (A[3] < B[3])) || 
             (S == 3'b101 && (B[3] < A[3]));
  assign F = out;
    
endmodule
```