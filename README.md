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
  -[2.1 Schematic](#21-Schematic)
  -[2.2 Symbol](#22-Symbol)
    


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
