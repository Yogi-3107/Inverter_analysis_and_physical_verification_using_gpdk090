# Inverter_analysis_and_physical_verification_using_gpdk090
### Inverter Design, Analysis and Physical Verification using Cadence provided GPDK090 in Cadence Virtuoso
---

In this project, I'm designing a _CMOS Inverter_, which will be analysed using various simulations. Also, a **layout** will be designed for the same followed by _Physical Verification_ steps like _Design-Rule-Check_ (**DRC**), _Layout-Vs-Schematic_ (**LVS**) and _Parasitic/RC Extraction_ (**RCX**). Further,  the results from _Pre-Layout simulation_ will be compared with the _Post-Layout simulation_ and the design will be _streamed-out/tape-out_.

---

## Content
- [1. Tool and PDK used](#1-Tool-and-PDK-used)
  - [1.1 Cadence Virtuoso](#11-Cadence-Virtuoso)
  - [1.2 GPDK090](#12-GPDK090)
- [2. CMOS Inverter](#2-CMOS-Inverter)
  - [2.1 Schematic](#21-Schematic)
  - [2.2 Symbol](#22-Symbol)
- [3. Analysis of CMOS Inverter](#3-Analysis-of-CMOS-Inverter)
  - [3.1 Characteristics of CMOS Inverter](#31-Characteristics-of-CMOS-Inverter)
  - [3.2 Transient and DC Analysis](#32-Transient-and-DC-Analysis)
- [4. Layout and Physical Verification](#4-Layout-and-Physical-Verification)
  - [4.1 Layout](#41-Layout)
  - [4.2 Physical Verification](#42-Physical-Verification)
  - [4.3 Design Rule Checking](#43-Design-Rule-Checking)
  - [4.4 Layout Vs Schematic](#44-Layout-Vs-Schematic)
  - [4.5 RC Extraction](#45-RC-Extraction)
- [5. Post Layout Analysis](#5-Post-Layout-Analysis)
  - [5.1 Post Layout Transient Analysis](#51-Post-Layout-Transient-Analysis)
  - [5.2 Post Layout DC Analysis](#52-Post-Layout-DC-Analysis)
    


## 1. Tool and PDK used

### 1.1 Cadence Virtuoso
![image](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQlqRde5Guj48ZQCn00CIVwFYYiYlWdEDDXFQ&s)

[Cadence Virtuoso](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/virtuoso-studio.html) is a system design platform for analog, mixed-signal, and RF designs. It is a commercially used and critically acclaimed EDA tool and not open-source. The Virtuoso version that I use is provided to me through my institute, and is an integration of multiple [Cadence](https://www.cadence.com/en_US/home.html) products such as [Virtuoso Schematic Editor](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-design/virtuoso-schematic-editor.html), [Virtuoso ADE Suite](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-design/virtuoso-ade-suite.html) and [Virtuoso Layout Suite](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/layout-design/virtuoso-layout-suite.html).

## 1.2 GPDK090
**90nm Generic Process Design Kit** (GPDK090)  is a complete design kit based on a fictitious 90nm BiCMOS process. It is provided by [Cadence](https://www.cadence.com/en_US/home.html) for the purpose of designing, simulating and verifying the ICs for research and educational programs. Manual for the same can be accessed here - [gpdk090-manual](https://www.princeton.edu/~nverma/cadenceSetup_6.1.7/gpdk090_v4.4/docs/gpdk090_spec.pdf).

## 2. CMOS Inverter

### 2.1 Schematic

**Complementary-Metal-Oxide-Semiconductor** (CMOS) Inverter is a fundamental building block in VLSI (**Very Large Scale Integration**) design. Its primary purpose is to _convert input signals into complementary output signals_. This conversion is achieved by leveraging the unique properties of complementary transistors, one **P-channel** and one **N-channel**, to efficiently switch between _logic states (high and low)_. CMOS inverters play a crucial role in _logic gates, amplifiers, and memory circuits_, facilitating signal processing and data manipulation in various electronic devices and systems. Additionally, they offer advantages such as _low power consumption, high noise immunity, and compatibility_ with modern semiconductor manufacturing processes.

![CMOS INV SCHEMATIC](./Schematic%20and%20Symbol/Inverter_Schematic.png)

Image above illustrates the schematic of a typical CMOS Inverter, consisting a **PMOS and NMOS 1V threshold voltage** models from GPDK090 library.
- The schematic shows two transistors tied up in series between the ground (**vss**) and the power(**vdd**) source in it.
- Unlike PMOS transistors where the source is linked to power supply and the drain is tied to the output , an NMOS transistor’s source is directly linked with earth while its drain is linked with output .
- The input to the inverter is actually a mutual connection between the gates of the two transistors.

### 2.2 Symbol

![SYM WITH TT](https://media.geeksforgeeks.org/wp-content/uploads/20240427161407/constructiondrawio.png)

The image above shows the symbol used in the circuits to simply represent a CMOS Inverter. Along with the symbol, the truth table for the CMOS logic is also given to better understand its working.

**Working of CMOS Inverter:**
- **Input High (Logic 1)**: An NMOS transistor is turned on by input of high voltage (logic 1) while a PMOS transistor is turned off there. When these two things happen, the output voltage (logic 0) is lowered through reduced resistance path between an output terminal and ground.
- **Input Low (Logic 0)**: In contrast, when a low voltage (logic 0) is provided to the input terminal, the NMOS transistor switches off and the PMOS transistor conducts. The output voltage (logic 1) rises as a result of the low resistance path that exists between the output terminal and the positive power supply voltage (**vdd**).
- The CMOS inverter operates more easily because of the complimentary characteristics of the NMOS and PMOS transistors. Because one of the transistors conducts while the other is off depending on the input voltage, the output of the transistors is inverted with respect to the input signal.
- CMOS inverters offer very low static power dissipation (no DC current flows between VDD and ground while the input is at a constant logic level) as a result of this complimentary pairing.

Below is the symbol designed in Cadence Virtuoso, that will be utilized in analysing the characteristics of the circuit.
![CMOS SYMBOL](./Schematic%20and%20Symbol/Inverter_Symbol.png)

## 3. Analysis of CMOS Inverter

### 3.1 Characteristics of CMOS Inveter

**Dynamic Characteristics**

![DYNAMIC CHAR](https://www.elprocus.com/wp-content/uploads/Dynamic-Characteristics-of-CMOS-Inverter.jpg)

The characteristics plotted on the graph after _Transient analysis_ is typically called **Dynamic Characteristics** of a CMOS Inverter, as we study the dynamics of the designed circuit.

**Static Characteristics**

![VTC](https://player.slideplayer.com/85/13705706/slides/slide_11.jpg)

Also referred as **Voltage-Transfer-Characteristics** (VTC), is used to measure quality of an inverter by plotting a _voltage transfer curve_ between the input voltage (_in_) and output voltage (_out_).

### 3.2 Transient and DC Analysis

![ANALYSIS SYMBOL](./Transient%20and%20DC%20Analysis/Tran_and_DC_Sim_Schematic.png)

I connected a DC Voltage supply of **1.8 V** across terminal _vdd_ and _vss_ of the inverter and give a pulsating signal as an input (Lower Voltage - **0** and Higher Voltage - **1.8 V**) to test the working of the circuit.

Below is the graphical representation of **Transient** (_left_) and **DC** (_right_) Analysis of a CMOS Inverter. Both are **Pre-Layout** Simulations, i.e., the analysis is done before we extract the **RC parasitics** for the designed circuit. **Green** trace represents the _input_ and **Red** represents the _output_.

![PRE LAYOUT SIM](./Transient%20and%20DC%20Analysis/Tran_and_DC_Sim_Plot.png)

**Transient Analysis**

- Transient behaviour of the Inverter is shown above in the figure (_left_). It shows how the inverter responds to changes in input signal over time, which is crucial for circuit speed and efficiency. It occurs due to effective charging and discharging of the output node of the CMOS inverters due to the quick switching speeds offered by complementary NMOS and PMOS transistors.
- This rapid charging and discharging accounts for the delay in the propagation of the output signal with respect to the recieved input signal, which is called **Propagation Delay**.

Propagation Delay can be calculated using the following formula:

![Formula Prop](https://s0.wp.com/latex.php?latex=t_%7Bp%7D+%3D+%5Cfrac%7Bt_%7Bphl%7D+%2B+t_%7Bplh%7D%7D%7B2%7D&bg=ffffff&fg=000&s=0&c=20201002)

where **tp** is _Propagation Delay_, **tphl** is _delay in the signal when output swtiches from high to low_ and **tplh** is _delay in the signal when output swithces from low to high_.

![TRAN DELAY1](./Transient%20and%20DC%20Analysis/Tran_Delay1.png)
![TRAN DELAY2](./Transient%20and%20DC%20Analysis/Tran_Delay2.png)

For the transient simulation above, the delay came out out to be **20.049 ns**.

**DC Analysis**

- Static Behaviour of the Inverter is shown above in the analysis response (_right_). It shows how the output voltage changes with the input voltage. The threshold voltage is the point at which the output states abruptly change from high to low. The production decreases below this level and stays high above it.
- The VTC is like an upside down step function because of the increased accuracy in turning ON/OFF transitions. Quality in the transition region is suggested by the existence of well-defined slopes that enable precise switching.

To ensure balanced functioning, CMOS inverters should ideally provide a symmetric VTC around the midpoint voltage. For this, we vary the width of the PMOS to find an ideal width at which our CMOS design provides a symmetric VTC. This is called a **Symmetric CMOS**, and its **switching threshold** (_midpoint of VTC_) is **half of the supply voltage** (_vdd_). The plot for the same is shown below:

![DC Sim Symmetric](./Transient%20and%20DC%20Analysis/DC_Analysis_for_Symmetric_Conditions.png)

The width of the PMOS at which the symmetric condition of the CMOS is fulfilled, comes out to be **Wp = 1.15 um**. At this point, the swtiching threshold is nearly equal to half of the supply voltage (**vdd**). 

## 4. Layout and Physical Verification

### 4.1 Layout

**Layout** in VLSI refers to the process of creating the __physical representation of an integrated circuit__ (IC) design. It involves **translating the logical circuit description (schematic) into geometric representations of the various layers** used in semiconductor manufacturing.

Purpose:
 - Translate logical design into a physical representation suitable for manufacturing.
 - Optimize chip area, performance, and power consumption.
 - Ensure manufacturability and reliability of the IC.

Process Flow: (_Also termed as_ **Physical Design Flow**)
 - **Floorplanning:** Arranging major functional blocks
 - **Placement:** Positioning individual cells or components
 - **Routing:** Connecting components with metal layers
 - **Compaction:** Optimizing layout for area efficiency
 - **Verification:** DRC, LVS, RCX/XRC

Below is the layout design of CMOS Inverter in Cadence Virtuoso:

![Layout](./Layout%20and%20Physical%20Verification/Inverter_Layout.png)

Layout is a critical phase in VLSI design, directly impacting the final chip’s performance, power efficiency, and manufacturability. Mastery of layout techniques is essential for creating high-quality integrated circuits.

### 4.2 Physical Verification

Commercially, there are various tools available for the Physical Verification of the MOS Circuits like _Cadence PVS, Mentor Graphics Calibre, Synopsys IC Validator, etc._ but the tool I utilized to do so is [Cadence Assura](https://www.cadence.com/en_US/home/tools/digital-design-and-signoff/silicon-signoff/assura-physical-verification.html). All the physical verification steps - _DRC, LVS and RCX_ for the project is done via this tool.

### 4.3 Design Rule Checking

Design Rule Checks are nothing but **physical checks of metal width, pitch and spacing requirement** for the different layers which _depend on different technology nodes_. We need to **clean up** the DRC of the design because there is a logical connection of various components, and if they are physically connected, then it will fail the functionality of the chips, and chips won’t be able to perform a specific task.

The layout of a design must be in accordance with a set of **predefined technology rules given by the foundry for manufacturability**. After completion of the layout and its physical connection, an automatic program will check each and every polygon in the design against these design rules and report any violations. This whole process is called **Design Rule Checking (DRC)**. 

There are many design rules at different technology nodes, a few of which are mentioned below:
- Minimum width and spacing for metal
- Minimum width and spacing for via
- Fat wire Via keep out Enclosure
- End of Line spacing
- Minimum area
- Over Max stack level
- Wide metal jog
- Misaligned Via wire
- Different net spacing
- Special notch spacing
- Shorts violation
- Different net Via cut spacing
- Less than min edge length

The layout I designed, pass the DRC and is DRC clean as illustrated  below
![DRC](./Layout%20and%20Physical%20Verification/Inverter_Layout_DRC.png)

### 4.4 Layout Vs Schematic

Layout Versus Schematic (LVS) checking **compares the extracted netlist from the layout to the original schematic netlist to determine if they match**. The comparison check is considered **clean** if all the devices and nets of the schematic match the devices and the nets of the layout. Optionally, the device properties can also be compared to determine if they match within a certain tolerance. When properties are compared, all the properties must match as well to achieve a clean comparison.

Two main processes make up the LVS flow. The first process in the flow is **extraction**, in which _the layers within the layout database are analyzed and all the devices and nets are extracted_. The second process in the flow is **compare**, in which the _actual comparison of devices and nets occurs_.

The LVS runset contains a series of function calls that control both extraction and netlist comparison.

LVS errors can be classified into two main categories:

1. Extraction Errors
   - Text short and open
   - Device extraction error
   - Missing device terminal
   - Extra device terminal
   - Unused text
   - Duplicate structure placement

2. Compare Errors
   - Unmatched nets in the layout/schematic
   - Unmatched devices in the layout/schematic
   - Property errors
   - Port swap errors

The LVS of the CMOS Layout design is a match after the debugging as shown below:
![LVS](./Layout%20and%20Physical%20Verification/Inverter_Layout_LVS.png)

### 4.5 RC Extraction

**Parasitic Extraction** provide the information about the _parasitic devices which are not included as a part of original circuit design_. But these parasitic devices **affect the circuit performance** in several ways. There are chances that because of these devices, the circuit stops working or does not meet design specifications.

Effect of Parasitic Devices on Circuit Design:

1. Extra Power Consumption
   - violate the Power specification extra power dissipation can increase local temperature which can effect other parameters

2. Effect the Delay of circuit
   - which can cause of timing violation can impact IR drop

3. Reduce the Noise Margin
   - which can cause logic failure

4. Increase Signal Noise which can
   - change the Logic of the signal (0 to 1) or (1 to 0)
   - logic failure introduce extra/unwanted delay which can impact the timing
   - speed up the signal which again impact the timing

5. Increase IR drop on power supply lines
   - which in turn affects delay

In order to get a good idea of realistic parameters in our design, we run RCX which can **estimate and add** to your design the _parasitic resistances (R), capacitances (C), self inductances (L), and mutual inductances (K)_. We are only interested in RC parasitics, hence, **RC Extraction**.

For the final step of physical verification of CMOS Inverter, I ran Assura RCX as shown below:
![RCX](./Layout%20and%20Physical%20Verification/Inverter_Layout_RCX.png)

The extracted view or  _Post-Layout View_ is saved with the name **av_extracted** and the Physical Verification step is concluded.

## 5. Post Layout Analysis

The procedure of running post-layout simulations is very similar to simulating a Schematic. The steps to prepare a design for post-layout simulations are listed below:
- Extracting the parasitics
  - which is already done in RCX.
- Creating Analog Extracted View
  - created after the completion of RCX (**av_extracted**).
- Simulating the Analog Extracted View
  - can be done after creating a config file for the Inverter to access the Analog Extracted View and simulating it similarly as done earlier in Pre-Layout Analysis.

In the Post-Layout Transient and DC Analysis, that is discussed below, the **Green** trace denotes _input_, **Dotted Yellow** trace denotes _Pre-Layout output_ results and **Red** trace denotes _Post-Layout output_ results.

### 5.1 Post Layout Transient Analysis

Below are the results from Post-Layout transient analysis of CMOS Inverter:
![Tran SIM1](./Post-Layout%20Simulations/Post-Layout_Trans_Sim1.png)
![Tran SIM2](./Post-Layout%20Simulations/Post-Layout_Trans_Sim2.png)
![Tran SIM3](./Post-Layout%20Simulations/Post-Layout_Trans_Sim3.png)

After taking a closer look at the results, it is clear that Pre-Layout and Post-Layout results **vary slightly**, therefore the delay in the output signal is also **affected by the RC parasitics** extracted after the physical verification. The delay is calculated is shown below:
![Tran Delay](./Post-Layout%20Simulations/Post-Layout_Trans_Delay.png)

The delay comes out to be, **20.0362 ns**. Difference in Pre-Layout and Post-Layout Delay is **0.0128 ns** or **12.8 ps**.

### 5.2 Post Layout DC Analysis

Similarly, results will also vary for DC simulation of the extracted view of the Inverter as illustrated below:
![DC SIM1](./Post-Layout%20Simulations/Post-Layout_DC_Sim1.png)
![DC SIM2](./Post-Layout%20Simulations/Post-Layout_DC_Sim2.png)

As we can see from the results illustrated above, the switching threshold for the _Pre-Layout DC Analysis_ came out to be **904.9415 mV** whereas for the _Post-Layout DC Analysis_, it came out to be **906.1876 mV**.
