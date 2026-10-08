# Launch Relay KiCad
This project contains the KiCad files for HPRC's Launch Relay board. This PCB was designed for the club's rover payload, which will be flown in the 2027 IREC competition.

## Description
The Launch Relay is designed to help conserve battery life and processing power of the rover payload by acting as a very low-power isolated solid-state relay. The board features an STM32 microcontroller, onboard flash for logging data, and an accelerometer to detect when the rocket launches and lands. It is all powered from a standard coin cell battery.

The firmware for the STM32 can be found [here](https://github.com/NCSU-High-Powered-Rocketry-Club/GildedTrigger).

<img width="690" height="562" alt="image" src="https://github.com/user-attachments/assets/6109a702-3163-4498-bc67-8020089af1c7" />


## Component Overview
Here are the main components that the board uses:

| Component Type | Part Number | Datasheet |
|---|---|---|
| Microcontroller | STM32U083KCU6 | [STMicroelectronics](https://www.st.com/resource/en/datasheet/stm32u083kc.pdf) |
| Accelerometer | BMA580 | [Bosch Sensortec](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bma580-ds000.pdf) |
| SPI NOR Flash (32 Mbit) | MX25R3235FM1IL0 | [Macronix](https://www.macronix.com/Lists/Datasheet/Attachments/8755/MX25R3235F%2C%20Wide%20Range%2C%2032Mb%2C%20v1.8.pdf) |
| D-Type Flip-Flop | SN74LVC1G74DQER | [Texas Instruments](https://www.ti.com/lit/ds/symlink/sn74lvc1g74.pdf) |
| N-Channel Power MOSFET | NVMFS5C460NLAFT1G-YE | [onsemi](https://www.onsemi.com/pdf/datasheet/nvmfs5c460nl-d.pdf) |

The STM32 was chosen for it's lower power consumption and small footprint, while still offering the needed peripherals for the board. The BMA580 accelerometer has excellent programmable interrupt features, allowing for customizable acceleration slopes and durations to be used to detect launch and wake the STM32. After launch, the acceleration data is stored to the MX25R3235F flash, which can be later retrieved for post-processing using the UART and DUMP pin provided on the pin header.

The board has two independent solid-state relays and are controlled using optocouplers. Optocouplers have relatively high power consumption compared to the rest of the board so a flip-flop circuit is used to limit the duration the optocoupler is powered. This powers the gate of the power MOSFET, which is wired as a low-side switch for the external circuit. Both relays on the board are designed for loads up to 10A. External circits must be at least 5.1V.

## Libraries
Some of the KiCad symbols and footprints for this project are not included in the standard KiCad library, and are located in [HPRC's KiCad Library](https://github.com/NCSU-High-Powered-Rocketry-Club/HPRC-KiCad-Library)


## PCBWay
A special thank you to our sponsor, [PCBWay](https://www.pcbway.com/), for supporting the manufacturing of this custom PCB! As a competitive high-powered rocketry team, reliable electronics are essential to the success of our projects. PCBWay's high-quality PCB manufacturing services have helped us turn our designs into functional hardware, allowing us to develop and test custom electronics for our rockets and payloads. Their support, attention to detail, and excellent communication throughout the manufacturing process have been greatly appreciated. We are grateful for their contribution to our team's success and highly recommend checking out their services for your next electronics project!

<img width="600" height="221" alt="image" src="https://github.com/user-attachments/assets/894d4a64-184d-4df3-aff9-4d1df62d253c" />
