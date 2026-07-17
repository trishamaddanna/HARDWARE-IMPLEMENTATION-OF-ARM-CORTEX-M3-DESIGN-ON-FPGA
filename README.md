# HARDWARE-IMPLEMENTATION-OF-ARM-CORTEX-M3-DESIGN-ON-FPGA
The Cortex-M3 processor is designed for high-performance, cost-effective platforms across a wide range of applications, including microcontrollers, automotive body systems, industrial control systems, and sensors. It is specifically chosen for its classification as a microcontroller processor from ARM, making it suitable for embedded IoT applications. The System-on-Chip (SoC) design integrates the ARM Cortex-M3 32-bit processor, with a customized IoT subsystem and peripherals on an FPGA. The design is tailored to meet specific requirements and specifications, ensuring chip functionality validation on the Xilinx FPGA platform, which was previously implemented on an Intel FPGA. The existing design had a limited number of master and slave ports for interfacing peripherals. The customization of peripherals is, to increase the number of master and slave ports by modifying the AHB and APB interconnects while modifying memory mapping of the ports to our specification, using an address decoding logic. FPGA prototyping is done to validate the test cases again for the modified Cortex-M3 Design on the Xilinx platform. The Keil uVision5 software is used to translate C-programs into binary files that is loaded into the SoC's Memory for the processor to run and Xilinx Vivado is used for simulation. The Hardware implementation is done on the Arty100– T FPGA platform to  test and verify the functionality of the chip.     

PROPOSED METHODOLOGY 

Customization of peripherals to increase the number of master and slave ports by modifying the AHB and APB interconnects [3]: 
•	Replacing existing peripherals to add design features. 
•	Digital peripherals like: General purpose Input Output (GPIO) pins; Timers; Pulse Width Modulator (PWM) – usually for motor or power electronic system control; UART for serial communication; SPI (Serial Peripheral Interface) for external hardware modules  such as LCDs; I2C / I3C – commonly used for sensors. 
•	Tightly-coupled timer peripherals – There are two Advanced Peripheral Bus (APB) timer modules that are instantiated within the subsystem hierarchy in Cortex-M3 Design. These APB timers are reserved for the operating system. 
•	Tightly-Coupled Memory interfaces - There are four AHB to SRAM interface modules instantiated within the subsystem hierarchy in the CortexM3 Design. This multi-bank memory configuration gives the fastest possible access. The IoT subsystem can be configured to provide 1, 2, 3 or 4 banks of SRAM. 
•	Primary code memory - In the subsystem included with the CortexM3 Design, there is a dedicated AHB interface that provides access to flash storage. The block RAM is preloaded in simulation with the executable code. For the SoC implementation, it will be necessary to replace the block RAM with a suitable equivalent, either SRAM or a flash interface. 
•	Closely coupled peripherals - The subsystem in Cortex-M3 Design provides APB master expansion ports used in the example system for UARTs, additional timers, Watchdog, Real Time Clock (RTC), and True Random Number Generator (TRNG). The remaining five APB master expansion ports can be used for communications interfaces, or other peripherals with a low latency requirement. There are six reserved interrupt lines that are suitable for additional peripherals.
•	Adding peripherals to memory map - In the IoT subsystem included with the Cortex- M3 Design, both the APB expansion and the FPGA peripheral APB interfaces have unused ports that can be used to add peripherals, without any modifications. If these ports are not sufficient and an existing peripheral cannot be replaced, we are required to modify at least one of the AHB interconnects in the system.
•	Memory map definition - The architectures used in the Cortex-M3 processor defines a memory map that allocates address ranges into regions. This allows the built-in peripherals like the interrupt controller and debug components to be accessed  by  simple memory access instructions, allowing system features to be accessible in the C program code
The memory mapping is modified according to our specification. The modification is done using an address decoding logic.

Features of Modified Interconnect Platform in the Cortex M3 Design: 

•	The AHB and APB Interconnects are modified by adding new slave ports and have to be memory mapped to the system by modifying memory mapping to our specification. The modification is done using an address decoding logic i.e the CPU address comes, based on which it decides which one of the slave gets access. 
•	Based on the decoder value, the slave is selected (for eg: the APB decoder has a particular set of bits toggling from 1 memory space to another, differentiating for the ports to select APB slave, whereas in AHB decoder, all 32 bits are used for selecting the slave). 
•	The AHB and the APB Interconnects
platforms are extended to 18 ports. 
•	The input and output ports are modified to more than 15 ports which were 8 ports initially. 
•	The slaves may be SRAM, UART or GPIO according to the requirements or specifications. 
•	The SRAM instantiates dedicated block RAMs and 1 bank of SRAM is designed. 
•	The SRAMs are designed for 128KB for more memory capacity and Flash memory is modified from 256KB to 512KB. 

Implementation of Modified ARM Cortex-M3 Design on Xilinx FPGA (Steps): 

•	In the existing design, the functionalities were verified in Intel FPGA whereas in the proposed design, the functionalities are verified in Xilinx FPGA. 
•	FPGA prototyping is done to validate the testcases again for the modified Cortex-M3 design on the Xilinx platform. 
•	During the FPGA flow - the clock is replaced with Mixed-Mode Clock Manager (MMCM) which takes reference clock from board and generates clock frequency required. 
•	The Keil uVision 5 software is used to translate the C-programs into binary files that is loaded into the SoC's Memory for the processor to run and Xilinx Vivado is used for simulation. 
•	The Hardware implementation is done on the Arty 100 - T FPGA platform to test and verify the functionality of the chip. 
•	This involves the process of generating the Bit file, programming FPGA Board, after giving reset to CPU, the application code gets executed from Flash memory. 
•	The programmed software algorithm is ARM mbed into the programmed FPGA board and it prints the output infinite times on the monitor screen. 
 
RESULTS AND DISCUSSIONS  
 
FPGA prototyping is done to validate the test cases again for the modified Cortex-M3 design on the Xilinx platform. During the FPGA flow – the clock is replaced with Mixed- Mode Clock Manager (MMCM) which acts a reference clock from FPGA board and generates required clock frequency. 

The Total on-chip Power analysis from implemented netlist is 0.368W. The dynamic power consumption is 0.265W and has a static consumption of 0.103W.

The Cortex-M3 includes packages such as RTL, Execution Test bench, and FPGA Evaluation Flow. The three pipeline stages in Cortex M3 are Instruction fetch, Instruction decode and Instruction execution. The Cortex M3 has integrated sleep modes, that can be entered using WFI or WFE instructions. It also has separate clocks for essential blocks. 
 
The Hardware Implementation Is done on the Arty 100 – T FPGA platform to test and verify the functionality of the chip. This involves the process of generating the Bit file, programming FPGA Board, after giving reset to CPU, the application code gets executed from Flash memory. The programmed software algorithm is ARM mbed into the programmed FPGA board and it prints the output infinite times on the monitor screen.
