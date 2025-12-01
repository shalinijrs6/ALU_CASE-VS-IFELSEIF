# Exp 4 Comparative Study of 32-Bit ALU Implementations Using Case and If-Else Constructs.

## Aim: 
Write a Verilog code for 32 32-bit ALU supporting four logical and four arithmetic operations, use case statement and if statement for ALU behavioral modeling. 

To verify the Functionality using Test Bench 

Synthesize and compare the results using if and case statements 

Identify Critical Path and constraints

## Tool Required: 
 Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim) 

 Synthesis: Genus 

## Design Information and Block Diagram: 
The ALU will take in two 32-bit values and a control line. An Arithmetic unit does the following tasks like addition, subtraction, multiplication and logical operations. As the input is given in 32-bit, we get a 32-bit output. The arithmetic will show only one output at a time, so a selector is necessary to select one of the operators. 

 <img width="668" height="344" alt="image" src="https://github.com/user-attachments/assets/b5f95c0d-1fd6-4c3c-9a35-11eb9c86cba3" />

#### Figure No 1: Block Diagram of 32 Bit ALU 

## Creating a Workspace:
Create a folder in your name (Note: Give the folder name without any spaces) and create a new sub-directory named Exp4 or alu_bl_model for the design. Then, open a terminal from the Sub-Directory.

## Creating Source Codes
In the Terminal window, type gedit <filename>.v (ex: gedit alu_case.v).

A Blank Document opens up into which the following source code can be typed.

(Note: File name should be with HDL Extension)

To verify the Functionality using the Test Bench

#### Source Code – Using Case Statement :
```
module alu_32bit_case(y,a,b,f);
input [31:0]a;
input [31:0]b;
input [2:0]f;
output reg [31:0]y;
always@(*)
begin
case(f)
3'b000:y=a&b; //AND Operation
3'b001:y=a|b; //OR Operation
3'b010:y=~(a&b); //NAND Operation
3'b011:y=~(a|b); //NOR Operation
3'b100:y=a^b; //XOR Operation
3'b101:y=~(a^b); //XNOR Operation
3'b110:y=~a; //NOT of a
3'b111:y=~b; //NOT of b
endcase
end
endmodule
```
Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Creating a Test Bench:
Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_case_tb.v).

#### Test Bench :
```
module alu_32bit_tb_case;
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_32bit_case test2(.y(y),.a(a),.b(b),.f(f));
initial
begin
a=32'h00000000;
b=32'h10101010;
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
#50 $finish;
end
endmodule
```
Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Source Code - Using If Statement :
```
module alu_ifelseif(y,a,b,f);
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin
if(f==3'b000)
y=a&b;	               //AND Operation 
else if (f==3'b001)
y=a|b;	              //OR Operation
else if (f==3'b010)
y=~(a&b);	      //NAND Operation
else if (f==3'b011)
y=~(a|b);	      //NOR Operation
else if (f==3'b100)
y=~(a^b);	      //XOR Operation
 else if (f==3'b101)
y=a+b;                //Addition
 else if (f==3'b110)
y=a-b;	              //Subtraction 
else if (f==3'b111)
y=a*b;	              //Multiply 
else
y=32'bx; 
end 
endmodule
```

#### Test Bench :
```
module alu_ifelseif_tb; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_ifelseif dut(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; b=32'h00100001; 
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
end 
initial
#100 $finish; 
endmodule
```

Functional Simulation for each design

Invoke the cadence environment by typing the commands below

tcsh (Invokes C-Shell)

source /cadence/install/cshrc (mention the path of the tools)

(The path of cshrc could vary depending on the installation destination)

After this, you can see the window like below

To Launch the Simulation tool

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG

It will invoke the nclaunch window for functional simulation. We can compile, elaborate and simulate it using Multiple Steps.

Setting Multi-step simulation

Select Multiple Step and then select “Create cds.lib File” as shown in the figure below

Click the .cds.lib file and save the file by clicking on the Save option

Fcds.lib file Creation

Save .lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used.

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in the figure below.

We are simulating a verilog design without using any libraries

Click “OK” in the “nclaunch: Open Design Directory” window, as shown in the figure below

<img width="1920" height="1080" alt="Screenshot 2025-10-07 145531" src="https://github.com/user-attachments/assets/1d31f756-12fd-47c8-8f85-6ef996da917a" />


#### Fig 2: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.

Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.
<img width="1920" height="1080" alt="Screenshot 2025-10-07 145541" src="https://github.com/user-attachments/assets/adee1dd1-076e-45e4-b816-1bd65232774b" />

#### Fig 3: Nclaunch Window

#### Step 1: Compilation:
– Process to check the correct Verilog language syntax and usage

Inputs: Supplied are Verilog design and test bench codes

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file

#####  Steps for compilation:
	Create work/library directory (most of the latest simulation tools creates automatically)
 
	Map the work to library created (most of the latest simulation tools creates automatically)
 
 Run the compile command with compile options
 
i.e Cadence IES command for compile: ncverilog +access+rwc -compile filename.v

Left side select the file and in Tools: launch verilog compiler with current selection will get enable. Click it to compile the code

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation

<img width="1920" height="1080" alt="Screenshot 2025-10-07 145556" src="https://github.com/user-attachments/assets/f8a57075-d0fd-45c9-a3b1-34079f9dfd78" />

#### Fig 4: Compiled database in WorkLib
After compilation, it will come under worklib. You can see on the right side window

select the test bench and compile it. It will come under Worklib. Under Worklib, you can see the module and test bench.

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”
<img width="1920" height="1080" alt="Screenshot 2025-10-07 145645" src="https://github.com/user-attachments/assets/7d64884b-4188-4301-87b4-3dcea9064fb0" />

![WhatsApp Image 2025-11-17 at 08 55 22_a6a05b44](https://github.com/user-attachments/assets/9451d44c-96e2-49ed-9a1a-b56fd59c7a0c)


#### Step 2: Elaboration:
To check the port connections in a hierarchical design

Inputs: Top-level design/test bench Verilog codes

Outputs: Elaborate database updated in the mapped library if successful, generates a report, else error reported in the log file

#####  Steps for elaboration

– Run the elaboration command with elaborate options

1.It builds the module hierarchy

2. Binds modules to module instances
   
3.Computes parameter values

4. Checks for hierarchical name conflicts
   
5.It also establishes net connectivity and prepares all of this for simulation

After elaboration, the file will come under snapshot. Select the test bench and simulate it.

#### Fig 5: Elaboration Launch Option
<img width="1920" height="1080" alt="Screenshot 2025-10-07 145645" src="https://github.com/user-attachments/assets/9df1a6ab-99fc-4348-b7e3-e84c4ff96253" />

![WhatsApp Image 2025-11-17 at 08 58 02_6fcce81d](https://github.com/user-attachments/assets/4db95edb-cd6c-43f8-9a40-985c6b7efcf3)

#### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options

<img width="1920" height="1080" alt="Screenshot 2025-10-07 145701" src="https://github.com/user-attachments/assets/b2e763e2-78a6-4430-97b4-4623a8cd2446" />

<img width="1920" height="1080" alt="Screenshot 2025-10-25 090329" src="https://github.com/user-attachments/assets/57b636e5-d69f-49a8-adb0-f2c5644c666b" />


#### Fig 6: Design Browser window for simulation
<img width="1920" height="1080" alt="Screenshot 2025-10-07 145828" src="https://github.com/user-attachments/assets/6f03b645-1253-4546-86be-8421c85752b7" />

![WhatsApp Image 2025-11-17 at 09 00 18_d5a7b2e0](https://github.com/user-attachments/assets/c42a3a94-83b0-47bf-bacd-ea8592f5f73e)


#### Fig 7: Simulation Waveform Window

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)
<img width="1920" height="1080" alt="Screenshot 2025-10-04 092953" src="https://github.com/user-attachments/assets/2331355d-8563-4ad1-b990-8319ae387520" />

![WhatsApp Image 2025-11-17 at 09 07 33_5305fa08](https://github.com/user-attachments/assets/3009549f-ab8c-40fc-9a34-35079ae3ac27)

##### Performing Synthesis

##### Synthesize Design

Run the synthesis Process one time for each code and make sure the output File names are changed accordingly

The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.

<img width="1602" height="877" alt="image" src="https://github.com/user-attachments/assets/4e6f1604-98e8-4381-b5f2-9cc1d80f3411" />


![WhatsApp Image 2025-11-17 at 09 10 58_85fcf726](https://github.com/user-attachments/assets/92793fd8-7558-4d63-9999-d3afb1317d7b)

#### Fig 8: Synthesis RTL Schematic using case and ifelseif construct
<img width="1920" height="1080" alt="Screenshot 2025-10-04 094132" src="https://github.com/user-attachments/assets/715f6870-51e7-4427-ab69-4d9ebc44ae41" />

![WhatsApp Image 2025-11-17 at 09 11 42_dbc30ca7](https://github.com/user-attachments/assets/c719ed7d-b294-4bca-b595-cdd3ba99d38d)

#### Fig 9: Area report of case and ifelseif construct
<img width="1920" height="1080" alt="Screenshot 2025-10-04 094243" src="https://github.com/user-attachments/assets/ab274a2e-6da7-429c-bc59-3ddccc7806a2" />

![WhatsApp Image 2025-11-17 at 09 28 44_ace05534](https://github.com/user-attachments/assets/66a14bdf-bf4d-4483-91e2-49d7112338be)

#### Fig 10: Power Report of case and ifelseif construct
<img width="1920" height="1080" alt="Screenshot 2025-10-04 094554" src="https://github.com/user-attachments/assets/84b519d1-caa7-48cc-8fd2-2710828bef08" />

![WhatsApp Image 2025-11-17 at 09 29 20_a459f804](https://github.com/user-attachments/assets/3a90ff76-5705-443a-bce4-c89b98421f95)

#### Fig 11: Timing Report of case and ifelseif construct

<img width="1105" height="499" alt="Screenshot 2025-11-17 105338" src="https://github.com/user-attachments/assets/ca91c0a5-9bda-4dba-80bb-65b9c183017b" />


#### Fig 12: Tabulate Area,Power and Timing Report Comparision of ALU using case and ifelseif construct

## Result
The 32-bit ALU implemented using behavioural case statements and if–elseif constructs was successfully verified under Incisive (ncvlog/ncsim) for all tested vectors. Both implementations were functionally correct and synthesizable. Synthesis using Cadence Genus generated gate-level netlists along with area, timing, and power reports.
A comparative analysis revealed that the case-statement-based ALU resulted in slightly lower area and better timing performance, while the if–elseif-based ALU exhibited higher logic complexity and marginally increased delay due to sequential decision evaluation. Both designs, however, produced identical functional outputs.
