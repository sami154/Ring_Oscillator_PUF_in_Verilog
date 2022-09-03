
Hardware Requirement:
    Zybo z7 10
Software Requirement:
    Vivado Design Suite 2018.2


Folder Hierarchy:

The project directory has the following folders:

1. finalprojectGroup4- standalone ropuf project


2. puf_soc - SoC project with the custom ro-puf IP core from 1.


3. ro_puf- generated custom ro-puf ip core for puf_soc project.


Project Description:

We evaluated our RO-puf design on the Xilinx FPGA platform. We generated two separate projects to evaluate our RO-PUF. 

1. In the <finalprojectGroup4> we implemented our ro-puf as a standalone project. The inputs are taken from the switches on the board and the responses are mapped to the on board leds. Here used the 4 push buttons as selectors to mux 64 bit response to the 4 bit leds. Please see the attached demo video for more information. 

How to Run this project:

- Browse to the finalprojectGroup4 directory and double click on the finalprojectGroup4.xpr file. This should open the project on vivado.
- The bitstream is already generated. Connect the above mentioned FPGA board to the computer through usb. Open hardware manager and program the device.
- Switch G15 on the board is used for the enable signal. Make it high to see RO-PUF response directly on the LED.
- These are the first 4 LSB of the PUF response. Use the push buttons to see responses of other bits.
    Bit map:
    <push 0000> = [3][2][1][0]  //led showing bit response of 
    <push 0001> = [7][6][5][4]
    .
    ..
    <push 1111> = [63][62][61][60]


Switch T16 and W13 are used to apply challenges in the PUF. It means we can apply 4 challenges to the RO-PUF and generate 4 distinct output. Please refer to the video for more details.


2. In the <puf_soc> project. We implemented the RO-PUF in SoC with a zynq processor. The PUF module’s input and output pins are mapped to AXI GPIO ports to map it to the memory mapped IO. Therefore, the processor can write challenges and read response and show the results on UART.

How to Run this project:

- Browse to the <puf_soc> directory and open the project.
- The bitstream is already generated generated. Go to File and launch SDK.
- Open TeraTerm and connect to the COM port where the zybo board is hooked.
    Baud Rate: 115200
- Now assert Xilinx→ <Program FPGA> to program the FPGA.  
- Once completed assert Run→ Run Configurations.
- On the pop-up window select <GDB Debug on Local> and apply Run. You should see response for different challenges in the uart port.


Verilog Module Description:

top_module.v: This is the top verilog file of the RO-PUF
dispModule.v: This module muxes the 64 bit PUF response to the 4 bit output of the RO-PUF.
Mux64to1.v: This module selects the indexed RO to the output depending on the input.
ro_unit.v: code for 5 stage ring oscillator.
NOTFUNC.v: not gate.
NANDFUNC.v: 2 input NAND. It replaces one of the not gate to facilitate enable pin.
