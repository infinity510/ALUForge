# ALUForge

ALUForge is a custom single-core CPU designed from scratch. The project focuses on building a full-fledged processor architecture from the ground up, including the design of the Arithmetic Logic Unit (ALU), datapath, control unit, and a custom Instruction Set Architecture (ISA).

## Key Features

- **Registers**: Built with three primary working registers:
  - **ACC (Accumulator)**: Acts as the primary register for arithmetic and logic results.
  - **A & B**: General-purpose registers for storing operands.
- **Instruction Set Architecture (ISA)**: Supports multiple instruction formats for flexibility:
  - **0-address**: Implicit operands (e.g., operations working directly on the Accumulator).
  - **1-address**: Single explicit operand.
  - **2-address**: Two explicit operands (typically source and destination).
  - **3-address**: Three explicit operands (two sources and one destination).
- **Supported Operations**: Includes essential instructions like `MOV` (data transfer), `ADD`, `SUB`, `MUL`, and `DIV`.

## Circuit Diagrams & Modules Completed

The digital logic design is implemented using Logisim (saved as `.circ` files). The development follows a modular approach, starting from basic memory elements and progressing to complex arithmetic components. The following modules have been completed:

### 1. Memory and Registers (`register.circ`)
- **Dflipflop**: The foundational 1-bit memory cell (D-type flip-flop) built using logic gates.
- **registor**: A multi-bit register module constructed by cascading `Dflipflop` instances. This forms the basis for the CPU's ACC, A, and B registers.

### 2. Arithmetic Logic Unit (ALU) Components
Arithmetic components are divided across multiple circuit files to ensure modularity and ease of testing.
- **Addition (`FinalCircuit.circ`)**:
  - **ADD_full / SUM**: A standard 1-bit full adder to compute the sum and carry of two bits.
  - **ADD**: A multi-bit ripple-carry adder that combines several `ADD_full` units.
- **Subtraction (`FullSubtracter.circ`)**:
  - **Full_Subtracter & mainFullSubtracter**: Dedicated circuits that handle multi-bit subtraction using borrow logic.
- **Complement & Utilities (`FinalCircuit.circ`)**:
  - **Rcomp**: A complement module designed to facilitate 1's or 2's complement operations, which are essential for subtraction and handling negative binary numbers.

### 3. Control Unit & Top-Level Integration (`FinalCircuit.circ`)
- **decode**: The instruction decoder module. It takes the binary instruction format, determines the addressing mode (0, 1, 2, or 3-address), and asserts the correct control signals across the CPU.
- **ALUForge**: The top-level master circuit. This integrates the ALU components, the registers, and the instruction decoder, completing the datapath and routing the control signals to orchestrate the CPU's execution cycle.

## Architecture Block Diagram
Below is a high-level conceptual overview of the ALUForge datapath and control unit interactions:

```mermaid
flowchart TD
    Bus{Data Bus / Multiplexers}
    Decoder[Instruction Decoder] -->|Control Signals| ALU
    Decoder -->|Read/Write Enable| Regs
    
    subgraph Regs[CPU Registers]
        ACC[ACC - Accumulator]
        RegA[Register A]
        RegB[Register B]
    end

    Regs <-->|Data| Bus
    Bus -->|Operands| ALU(Arithmetic Logic Unit)
    ALU -->|Computation Result| ACC
    
    %% Annotations
    ALU -.->|Performs| Add[ADD / SUB / MUL / DIV]
```

## Schematic Diagrams (Logisim)

> **Note:** The actual schematics are stored in `.circ` files which are XML-based logic models for Logisim. To view these exactly as they look in the simulator, you can open the project in Logisim. 

*(Placeholders for exported images: To display your actual circuit diagrams below, export them as PNGs from Logisim and save them to an `images` folder in this repository, then update the paths).*

### ALUForge Top-Level Datapath
<!-- ![ALUForge Top Circuit](images/ALUForge.png) -->

### 1-Bit Full Adder
<!-- ![Full Adder](images/ADD_full.png) -->

### Register / Memory Block
<!-- ![Register](images/registor.png) -->
