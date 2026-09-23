# DVCon - Hardware Accelerator

## Overview
DVCon is a parameterized Neural Network Hardware Accelerator designed in SystemVerilog. It is built around a Systolic Array architecture optimized for matrix multiplication operations, featuring custom memory hierarchy (BRAM buffers), an instruction FIFO, and a Vector Unit with a SiLU (Sigmoid Linear Unit) look-up table (LUT) for non-linear activation functions. 

The accelerator communicates with a host processor or memory subsystem via industry-standard **AXI4** interfaces:
- **AXI4-Lite Slave**: Used for configuration, control, and status registers.
- **AXI4 Master**: Used for high-bandwidth DMA transfers of weights, biases, and activations from/to main memory.

## Architecture Highlights
- **Systolic Array**: A 2D array of Processing Elements (PEs) designed for high-throughput MAC (Multiply-Accumulate) operations.
- **On-chip BRAM Buffers**:
  - `bram_act_buffer`: Stores input activations.
  - `bram_weight_buffer`: Stores network weights.
  - `bram_bias_buffer`: Stores biases.
  - `bram_accum_buffer`: Stores intermediate accumulation results.
  - `bram_out_buffer`: Stores final output results.
- **Vector Unit**: Performs element-wise vector operations and applies the SiLU activation function via `silu_lut`.
- **Control Unit**: Fetches and decodes instructions from `instructions_fifo` and orchestrates data movement and computation across the systolic array and vector unit.

## Directory Structure
- `rtl/`: Contains all synthesizable SystemVerilog design files (e.g., `accelerator.sv`, `systolic_array.sv`, `pe.sv`, `axi4_master.sv`).
- `tb/`: Contains the comprehensive testbench suite for module-level and system-level verification (e.g., `tb_accelerator.sv`, `tb_systolic_array.sv`).
- `documentation/`: Detailed documentation and specifications.
- `patches/`: Patch files and updates for the project.

## Key Parameters
The top-level `accelerator` module can be configured via parameters:
- `DATA_WIDTH`: Width of the data paths (default: 8-bit).
- `ADDR_WIDTH`: Width of the memory addresses (default: 64-bit).
- `INSTR_WINDOW_SIZE`: Size of the instruction window (default: 4).
- `SYSTOLIC_ARRAY_ROWS`: Number of rows/columns in the systolic array (default: 32).

## Getting Started
To simulate the design, you can use any standard SystemVerilog simulator (e.g., ModelSim, Questa, Vivado Simulator, Verilator).
1. Add all files in the `rtl/` directory to your project.
2. Add the desired testbench from the `tb/` directory as your top-level simulation module.
3. Run the simulation and observe the waveforms or terminal outputs.

## License
*Please specify the license for this project here.*
