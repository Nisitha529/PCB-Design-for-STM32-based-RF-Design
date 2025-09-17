# PCB-Design-for-STM32-based-RF-Design
This PCB board design is a USB-powered platform combining an STM32L432 Cortex-M4 microcontroller and an nRF24L01+ 2.4GHz transceiver. The board is designed with a focus on power delivery and signal integrity. Power is supplied via a USB Micro-B connector and regulated down to 3.3V by an XC6206 LDO, with attention paid to in-rush current limits for USB compliance. The USB data lines are protected against electrostatic discharge (ESD) by a dedicated USBLC6-2SC6 chip. The nRF24 module features a full impedance-matching network and a passive antenna circuit, ensuring optimal RF performance. The board includes a 10-pin ARM Serial Wire Debug (SWD) header for programming and debugging, status LEDs, and a crystal oscillator for the radio module.

## Power Regulation and USB Interface
The 5V supply from the USB port is first passed through a 100mA fuse for overcurrent protection, safeguarding the host port. A ferrite bead filters high-frequency noise from the power line. The core of the power circuit is an XC6206 low-dropout (LDO) regulator, which efficiently converts the 5V input to a stable 3.3V output, capable of supplying up to 200mA. Input and output capacitors ensure voltage stability and are carefully sized to limit in-rush current upon connection, ensuring compliance with the USB specification.

For the data interface, the USB D+ and D- lines are routed directly from the connector through a USBLC6-2SC6 ESD protection chip. This component is critical for shielding the sensitive microcontroller pins from electrostatic discharge, a common cause of failure in USB-connected devices. The design foregoes reverse polarity protection as the physical keying of the standardized USB connector makes incorrect insertion impossible.

<img width="915" height="625" alt="Power Regulation and USB Interface Circuit Diagram" src="https://github.com/user-attachments/assets/1e5e2c34-9708-4ef1-b685-4188a5c8adc9" />

## Power Decoupling and Debug Interface
The board features a robust power delivery network for the microcontroller, utilizing multiple decoupling capacitors (a 1µF and three 100nF) on the +3.3V rail to ensure stable operation by filtering high and low-frequency noise. For programming and debugging, a standard 10-pin ARM Serial Wire Debug (SWD) connector is implemented. This interface provides access to the essential SWDIO and SWCLK signals, a connection to the NRST (Reset) line, and is powered by the board's +3.3V supply. An optional capacitor on the NRST line is noted to safeguard against potential parasitic resets, enhancing the board's stability.

<img width="596" height="554" alt="Power Decoupling and Debug Interface Circuit Diagram" src="https://github.com/user-attachments/assets/36e7d7f9-cee7-4c96-914e-1144f517e1b4" />


## nRF24L01+ Transceiver and RF Circuitry
The wireless core of the board is built around the nRF24L01+ transceiver module. It is connected to the microcontroller via a dedicated SPI bus (MOSI, MISO, SCK) and controlled using chip select (CS), chip enable (CE), and interrupt (IRQ) lines. Local power decoupling is ensured by a bank of 10nF capacitors. For RF performance, an impedance matching network is implemented between the module's antenna outputs (ANT1/ANT2) and the SMA connector. This network, consisting of inductors (L1-L3) and capacitors (C15-C18), transforms the output impedance for efficient power transfer to the passive antenna. A 16MHz crystal oscillator with its associated load capacitors (C13, C14) and a 1MΩ bias resistor (R5) provides the critical reference clock for the operation.
<img width="856" height="513" alt="nRF24L01+ Transceiver and RF Circuitry Diagram" src="https://github.com/user-attachments/assets/5b5263e0-8ca0-48cd-8bcf-023672666220" />



<img width="1084" height="425" alt="PCB Routing Diagram" src="https://github.com/user-attachments/assets/80a8eb84-6fd0-4981-aa21-1fc5d382dd3e" />

## 3D View of the Final PCB Design
### Front View

<img width="586" height="229" alt="3D Preview Front View" src="https://github.com/user-attachments/assets/7189bd72-baae-43fc-ae7e-a49bbb380f4b" />

### Backward View

<img width="586" height="229" alt="3D Preview Backward View" src="https://github.com/user-attachments/assets/bbda2bd3-a91f-46db-8f4f-4d8740ba5b27" />



<img width="615" height="411" alt="3D Preview 3" src="https://github.com/user-attachments/assets/e47e48f9-2ff3-45cd-b483-318d845a1464" />
