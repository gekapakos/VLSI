

# 1st Assignment: CMOS Inverter Design and Simulation

## Exercise 1: CMOS Inverter Design
- **Objective**: Design a minimum-area CMOS inverter in MAGIC.  
- **Specifications**:  
  - NMOS/PMOS size: `W = 3µm`, `L = 2µm`.  
  - Vertical polysilicon common gate.  
  - Power lines (4µm): `vdd`, `gnd`.  
  - Wells: `p-well` (NMOS), `n-well` (PMOS).  
  - Substrate contacts: `psubstratepcontact`, `nsubstratencontact`.  
  - Labels: `in` (input), `out` (output).  
- **Output**: Extract to SPICE netlist.  
- **Verification**: Check MOSFET terminals (`d g s b`) in `Mxxx d g s b MNAME w=val l=val` for correct connections (`in`, `gnd`, `out`, `vdd`).

## Exercise 2: Functional Verification and Timing Analysis
- **Objective**: Simulate inverter in SPICE and measure timing.  
- **Measurements**:  
  - (a) Propagation delays (0→1, 1→0) at 50% transitions.  
  - (b) Output rise/fall times for input `trise,fall = 200ps` (10% to 90%).  
- **Simulation Setup**:  
  - Include `0.25-models` (`.include`).  
  - Use MAGIC netlist, rename models to `CMOSN`, `CMOSP`.  
  - Define DC voltages (`Vxxxx n+ n- DC`).  
  - Input: Linear waveform (`PWL time voltage ...`).  
  - Transient analysis: `.tran 10ps tstop`.  
- **Timing Measurement**:  
  - Use `.meas tran trig v(node1) val=xx at=1 targ v(node2) val=xx at=1`.  
  - Set `node1`, `node2` (e.g., `in`, `out`) and `xx` (voltage).
 
 # 2nd Assignment: CMOS Transistor and Inverter Analysis

## Exercise 1: NMOS and PMOS Characterization
- **Setup**: NMOS and PMOS transistors with `W = 3µm`, `L = 2µm`, 2.5V, MOSIS-TSMC 0.25µm process, SPICE Level 3 models.  
- **(a) Ids Characteristics**:  
  - Perform DC analysis to plot `Ids` vs. `Vgs` and `Vds` (0.25V steps).  
  - Identify `Vds = Vgs - Vt` points and vertical `Vgs` distances.  
  - Calculate:  
    - (i) Instantaneous resistance `Reqabs = V/I`.  
    - (ii) Average resistance `Reqav = ∆V/∆I` in saturation for `Vgs = {0.8, 1.2, 2, 2.5}`.  
  - Comment on differences between `Reqabs` and `Reqav` across `Vgs`.  
- **(b) RC Equivalent Resistance**:  
  - Simulate NMOS (discharge) and PMOS (charge) with a capacitor (e.g., `C = 0.1pF`).  
  - Calculate average equivalent resistance for both transistors.  
  - Compare results with (a) and discuss transistor type differences.

## Exercise 2: Threshold Voltage in Series
- **Setup**: Same transistors as Exercise 1.  
- **Objective**: Use NGSPICE transient analysis to calculate threshold voltage `VT` for transistors in series.  
- **Simulation**:  
  - Measure voltage drop for two identical transistors in series.  
  - Determine total voltage drop and explain the cause.

## Exercise 3: CMOS Inverter Analysis
- **Setup**: Inverter with NMOS/PMOS, `W = 3µm`, `L = 2µm`, 2.5V, MOSIS-TSMC 0.25µm.  
- **(a) Transfer Curve (Vout/Vin)**:  
  - Perform DC analysis to plot the transfer curve.  
  - Calculate `VM`, `VOH`, `VOL`, `VIH`, `VIL`, and noise margins for logic 0 and 1.  
  - Adjust transistor sizes minimally for symmetric noise margins.  
  - Comment on changes and related physical phenomena.  
- **(b) Voltage Scaling Impact**:  
  - Analyze noise margins and power consumption for `Vdd = {0.7, 1.2, 1.8}`.  
  - Generate transfer curves and evaluate improvement or degradation.
 
# 3rd Assignment: CMOS Logic Gate Design and Analysis

## Exercise 1: CMOS Gate Implementation
- **Functions**:  
  - `faoi21 = (a + bc)'`  
  - `foai31 = (ab + b(c + d))'`  
  - `fmaj = (ab + bc + ac)'`  
  - `faoi22 = (ac + bd)'`  

### (a) Schematic Design and Transistor Sizing  
- Design static CMOS gates with minimal transistor count.  
- Size transistors so pull-up and pull-down networks each have `6.5kΩ` resistance.  
- Given: NMOS `13kΩ`, PMOS `31kΩ` at 2.5V, `W = L = 2λ` (`λ = 0.125μm`), 0.25μm process.  

### (b) Stick Diagram Design  
- Draw dimensionless stick diagrams for each gate from (a), showing transistor layout and interconnections.  

### (c) Layout Design  
- Implement stick diagrams in Magic (SCMOS technology) as EDA standard cells.  
- Verify functionality in NGSPICE and display waveforms.  

### (d) Capacitance Analysis (AOI21 Gate)  
- For the AOI21 gate from (c):  
  - Calculate diffusion area and perimeter per transistor.  
  - Compute diffusion capacitances for 1→0 output transition.  
- Given:  
  - `Cj = 2 fF/μm²`  
  - `Cjsw = 0.28 fF/μm`  
  - `Knj = 0.57`, `Knjsw = 0.61`, `Kpj = 0.79`, `Kpjsw = 0.86`  

### (e) Delay Analysis (AOI21 Gate)  
- Use the Elmore delay model to calculate worst-case pull-down network delay.  
- Base calculations on capacitances from (d), assuming the gate drives four identical AOI21 gates.

# 4th Assignment: CMOS Latch and Flip-Flop Design

## Exercise 1: State-Enforcing Latch
- **Objective**: Design and simulate a state-enforcing latch with weak inverter feedback in SPICE (see Figure 1).  
- **Setup**: Minimum transistor sizes: `Wn = 3µm`, `Wp = 9µm`.  
- **Task**:  
  - Select appropriate sizes for correct operation.  
  - Describe the schematic in SPICE.  
  - Simulate the full truth table to verify functionality.  
- **Output**: Present waveforms and analysis for verification.

## Exercise 2: Edge-Triggered Flip-Flop
- **Objective**: Design and simulate an edge-triggered flip-flop in SPICE (see Figure 2).  

### (a) Schematic and Verification  
- **Setup**:  
  - Transistors: `Wn = 3µm`, `Wp = 9µm`.  
  - Clock input (`CLK`) buffered with two unit-sized inverters (`g1`, `W = 3µm`), followed by x2 gates (2x size).  
- **Task**:  
  - Describe the master-slave flip-flop schematic in SPICE.  
  - Simulate the full truth table to verify functionality.  
- **Output**: Present waveforms and analysis for verification.

### (b) Timing Parameter Measurement  
- **Conditions**:  
  - Fixed `CLK` rise/fall time: 200ps.  
  - Input `D` rise/fall times: `trf(D) = {200ps, 400ps}`.  
  - Load on `Q`: `CQ = {Cg1, 2Cg1}`.  
- **Measurements**:  
  - `CLK→Q` delay.  
  - Rise/fall times of `QM` (master) and `Q` (output).  
  - `SETUP` time/constraint.  
  - `HOLD` time/constraint.  
- **Analysis**:  
  - Identify `SETUP` and `HOLD` constraints by simulating CLK-D timing deviations causing metastability (affecting `CLK→Q` delay).  
  - Provide detailed waveforms, measurements, and comments on the impact of input rise/fall times.
