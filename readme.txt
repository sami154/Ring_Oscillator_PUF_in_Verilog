Folder Description:
ro_puf- generated custom ro-puf ip core for puf_soc project.


Project Description:

We evaluated our RO-puf design on the Xilinx FPGA platform. 

Verilog Module Description:

top_module.v: This is the top verilog file of the RO-PUF
dispModule.v: This module muxes the 64 bit PUF response to the 4 bit output of the RO-PUF.
Mux64to1.v: This module selects the indexed RO to the output depending on the input.
ro_unit.v: code for 5 stage ring oscillator.
NOTFUNC.v: not gate.
NANDFUNC.v: 2 input NAND. It replaces one of the not gate to facilitate enable pin.
