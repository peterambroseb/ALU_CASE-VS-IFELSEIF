# Exp 4 Comparative Study of 32-Bit ALU Implementations Using Case and If-Else Constructs

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
module alu_case(y,a,b,f); 
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin 
case(f)
3'b000:y=a&b;		//AND Operation
3'b001:y=a|b;		//OR Operation
3'b010:y=~(a&b);	//NAND Operation
3'b011:y=~(a|b);	//NOR Operation
3'b100:y=a^b;    	//XOR Operation
3'b101:y=a+b;		//Addition
3'b110:y=a-b;		//Subtraction
3'b111:y=a*b;		//Multiply 
default:y=32'bx;
endcase
end 
endmodule

```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Creating a Test Bench:
Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_case_tb.v).

#### Test Bench :
```
module alu_case_tb; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_case dut(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; 
b=32'h00110001; 
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
y=a&b;			//AND Operation 
else if (f==3'b001)
y=a|b;	         	//OR Operation
else if (f==3'b010)
y=~(a&b);        	//NAND Operation
else if (f==3'b011)
y=~(a|b);		//NOR Operation
else if (f==3'b100)
y=a^b;			//XOR Operation
else if (f==3'b101)
y=a+b;        		//Addition
 else if (f==3'b110)
y=a-b;			//Subtraction 
else if (f==3'b111)
y=a*b;			//Multiply 
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
begin a=32'h00000000; 
b=32'h00110001; 
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
end initial
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

<img width="1920" height="1080" alt="Screenshot (148)" src="https://github.com/user-attachments/assets/8a84da3d-295d-40ab-a2fa-13c2dff8b3d0" />


#### Fig 2: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.

Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.

<img width="1920" height="1080" alt="Screenshot (151)" src="https://github.com/user-attachments/assets/565ec125-0141-4577-97bf-469c7b0e7f7b" />


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

<img width="1920" height="1080" alt="Screenshot (152)" src="https://github.com/user-attachments/assets/47d5c990-f44f-4a80-8091-1cb6f372f835" />

#### Fig 4: Compiled database in WorkLib
After compilation, it will come under worklib. You can see on the right side window

select the test bench and compile it. It will come under Worklib. Under Worklib, you can see the module and test bench.

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”

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

<img width="1920" height="1080" alt="Screenshot (153)" src="https://github.com/user-attachments/assets/604a7f4c-81d7-4e92-8c59-1beccbd77641" />


#### Fig 5: Elaboration Launch Option

#### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options

<img width="1920" height="1080" alt="Screenshot (154)" src="https://github.com/user-attachments/assets/d6ad667d-d8bc-459f-bc99-5edcc3d35da8" />

#### Fig 6: Design Browser window for simulation

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (155)" src="https://github.com/user-attachments/assets/b8a8a935-34f8-4b96-ac23-ead23c92c938" />

#### ALU IFELSE:
<img width="1920" height="1080" alt="Screenshot (170)" src="https://github.com/user-attachments/assets/695a3eee-df01-4cbe-941c-dc53ebaf430c" />


#### Fig 7: Simulation Waveform Window

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

##### Performing Synthesis

##### Synthesize Design

Run the synthesis Process one time for each code and make sure the output File names are changed accordingly

The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (156)" src="https://github.com/user-attachments/assets/c11db41f-a153-41d1-9250-1457d8a7a8e7" />

#### ALU IFELSEIF:
<img width="1920" height="1080" alt="Screenshot (171)" src="https://github.com/user-attachments/assets/33cdc6b3-a375-4cf8-90d3-a1a7786afaa0" />


#### Fig 8: Synthesis RTL Schematic using case and ifelseif construct

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (172)" src="https://github.com/user-attachments/assets/e3e45fb9-ef86-4ec6-8499-47a7079aea15" />


#### ALU IFELSEIF:
<img width="1920" height="1080" alt="Screenshot (175)" src="https://github.com/user-attachments/assets/fc65ca30-9077-4c9b-a4fe-edc34bbec0db" />


#### Fig 9: Area report of case and ifelseif construct

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (173)" src="https://github.com/user-attachments/assets/1e949814-d292-4528-b770-c7eaea14ae2f" />


#### ALU IFELSEIF:
<img width="1920" height="1080" alt="Screenshot (176)" src="https://github.com/user-attachments/assets/0178cb44-7534-4ec0-aef5-b89b8464e1bb" />


#### Fig 10: Power Report of case and ifelseif construct

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (174)" src="https://github.com/user-attachments/assets/cb4a2af4-5282-43fc-9dea-2c04d69ad0bb" />


#### ALU IFELSEIF:
<img width="1920" height="1080" alt="Screenshot (177)" src="https://github.com/user-attachments/assets/d72d5a6f-08e5-4f16-bf48-4723b61f50eb" />

#### Fig 11: Timing Report of case and ifelseif construct



<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/3d449925-3dee-4288-8f57-61dfc83d5452" />

#### Fig 12: Tabulate Area,Power and Timing Report Comparision of ALU using case and ifelseif construct

## Result
The 32-bit ALU implemented using behavioural case statements and if–elseif constructs was successfully verified under Incisive (ncvlog/ncsim) for all tested vectors.A comparative analysis revealed that the case-statement-based ALU and the if–elseif-based ALU exhibited identical area and power consumption have no differnce Both implementations were functionally correct and synthesizable Both designs, however, produced identical functional outputs.
