# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

ALU.v :
~~~
module ALU_32_bit(y,a,b,f);
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
~~~
RUN.tcl :
~~~
read_libs /cadence/install/FOUNDRY-01/digital/90nm/dig/lib/slow.lib
read_hdl ALU_32_bit.v
elaborate
 
syn_generic
report_area
syn_map
report_area
syn_opt
report_area 

report_area > ALU_32_bit_area.txt
report_power > ALU_32_bit_power.txt
report_area > ALU_32_bit_cell.txt
report_gates > ALU_32_bit_gates.txt

write_hdl > ALU_32_bit_netlist.v

gui_show
~~~
### Step 2 : Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :
![Screenshot 2025-05-20 141729](https://github.com/user-attachments/assets/447b3b5a-d06c-4a32-9c67-2e6cc6da33c0)


#### Area report:
![Screenshot 2025-05-20 141814](https://github.com/user-attachments/assets/ed5e6562-b76b-49c2-95ff-32acfa0eece5)


#### Power Report:
![Screenshot 2025-05-20 141848](https://github.com/user-attachments/assets/a30db11b-622f-4254-955a-e24069b3c8f9)


#### Result: 

The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
