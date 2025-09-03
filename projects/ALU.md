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

Arithmetic Logic Unit also known as ALUs are a fundemental part of a computer's central proccessing unit (CPU). They are responsible for performing basic arithmetic operations such as addition, subtraction, and multiplication. The particular ALU that I had to design for this project did operations on two 4-bit inputs based on the following table: 

<div style="text-align:center;">
  <img src="{{ "/img/ALU/table.png" | relative_url }}"     >
  <img src="{{ "/img/ALU/schematic.png" | relative_url }}" >
</div>

### Inputs
**A** and **B** were 4-bit inputs for the ALU, **S** was the 3-bit operation code specifier, and **XIN** was the carry in bit.

### Ouputs
**F** was the 4-bit output that resulted from the operation. **Z** was the flag to indicate that **F** was zero, **V** was the flag to indicate to indicate if there was no overflow. **C** was the flag only for subtraction and addition to indicate if there was a carry/borrow out.

We first desgined and solved the truth tables for each operation separately on paper. Then we had to simulate each operation on Falstad which is a circuit simulator. 
<a href="{{ '/downloads/alu.txt' | relative_url }}" download>
  Download Simulation File
</a>

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
//  assign V = (out >= 4'b1111 || out <= -15);
  assign C = (S == 3'b011 && (out[4] | (A[3] & B[3]))) || (S == 3'b100 && (A[3] < B[3])) || (S == 3'b101 && (B[3] < A[3]));
  assign F = out;

    
endmodule
```

You can learn more about the [project](https://sites.google.com/view/ee260/homework/alu-project?authuser=0) and the course [ECE 260](https://catalog.manoa.hawaii.edu/preview_course_nopop.php?catoid=2&coid=36706).
