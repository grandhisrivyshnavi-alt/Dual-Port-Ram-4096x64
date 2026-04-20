
# 🧠 Dual Port RAM Verification using SystemVerilog (SV TB)

## 📌 Overview

This project implements a **4096 × 64 Dual Port RAM** along with a **SystemVerilog-based layered testbench** to verify its functionality.
The verification environment is built using **object-oriented methodology (without UVM)** and achieves **100% functional coverage through regression testing** using extended test scenarios .


## 🏗️ Design Architecture

### 🔹 RTL Design

The design consists of:

* `dual_mem` → Basic memory block (1024 depth)
* `mem_dec` → Address decoder
* `ram_4096` → Top module (4 banks of memory)

### 🔹 Key Features

* 64-bit data width
* 4096 memory locations
* Independent read & write operations
* Bank-based architecture using decoder
* Tri-state output handling


## 🧪 Verification Architecture

The testbench follows a **layered architecture** with modular components:

### 🔹 Components Description

* **Generator**

  * Generates randomized transactions
  * Sends data to read & write drivers via mailboxes

* **Drivers**

  * Write Driver → Drives write operations
  * Read Driver → Drives read operations

* **Monitors**

  * Capture DUT signals
  * Convert them into transactions

* **Reference Model**

  * Golden model using associative array
  * Mimics DUT behavior

* **Scoreboard**

  * Compares DUT output with reference model
  * Tracks correctness and triggers completion
  * Includes **functional coverage model**


## 🔁 Transaction Flow

Generator → Drivers → DUT → Monitors → Reference Model → Scoreboard

This ensures **end-to-end data integrity checking**.


## 🎯 Transaction Class Features

* Randomized fields:

  * `data`, `rd_address`, `wr_address`, `read`, `write`
* Constraints:

  * Read/Write cannot both be zero
  * Read and Write addresses must differ
  * Valid data range
* Built-in:

  * Transaction counters
  * Display method
  * Compare method (used in scoreboard)


## 📊 Functional Coverage

Implemented inside the **Scoreboard**:

* Coverpoints:

  * Read signal
  * Read address (bucketed ranges)
  * Data output ranges
* Cross coverage:

  * Read × Address

### ✅ Result

* Achieved **100% functional coverage**
* Coverage holes filled using **extended transaction classes**


## 🧪 Test Strategy

### 🔹 Base Test

* Random transactions
* Valid constraints

### 🔹 Extended Tests (Regression)

#### ✅ Test 1 (Base Test)

* Standard random testing

#### ✅ Test 2 (Extended Transaction 1)

* Covers:

  * Boundary data (4294)
  * Extreme addresses (0, 4095)

#### ✅ Test 3 (Extended Transaction 2)

* Targets uncovered bins
* Focused randomization

### 🚀 Regression Outcome

* Multiple test executions using `+TEST1`, `+TEST2`, `+TEST3`
* Achieved **complete functional coverage closure**


## 🔄 Environment Flow

1. Reset DUT (memory initialized)
2. Generator produces transactions
3. Drivers apply stimulus
4. Monitors capture DUT activity
5. Reference model predicts expected output
6. Scoreboard compares and validates
7. Coverage sampled and updated
8. Simulation ends on completion event


## 📁 Project Structure

```id="ram_proj01"
dual_port_ram/
│
├── rtl/
│   ├── dual_mem.sv
│   ├── mem_dec.sv
│   └── ram_4096.sv
│
├── tb/
│   ├── ram_if.sv
│   ├── ram_trans.sv
│   ├── ram_gen.sv
│   ├── drivers/
│   ├── monitors/
│   ├── ram_model.sv
│   ├── ram_sb.sv
│   ├── ram_env.sv
│   └── tests/
│
├── top.sv
└── README.md
```


## ⚡ Key Highlights

* ✔️ Complete SV TB (non-UVM)
* ✔️ Mailbox-based communication
* ✔️ Modular and reusable components
* ✔️ Self-checking testbench
* ✔️ Functional coverage driven verification
* ✔️ Regression-based coverage closure


## 🚀 Future Enhancements

* Migration to **UVM**
* Add **functional coverage bins for write operations**
* Assertion-based verification (SVA)
* AXI interface integration
* Performance and latency checks


## 🎯 Applications

* Cache memory systems
* Multi-port memory design
* High-speed processors
* FPGA/ASIC memory verification

