8- BIT CARRY LOOK AHEAD ADDER

A VLSITD LAB PROJECT REPORT 

Submitted
in the partial fulfillment of the requirements for
the award of the degree of

BACHLEOR OF TECHNOLOGY
in
Electronics and Communication Engineering 
by

T. Sneha [21311A04L6]
U. Pooja[21311A04L7]


UNDER THE GUIDANCE OF
Dr .D. ASHADEVI, 
Professor, Dept. of ECE




DEPARTMENT OF ELECTRONICS & COMMUNICATION ENGINEERING
SREENIDHI INSTITUTE OF SCIENCE & TECHNOLOGY
Yamnampet, Ghatkesar, Hyderabad – 501 301
FEBRUARY 2023-2024

	         SREENIDHI INSTITUTE OF SCIENCE & TECHNOLOGY
Yamnampet, Ghatkesar, Hyderabad – 501 301


CERTIFICATE

This is to certify that the Lab Project entitled “ 8-BIT CARRY LOOK AHEAD ADDER”being submitted by T. SNEHA (Roll No.21311A04L6) an U. POOJA (Roll No.21311A04L7) in partial fulfillment for the award of Bachelor of Technology in Electronics and Communication Engineering [ECE], Sreenidhi Institute of Science and Technology, an autonomous institute under Jawaharlal Nehru Technological University, Telangana, is a record of bonafide work carried out by them under our guidance and supervision.
	






Dr. D. ASHADEVI						           (Dr.S.P.V. Subba Rao)
Professor, Department of ECE.		               		Professor & Head,ECE



	



	DECLARATION

 We hereby declare that the work described in this report, entitled   “8-BIT CARRY LOOK AHEAD ADDER”  which is being submitted by us in partial fulfillment for the award of Bachelor of Technology in Electronics and Communication Engineering [ECE], Sreenidhi Institute Of Science &  Technology  affiliated to Jawaharlal Nehru Technological University Hyderabad, Kukatpally, Hyderabad (Telangana) -500 085 is the result of investigations carried out by us/me under the Guidance of Dr.D.ASHADEVI, Professor, ECE Department, Sreenidhi Institute Of Science And Technology, Hyderabad.












Place: Hyderabad
Date:						                                                 Signature


                                                           T.SNEHA(21311A04L6)
                                                       
                                                          U.POOJA(21311A04L7)





                                       CONTENTS
										Page No.
List of Figures                							i		
Abstract										ii
CHAPTER1    INTRODUCTION						1-4
        1.1 Introduction							1-3
        1.2 Strategy for building Carry look ahead adder
          in FPGA using verilog						
1.3    Implementation of Verilog codes in Xilinx           
CHAPTER 2    EXPERIMENTAL WORK					4-6
	2.1	Design Module							4-5
	2.2	Testbench Module							5-6
	2.3	Explanation of the Design Logic				6
CHAPTER 3    EXPERIMENTAL PROCEDURE				6-13 
CHAPTER 4   RESULTS							14-18
4.1	RTL Schematic							14
4.2	Simulated Waveforms			                            14
4.3	Implementation Schematic					16
4.4	Power Report							16
4.5	Utilization Report							17
4.6	Noise Report							17
4.7	Timing Report							18
CHAPTER 5    CONCLUSION							19
CHAPTER 6    REFERENCES							19
ABSTRACT
Full adders are the building blocks of nearly all the VLSI applications—be it digital signal processing or image and video processing. In this paper, an 8-bit Carry Look-ahead Adder is implemented and compared using two different types of designs—a conventional Complementary Metal-Oxide Semiconductor (CMOS) logic and an Efficient Charge Recovery Logic (ECRL). These adders are designed and simulated using Tanner Tools v15.23 with 180 nm technology. Performance parameters like power consumption and propagation delay are compared by varying input supply and operating frequency for the two different circuits. The comparison shows that an 8-bit CLA design using ECRL Adiabatic logic is better than an 8-bit CLA design using CMOS logic in terms of power consumption, transistor count, and power delay product (PDP).
The adder produce carry propagation delay while performing other arithmetic operations like multiplication and divisions as it uses several additions or subtraction steps. This is a major problem for the adder and hence improving the speed of addition will improve the speed of all other arithmetic operations. Hence reducing the carry propagation delay of adders is of great importance. There are different logic design approaches that have been employed to overcome the carry propagation problem. One widely used approach is to employ a carry look-ahead which solves this problem by calculating the carry signals in advance, based on the input signals. This type of adder circuit is called a carry look-ahead adder.












    1. INTRODUCTION

An 8-bit Carry Look-Ahead Adder (CLA) is a digital circuit designed to perform the addition of two 8-bit binary numbers. The primary advantage of a Carry Look-Ahead Adder over a ripple-carry adder is its ability to generate carry bits in parallel, eliminating the need for a sequential carry propagation through each bit. This parallelism reduces the propagation delay, making the CLA faster for addition operations.

The main advantage of Pulse width modulation is that it has very low power loss in switching devices and higher frequency that affects the devices which uses power. Only digital circuits can produce PWM signals. In this paper counters are used to generate PWM signals which will be in the form of square wave [6]-[7]. The conventional method of generating the PWM pulses using analog circuitry have disadvantages of complex circuitry, limited function and low flexibility in circuit modification. Due to limitations offered by analog circuit designing, the digital methods of generating the pulses are getting more popularity [8]-[9]. Today basically engineers use various micro-controllers to make control system but these microcontrollers are being replaced by FPGA. The FPGA (FieldProgrammable Gate Array) allows user to have all features on a single chip. It is an array of programmable logic blocks which can be connected to each other by using Hardware Description Language. The most common HDL used are VERILOG and VHDL. This paper describes or propose how to generate PWM in Verilog for implementation on FPGA for further applications.FPGA Board, ISE software is necessary for this implementation[10]-[11]. 


Components:

Input Signals (A and B):

Two 8-bit binary numbers (A and B) are provided as inputs to the adder.
Carry-In Signal (Cin):

A carry-in signal (Cin) is an additional input that represents the carry bit from a previous stage or operation. It's used when chaining multiple adders together.
Generate (G), Propagate (P), and Carry (C) Signals:

For each bit position i (from 0 to 7 in an 8-bit adder), generate two signals:
Generate Signal (G[i]): The AND operation between the corresponding bits of A and B.
Propagate Signal (P[i]): The XOR operation between the corresponding bits of A and B.
Additionally, compute the carry signals C[i+1] in parallel using the formulas:
1.1STRATEGY FOR BUILDING CARRY LOOK AHEAD ADDER IN FPGA USING VERILOG:

Building an 8-bit Carry Look-Ahead Adder (CLA) in FPGA using Verilog involves several steps. Here's a strategy to guide you through the process:

1. Design the Carry Look-Ahead Adder Module:
Define a Verilog module for the 8-bit Carry Look-Ahead Adder. This module will include input ports for the two 8-bit binary numbers (A and B), a carry-in port (Cin), and output ports for the 8-bit sum (Sum) and carry-out (Cout). Implement the CLA logic inside the module.

2. Implement the Carry Look-Ahead Logic:
Inside the module, implement the generate (G), propagate (P), and carry (C) signals for each bit position. Use the generate and propagate signals to compute the carry bits for all bit positions in parallel. Finally, calculate the sum bits based on the propagate and carry signals.

3. Create a Testbench:
Write a Verilog testbench to verify the functionality of your Carry Look-Ahead Adder. Apply test vectors to the inputs and observe the outputs. Use $display or other simulation constructs to monitor the behavior of your design.

4. Simulate the Design:
Use a Verilog simulator (e.g., ModelSim, VCS) to simulate your design. Check for correct functionality and observe the waveform to ensure that the carry look-ahead logic is working as expected.

5. Synthesize and Implement on FPGA:
Synthesize your Verilog design using FPGA synthesis tools (e.g., Vivado, Quartus). Map the design to the target FPGA, assign pin locations, and generate a bitstream.

6. Hardware Testing:
Download the generated bitstream onto your FPGA board and test the Carry Look-Ahead Adder in hardware. Verify that it operates correctly for various test cases.

7. Optimization (Optional):
Optimize the design based on the FPGA's architecture and your performance requirements. Experiment with different synthesis and optimization settings to achieve the desired speed and resource utilization.

By following these steps, you can design, simulate, and implement an 8-bit Carry Look-Ahead Adder on an FPGA using Verilog. Adjust the specific details based on your FPGA vendor and tools.
 
1.2 IMPLEMENTATION OF VERILOG CODES IN XILINX:

When the codes are written in Xilinx one can get output waveforms on Model Sim as well as one can view the RTL schematic (Fig.2) so the RTL schematic which is shown below parts from Fig.3-Fig.6 which provides a brief overview of the functioning of our proposed CARRY LOOK AHEAD ADDER. The code used is mentioned in appendix in which the functionality is described of proposed design for 
CARRY LOOK AHEAD ADDER. Before we proceed its most important to understand that what is RTL (Register Transfer Level) schematic. RTL schematic tells us how our HDL code is interpreted and implemented. It helps to do analysis in one go and to derive actual wiring from higher level representation for lower leveldesign implementation. The detailed RTL schematic is bit complex but it is not so difficult to understand. Once if we look carefully to the RTL schematic we are able to understand how the proposed design is working. Basically Verilog is a hardware description language which is standardized as IEEE 1364 which is most commonly used for designing and verification of designed digital circuits,at the register transfer level (RTL). We have used Verilog instead of VHDL because of various advantages of Verilog over VHDL
                                             



   2.EXPERIMENTAL WORK:

2.1DESIGNMODULE:

module cla(
    input [7:0] A, B,
    input cin,
    output [7:0] sum,
    output cout
);

wire [7:0] G, P, C;

assign G = A & B;
assign P = A ^ B;
assign C[0] = cin;

generate
    genvar i;
    for (i = 0; i < 8; i = i + 1) begin : generate_CLA
        assign G[i] = A[i] & B[i];
        assign P[i] = A[i] ^ B[i];
        assign C[i+1] = G[i] | (P[i] & C[i]);
    end
endgenerate

assign sum = P ^ C;
assign cout = G[7] | (P[7] & C[7]);

endmodule

2.2 TESTBENCH MODULE:

`timescale 1ns/1ns

module cla_tb( );

reg [7:0] A, B;
reg cin;
wire [7:0] sum;
wire cout;

// Instantiate the CarryLookAheadAdder module
cla uut (
    .A(A),
    .B(B),
    .cin(cin),
    .sum(sum),
    .cout(cout)
);

// Initial block for test inputs
initial begin
    A = 8'b11011010;
    B = 8'b01101101;
    cin = 0;

    // Add some delay before applying inputs
    #10;

    // Display input values
    $display("Input A = %b", A);
    $display("Input B = %b", B);
    $display("Input cin = %b", cin);

    // Display initial output values
    #5 $display("Initial sum = %b, cout = %b", sum, cout);

    // Apply some additional delay before changing inputs
    #5;

    // Change inputs for the next test
    A = 8'b10101010;
    B = 8'b01010101;
    cin = 1;

    // Display updated input values
    $display("Input A = %b", A);
    $display("Input B = %b", B);
    $display("Input cin = %b", cin);

    // Display output values after the second set of inputs
    #5 $display("Final sum = %b, cout = %b", sum, cout);

    // Add more test cases as needed
    // ...

    // Stop the simulation
    $stop;
end

endmodule

3.EXPERIMENTAL PROCEDURE:

Step-1: Open Vivado and click on “create project” and click “next”
                                      
                             

Step-2: : Create a RTL project







Step-3: Add design source



Step-3: Give a file name


Step-4: Give all the specifications





Step-5: Add input and output ports


Step-6: Write the code





Step-7: Add simulation sources


Step-8: Create a testbench file






Step-9: Add input and output ports and write testbench code



Step-10: Run behavioural simulation




RESULTS

4.1 RTL SCHEMATIC

4.2 SIMULATED WAVEFORMS:


4.3 IMPLEMENTATION  SCHEMATIC
	

                                 Fig 4.4: Technology Implementation schematic

        ​ 
  4.4 POWER REPORT:



                                                                  Fig 4.5: power report

4.5 UTILIZATION REPORT:




Fig 4.6: utilization report

        ​ 4.6 NOISE REPORT:




Fig 4.7: Noise report

4.7 TIMING REPORT:


   





5. CONCLUSION AND FUTURE SCOPE	
  In conclusion, the Carry Look-Ahead Adder (CLA) is a powerful digital circuit designed to perform binary addition with a focus on reducing the propagation delay associated with generating carry bits. Here are some key points to conclude:
Parallel Carry Calculation
Generate (G) and Propagate (P) Signals
Carry Generation
Sum Calculation
Verilog or VHDL can be used to describe and simulate the Carry Look-Ahead Adder.
FPGA synthesis tools can be employed to implement the design on specific FPGA platforms.
In summary, the Carry Look-Ahead Adder is a key component in digital arithmetic circuits, offering a balance between speed and hardware complexity. Its parallel carry calculation makes it suitable for applications where minimizing propagation delay is critical, such as in high-performance computing systems.
6. REFERENCES
https://history-computer.com/analytical-engine-history-of-charles-babbage-analytical
engine/
