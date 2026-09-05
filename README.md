
# AMC-Mark-1
KiCad-based 2-layer STM32F401RE evaluation board with USB, UART, SPI, I²C, SWD, GPIO expansion, power regulation and user interfaces.

**STM32F401RE DEVELOPMENT BOARD**

**1. Selected MCU & Design Concept**

**Selected MCU**

**STM32F401RE / STM32F401RET6**

The **STM32F401RE** is selected as the core microcontroller for the evaluation board. It is based on an **Arm Cortex-M4 processor with Floating Point Unit (FPU)** and provides a broad set of peripherals, including GPIO, timers, ADC, UART/USART, SPI, I²C, USB 2.0 Full-Speed and SWD/JTAG debugging capabilities.
The MCU was selected because its peripheral set allows the major requirements of the evaluation board to be implemented around a **single central processing device**, while providing sufficient GPIO for external expansion.

**Why STM32F401RE?**

The core objective is to develop a **compact evaluation platform around the STM32F401RE** that allows users to:

- Program and debug the MCU through SWD.
- Communicate with a PC or USB host through USB.
- Experiment with UART, SPI and I²C peripherals.
- Access additional GPIOs for external circuits and modules.
- Interact with the board through user buttons and LEDs.
- Evaluate the MCU in a practical embedded-system development environment.

Thus, the STM32F401RE acts as the **central hub connecting the processing, communication, debugging and expansion interfaces**.

**Design Concept**

We propose a **compact, custom 2-layer STM32F401RE evaluation board** designed to provide convenient access to the MCU's processing, communication, debugging and GPIO capabilities.
The design is **functionally inspired by the STM32 NUCLEO-F401RE**, which provides STM32 development, Arduino compatibility, ST Morpho expansion and integrated ST-LINK debugging.
However, instead of reproducing the Nucleo architecture, our design independently implements the required functionality with a simpler and more focused architecture.

**Key design approach**

- **STM32F401RE** as the central MCU.
- **External ST-Link through SWD**, avoiding duplication of the on-board ST-LINK circuitry.
- **USB Type-C** providing direct USB 2.0 connectivity to the STM32.
- Dedicated and clearly labelled **UART, SPI and I²C interfaces**.
- **GPIO expansion headers** for external experimentation.
- Dedicated **reset button, user button, user LED and power indication**.
- Custom **power distribution, decoupling and grounding strategy**.
- Independently designed **2-layer PCB layout and routing** within the competition's 100 mm × 100 mm limit.

**Core Design Idea**

> To create a compact and accessible STM32F401RE evaluation platform that brings the MCU's major communication, debugging and GPIO capabilities onto a single independently designed 2-layer PCB, allowing users to program, debug and experiment with the MCU and external peripherals without reproducing the complete Nucleo architecture.

---

**Design Objectives**

1. Develop a functional **STM32F401RE evaluation platform**.
2. Provide **USB Type-C USB 2.0 connectivity** to the MCU.
3. Provide accessible **UART, SPI and I²C interfaces**.
4. Provide **SWD programming and debugging** using an external programmer/debugger.
5. Provide **user reset, user button, user LED and power indication**.
6. Provide **GPIO expansion headers** with power and ground.
7. Implement appropriate **power regulation and local decoupling**.
8. Develop a compact and electrically complete **2-layer PCB within 100 mm × 100 mm**.
9. Independently design the **schematic, component selection, placement, routing and silkscreen** rather than reproducing the reference board.





**2. BLOCK DIAGRAM**

<img width="1536" height="1024" alt="ChatGPT Image Sep 5, 2026, 11_15_35 PM" src="https://github.com/user-attachments/assets/f2417879-76ab-417a-bf01-fd271e539921" />




**3. Schematic progress**

**4. Components Used**

| **Sl. No.** | **Component Type**     | **Value / Part Number**         | **Quantity** | **Section / Function**          |
| ----------- | ---------------------- | ------------------------------- | ------------ | ------------------------------- |
| 1           | Microcontroller        | STM32F401RET6                   | 1            | Main MCU                        |
| 2           | Voltage Regulator      | AMS1117-3.3                     | 1            | 5 V to 3.3 V regulation         |
| 3           | USB Type-C Connector   | USB\_C\_Receptacle\_USB2.0\_16P | 1            | USB communication and 5 V input |
| 4           | Pin Header / Connector | Conn\_01x02\_Pin                | 1            | External 5 V / GND connection   |
| 5           | Pin Header             | Conn\_01x05\_Pin                | 1            | SWD programming/debugging       |
| 6           | Pin Header             | Conn\_01x04\_Pin                | 1            | UART interface                  |
| 7           | Pin Header             | Conn\_01x06\_Pin                | 1            | SPI interface                   |
| 8           | Pin Header             | Conn\_01x04\_Pin                | 1            | I²C interface                   |
| 9           | Pin Header             | Conn\_01x10\_Pin                | 1            | GPIO expansion                  |
| 10          | Push Button            | SW\_Push                        | 1            | User button                     |
| 11          | Push Button            | SW\_Push                        | 1            | Reset button                    |
| 12          | LED                    | LED                             | 1            | Power ON indicator              |
| 13          | LED                    | LED                             | 1            | User-programmable LED           |
| 14          | Resistor               | 4.7 kΩ                          | 1            | I²C SCL pull-up                 |
| 15          | Resistor               | 4.7 kΩ                          | 1            | I²C SDA pull-up                 |
| 16          | Resistor               | 1 kΩ                            | 1            | Power LED current limiting      |
| 17          | Resistor               | 330 Ω                           | 1            | User LED current limiting       |
| 18          | Resistor               | 10 kΩ                           | 1            | BOOT0 pull-down                 |
| 19          | Resistor               | 10 kΩ                           | 1            | User button pull-up             |
| 20          | Resistor               | 10 kΩ                           | 1            | NRST pull-up                    |
| 21          | Resistor               | 5.1 kΩ                          | 1            | USB-C CC1 pull-down             |
| 22          | Resistor               | 5.1 kΩ                          | 1            | USB-C CC2 pull-down             |
| 23          | Capacitor              | 10 µF                           | 1            | AMS1117 input capacitor         |
| 24          | Capacitor              | 10 µF                           | 1            | AMS1117 output capacitor        |




**5. Major design decisions**

- Selected USB Type-C as the USB connector for communication and power input.
- Designed the board to accept 5 V power from either USB-C or an external 5 V connector.
- Selected the AMS1117-3.3 voltage regulator to generate the required 3.3 V supply.
- Used an external ST-Link through the SWD header instead of including an onboard ST-Link debugger.
- Selected PA11 and PA12 for USB D− and D+ communication.
- Selected PA9 and PA10 for UART TX and RX.
- Selected PA4, PA5, PA6 and PA7 for SPI communication.
- Selected PB6 and PB7 for I²C communication.
- Used 4.7 kΩ pull-up resistors for the I²C SCL and SDA lines.
- Used 5.1 kΩ pull-down resistors on CC1 and CC2 to configure the USB-C connector for device operation.
- Pulled BOOT0 to GND using a 10 kΩ resistor to ensure normal boot from internal Flash memory.
- Used separate headers for UART, SPI, I²C, SWD and GPIO expansion for easier testing and external interfacing.
- Selected additional unused MCU pins and brought them out through a dedicated GPIO expansion header.
- Used separate Power ON LED and User LED to distinguish power status from software-controlled indication.
- Chose a simple push-button reset circuit with a pull-up resistor for reliable manual reset.

