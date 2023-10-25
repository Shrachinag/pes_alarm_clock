
# pes_aclock
  - [Implementation of an Alarm Clock in Verilog This project carries out the design and development of a fully implementable Verilog code of a working digital]
# Contents
- [alarm_clock](#alram_clock_introduction)
 - [Iverilog and yosys installation](#iverilog-and-yosys-installation)
  - [GLS Process to verify alarm_clock][[#GLS-Process-to-verify-alarm-clock]

 
 ## a_clock
-  this design aims to apply the Verilog language into the
   development of a simple mechanism of a digital alarm clock. The block diagram for     the proposed design is shown below:
![image](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/d0b1b999-e0fd-41db-a91b-dc57ccb1f58d)

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
'''
![image](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/9da88444-9ae0-41ce-b134-b446e46da5cd)
iverilog pes_aclock.v pes_aclock_tb.v
'''

- Then we type ```./a.out```
 to generate the .vcd file
- Now we type
'''gtkwave test.vcd'''


[Screenshot from 2023-10-25 17-26-03](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/90cdaa7d-fa19-417b-a3f8-fa0cb366e30e)

the waveform is obtained is 


Now we will synthesize the design and generate the netlist file.

![Screenshot from 2023-10-25 19-12-36](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/02fa9693-09e8-4b6e-8393-9c2b5f5bdff3)

'''
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog pes_aclock.v
synth -top pes_aclock
'''
![Screenshot from 2023-10-25 19-31-19](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/acc13294-3573-448f-bd28-e34e75deb53f)

![Screenshot from 2023-10-25 20-27-54](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/2b6cdac8-1580-40b0-b3c2-86e0bde7181b)

![Screenshot from 2023-10-25 20-27-54](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/8df5b320-eb67-4808-a0f0-0069eadcb9eb)

'''
abc -liberty sky130_fd_sc_hd__tt_025C_1v80.lib
'''
![Screenshot from 2023-10-25 20-28-35](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/e1aba18a-9a6f-481c-b395-db6ce4518f70)


we type show to display our design
![Screenshot from 2023-10-25 20-29-34](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/2d79e2bf-8179-4162-a6ab-5f5cdb1e693d)



To generate the netlist file we must type the command
'''
write_verilog -noattr pes_tff_netlist.v
'''
![Screenshot from 2023-10-25 20-31-16](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/571bdbe8-9c31-4cf9-8343-2a41c04a33ca)

    Now using the netlist file, we verify the waveform once more

![Screenshot from 2023-10-25 21-16-10](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/85bb7fce-3dba-4bfe-8a8a-00e31c855082)

To read the design and test bench file we must use the command
'''
iverilog primitives.v sky130_fd_sc_hd.v pes_aclock _netlist.v pes_aclock_tb.v
'''
To see the waveform we type the command
'''
gtkwave test.vcd
'''
![image](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/83412427-69b3-404f-a661-cb15d1af2b0d)


the sythesis and simulation are matching






