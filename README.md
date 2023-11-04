
# pes_aclock
  - [Implementation of an Alarm Clock in Verilog This project carries out the design and development of a fully implementable Verilog code of a working digital]
# Contents
- [alarm_clock](#alram_clock_introduction)
 - [Iverilog and yosys installation](#iverilog-and-yosys-installation)
  - [GLS Process to verify alarm_clock][[#GLS-Process-to-verify-alarm-clock]
  - [Installation of ngspice magic and OpenLANE]
    - [OpenLANE Flow]

 
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


#### OpenLane
OpenLane is an open-source VLSI flow built around open-source tools. That is, it's a collection of scripts that run these tools, in the right order, transforming their inputs and outputs as appropriate, and organising the results. It is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, SPEF-Extractor, CU-GR, Klayout and a number of custom scripts for design exploration and optimization. The flow performs full ASIC implementation steps from RTL all the way down to GDSII.

For installation of OpenLane, type the follow the below steps.

Installing python as it is a pre-requisite:
```
$   sudo apt install -y build-essential python3 python3-venv python3-pip
```
For installing Docker Engine on Ubuntu, use the following link -- https://docs.docker.com/engine/install/ubuntu/.

Next, go to the `iiitb_aclock` directory and type the following in the terminal:

```
$   git clone https://github.com/The-OpenROAD-Project/OpenLane.git
$   cd OpenLane
$   sudo make
```

Now, to check that OpenLane dependencies are succesfully installed, run the test command:

```
$   sudo make test
```
If the line `Basic test passed` is printed in the terminal, then the installation is successful.

#### Magic
Magic is an electronic design automation (EDA) layout tool for very-large-scale integration (VLSI) integrated circuit (IC) originally written by John Ousterhout and his graduate students at UC Berkeley. Due largely in part to its liberal Berkeley open-source license, magic has remained popular with universities and small companies. The open-source license has allowed VLSI engineers with a bent toward programming to implement clever ideas and help magic stay abreast of fabrication technology. However, it is the well thought-out core algorithms which lend to magic the greatest part of its popularity. Magic is widely cited as being the easiest tool to use for circuit layout, even for people who ultimately rely on commercial tools for their product design flow.

For installation of magic, type the following commands in your terminal in the `pes_aclock` directory to install dependencies:
```
$   sudo apt-get install m4
$   sudo apt-get install csh
$   sudo apt-get install tcsh
$   sudo apt-get install libx11-dev
$   sudo apt-get install tcl-dev tk-dev
$   sudo apt-get install libcairo2-dev
$   sudo apt-get install mesa-common-dev libglu1-mesa-dev
$   sudo apt-get install libncurses-dev
```

To install Magic, type the following in the terminal:
```
$   git clone https://github.com/RTimothyEdwards/magic
$   cd magic
$   ./configure
$   sudo make
$   sudo make install
```
To check if Magic has been successfully installed, type the command `magic` in the terminal.

![Screenshot from 2023-11-04 13-10-24](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/59a4eebc-3e5a-4258-b4b5-1cdcac46a128)

### Generating Layout
#### Creating custom inverter cell
To design a custom inverter cell, include it in library and get it in the final layout, clone the following repo:
```
$   git clone https://github.com/nickson-jose/vsdstdcelldesign.git
$   cd vsdstdcelldesign
$   cp ./libs/sky130A.tech sky130A.tech
$   magic -T sky130A.tech sky130_inv.mag
```
The following Magic windows should appear:


![Screenshot from 2023-11-04 13-11-40](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/903fd1fb-c735-4a5b-a27c-68e4a250d8de)

![Screenshot from 2023-11-04 13-11-58](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/9280f2a4-4238-407d-8f9e-5f8444b26e0b)

## STEP-1:

To start with the Flow we first need to write the verilog code for the idea to create a ".v" file and we even write the testbench for the file which we will be implement together in the iVerilog tool in order for it to generate a dump file to view the waveform.

`vim pes_aclock.v`

![Screenshot from 2023-11-04 20-32-20](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/92bcb292-0835-4eb4-862b-f5163929dbb0)

##STEP-2 :
###OPENLANE FLOW
![Screenshot from 2023-11-04 21-30-18](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/60908d9b-abbf-4677-8b3d-398abb5babe6)


- Type ```make mount``` in the main Openlane folder.
- Then type ```./flow.tcl -interactive```.
- To prep the design type
- ![Screenshot from 2023-11-04 21-33-20](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/488a3ac7-eb45-415e-bc14-c9631f93376c)

RTL synthesis

**what do we do in RTL synthesis?**

Synthesis transforms the simple RTL design into a gate-level netlist with all the constraints as specified by the designer. In simple language, Synthesis is a process that converts the abstract form of design to a properly implemented chip in terms of logic gates.

Synthesis takes place in multiple steps:
-   Converting RTL into simple logic gates.
-   Mapping those gates to actual technology-dependent logic gates available in the technology libraries.
-   Optimizing the mapped netlist keeping the constraints set by the designer intact.
-   ![Screenshot from 2023-11-04 21-37-18](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/345d20a2-5758-46cf-bd45-b31a4152f2dd)

</details>
Routing

    Now to run routing we type


![Screenshot from 2023-11-04 22-20-30](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/6ce4311e-f464-4e0f-82e5-b69b5b88d2ff)

![Screenshot from 2023-11-04 21-39-38](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/569be1dd-1a65-4e18-a21d-3c50c456a03c)

## to view the design we type 
```sh
magic -T /home/nagesh/Desktop/sky130A.tech lef read ../../tmp/merged.nom.lef def read pes_aclock.def &
```
![Screenshot from 2023-11-04 22-46-48](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/cda0fbc9-8692-411d-95d9-90a0fd8beb34)

## congention report
![Screenshot from 2023-11-04 22-50-24](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/f28e5412-36ea-4639-8981-6b111c9b7352)


The reports generated are given below
![Screenshot from 2023-11-04 22-09-51](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/13354b7c-7121-499e-a474-231e6cad0a0e)
![Screenshot from 2023-11-04 22-10-58](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/3b261e32-01dd-4f10-a1a7-f3be6117c05c)
![Screenshot from 2023-11-04 22-11-52](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/e9a39e85-b43b-4299-8851-0383dd018933)

![Screenshot from 2023-11-04 22-12-38](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/52e953ab-09b9-48a8-9ec7-1a8554d2d4df)
###Power Report
![Screenshot from 2023-11-04 22-15-24](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/d9630c32-ab83-44d6-b243-4d0c019084d0)

###skew report 
![image](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/85fc3c69-ccc1-41f8-ad98-ee250878c4ca)






area report

![Screenshot from 2023-11-04 22-19-17](https://github.com/Shrachinag/pes_alarm_clock/assets/119600435/b76601aa-dfd3-4059-8b52-8c600960da4a)

```
    Area = 243 u^2 17% utilisation
    Internal Power = 6.77e-05 W 86.3% 
    Switching Power = 1.08e-05 W 13.7%  
    Leakage Power = 1.97e-10 W  0.0%
    Total Power = 7.85e-05 W
```













