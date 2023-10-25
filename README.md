#pes_aclock
 Implementation of an Alarm Clock in Verilog
This project carries out the design and development of a fully implementable Verilog code of a working digital
# Contents
[alarm_clock](#alram_clock_introduction)
[Iverilog and yosys installation](#iverilog-and-yosys-installation)
 [GLS Process to verify alarm_clock][[#GLS-Process-to-verify-alarm-clock]

 
 ##aclock
 his design aims to apply the Verilog language into the
development of a simple mechanism of a digital alarm clock. The block diagram for the proposed design is shown below:

## Iverilog and yosys Installation
- To install iverilog and gtkwave we type the following
```
- sudo apt-get update
- sudo apt-get install iverilog gtkwave
```

- To install yosys we type the following
```
- git clone https://github.com/YosysHQ/yosys.git
- sudo apt install make
- sudo apt-get install build-essential clang bison flex \
   libreadline-dev gawk tcl-dev libffi-dev git \
   graphviz xdot pkg-config python3 libboost-system-dev \
   libboost-python-dev libboost-filesystem-dev zlib1g-dev
```

- Now we type ```cd yosys``` and go into the yosys folder.
- Now we type
```
sudo make install
```
## GLS Process to Verify T flip flop


First we will look at the waveform simulation of the program 

![Screenshot from 2023-10-25 17-25-14](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/9c1feff8-f0c3-41bb-8635-6c4654aff1d6)
- We first read the design and testbench file using the command
```iverilog pes_aclock.v pes_aclock_tb.v
- Then we type ```./a.out``` to generate the .test=file
- Now we type







