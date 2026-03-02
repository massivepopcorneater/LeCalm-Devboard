# LeCalm-Devboard
LeCalm Devboard is an open source RP2040 based development board designed as a compact and capable platform for embedded projects. Built around the Raspberry Pi RP2040 microcontroller, it features a USB-C connector for programming and power, an onboard 3.3V regulator, a 16MB flash chip, and a 12MHz crystal oscillator for precise timing. The board includes a BOOTSEL button for easy drag and drop firmware flashing with no external programmer required.
This project was designed from scratch in KiCad as a personal learning project, exploring PCB layout, component selection, and design for manufacture with JLCPCB.

## Schematic
<img width="1225" height="866" alt="Schematic" src="https://github.com/user-attachments/assets/14d62234-4e0e-4939-8a38-b095d01779a9" />
The schematic of the LeCalm Devboard centers around the RP2040 microcontroller. The power section takes 5V from the USB-C connector and passes it through the MCP1700 LDO regulator to produce a clean 3.3V rail, with 1uF and 10uF bulk capacitors smoothing out any voltage fluctuations. Each power pin on the RP2040 is decoupled with a dedicated 0.1uF capacitor placed as close to the pin as possible to suppress high frequency noise. The 12MHz crystal oscillator is connected to the XIN and XOUT pins of the RP2040 with two 33pF load capacitors to ground, providing the precise clock reference needed for full speed operation and stable USB communication. The USB-C connector is wired with 5.1K resistors on the CC1 and CC2 configuration pins for proper power negotiation, and 27Ω series resistors on the D+ and D- differential pair to reduce signal reflections. The W25Q128JVS flash chip is connected to the RP2040 via SPI with all power pins properly decoupled, and the BOOTSEL button is wired to the flash chip select line through a current limiting resistor to ground, allowing the RP2040 to enter USB Mass Storage mode on boot when pressed.

## PCB Design
<img width="364" height="649" alt="PCB Design" src="https://github.com/user-attachments/assets/4df4ef63-a6a6-49a0-bd78-d35c4ae1027b" />
The PCB layout of the LeCalm Devboard was designed in KiCad with a focus on signal integrity and clean power distribution.  Decoupling capacitors are placed as close as physically possible to the power pins of the RP2040 and the W25Q128JVS flash chip to minimize trace inductance and ensure effective high frequency filtering. The 12MHz crystal oscillator is positioned close to the XIN and XOUT pins of the RP2040 to keep the clock traces short and reduce the risk of noise pickup. The USB-C connector is placed at the edge of the board for easy access, with the 27Ω series resistors on the D+ and D- differential pair routed as a matched length pair to maintain signal integrity across the USB data lines. A ground copper pour covers both the front and back copper layers, providing a low impedance return path for all signals and helping to dissipate heat across the board. Thermal relief spokes are used where pads connect to the ground pour to ensure reliable soldering during assembly. The BOOTSEL button is positioned on the top of the board for easy access during firmware flashing. All SMD components use 0402 and 0603 imperial footprints, keeping the overall board size compact while remaining manufacturable through JLCPCBs standard PCB assembly service.

## Bill of Materials
| Designation | Designation | JLCPCB Part # | Value | Footprint |
| ------------|-------------|---------------|-------|-----------|
| Capacitor | C1, C10 | C52923 | 1uF | C_0402_1005Metric |
| Capacitor | C2, C3, C4, C5, C6, C7, C8, C9, C11, C12, C17 | C1525 | 0.1uF | C_0402_1005Metric |
| Capacitor | C13, C14 | C19702 | 10uF | C_0603_1608Metric |
| Capacitor | C15, C16 | C1562 | 33pF | C_0402_1005Metric |
| USB_C Power | J1 | C165948 | USB_C_Receptacle_USB2.0_14P | USB_C_Receptacle_HRO_TYPE-C-31-M-12 |
| Resistor | R1, R2 | C25905 | 5.1K | R_0402_1005Metric |
| Resistor | R3, R4 | C25100 | 27Ω | R_0402_1005Metric |
| Resistor | R5, R6 | C11702 | 1K | R_0402_1005Metric |
| Resistor | R7 | C25744 | 10K | R_0402_1005Metric |
| Bootsel Button | SW1 | C720477 | SW_Push | SW_Push_SPST_NO_Alps_SKRK |
| Microcontroller | U1 | C2040| RP2040 | QFN-56-1EP_7x7mm_P0.4mm_EP3.2x3.2mm |
| LDO | U2 | C39051 | MCP1700x-120xxTT | SOT-23 |
| Flash Memory | U3 | C2843335 | W25Q128JVS | Winbond_USON-8-1EP_3x2mm_P0.5mm_EP0.2x1.6mm |
| Crystal Oscillator | Y1 | C9002 | 12MHz | Crystal_SMD_Abracon_ABM8-2Pin_3.2x1.5mm |
