# Immortals Main Electronics
The main electronics of Immortals SSL robots, used to receive commands from the main computer through wireless link, drive the robots’ motors, apply a control loop on the motors, do some local sensing and send some feedback data to the main computer.

![PCB](/Images/main_3d.png)

The main features are:
* A **Xilinx Spartan 3** FPGA containing **400K** logic gates as the main processor.
* **2.4 GHz full duplex** wireless communication, with a total bandwidth of **2Mbps**. It uses our own software layer, which allows 12-bit addressing (much more than the requirements for our purpose), delivery acknowledgment and auto re-transmitting when required, auto detection of the working channel, signal strength detection and much more.
* An alternative **915 MHz** RF communication, with much lower bandwidth (38 Kbps), to use when the ISM band traffic is too high, or a higher range is needed.
* **TSK3000A**, a **32-bit RISC** soft-processor, implemented inside the FPGA. It has 5 pipelines, and a theoretical value of **1.2 MIPS per MHz**. We use this processor at the frequency of **40 MHz**. It’s the main processing unit of the board.
* **9-Axis IMU**, used to determine a local transformation of the robot. This local data are used when:
  * There are lost packets
  * The vision could not determine the global state
  * Removing the global vision latency by predicting the vision data (for about 150 mS)
* BLDC motor drivers, capable of driving 5 BLDC motors at a very high frequency, using hall-sensor commutation. The commutation logic is implemented inside the FPGA.
* A flash memory, to save the firmware, its parameters’ values and debugging data. The firmware allows the downloading of a newer version, changing the parameters, and error reading via the wireless link.

From an electrical point of view, the PCB is designed in a **multi-layer** fashion (**4-layer**). This is because of the FPGA requirements, and the very high current drawn by the BLDC motors (230 amperes!).
![PCB](/Images/main_pcb.jpg)
