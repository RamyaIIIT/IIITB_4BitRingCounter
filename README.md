# iiitb_4bit_ring_counter

This project simulates the designed 4 bit ring counter. A ring counter is a digital sequential circuit that recirculates the same data throughout the circuit. It is one of the applications of shift registers.

## Introduction
In this digital world, counters are the most important sequential logic circuits which are used widely in many day-to-day life applications such as microwave ovens, washing machines, digital clocks, timers and in many electronic devices such as frequency dividers, analog to digital converters, triangular waveform generators, etc. Any digital circuit which is used to count the number of occurrences of the input is called counter. The purpose of counters is not only for counting but also for measuring frequency and time.
Basically, counters are of 2 types: synchronous and asynchronous counters. If the change in transition occurs based on the clock input of the counter, then it is called synchronous counter. If not, then, it is called asynchronous counter. There are many other types of counters, such as decade counter, mod counter, binary counter, ring counter,etc. This paper mainly focuses on the ring counter only.

## Applications

Ring counters can be used in many applications such as:

- Frequency counter
- ADC
- Digital clocks
- Measure timers and rate, etc.


## Block Diagram of 4 bit Ring counter

 A ring counter is a synchronous counter which transfers the same data throughout it. It is a typical application of shift register and can be designed using either D or JK flip-flops (FFs). Here, a 4-bit ring counter is designed by a series of 4 D-FFs connected together in feedback manner. That means the output of the last FF is connected to the input of the first FF. The clock signal is applied to all the FFs simultaneously.


<p align="center">
  <img width="600" height="200" src="https://user-images.githubusercontent.com/110991148/184100206-85029b36-35d0-40cc-81f4-20be8b8cf800.png">
</p>


Initially all the FFs are at RESET state. When the PRESET is applied, the input of the ring counter becomes 1. Now the output of the first FF (Q3) is 1 and other FF outputs (Q2, Q1 and Q0) will be low. Then for the next clock signal, Q2 becomes 1 and others outputs will be low. In this way, as the clock input changes, the outputs change and the data sequence rotates in the ring counter.

<p align="center">
  <img width="500" height="200" src="https://user-images.githubusercontent.com/110991148/184101589-522df4ae-0d76-4678-a773-fdabf18a67d0.png">
</p>

State diagram is used to describe the behaviour of the digital sequential circuits. It shows the transitions of states from one state to the next as well as the output for a given input.

<p align="center">
  <img width="200" height="200" src="https://user-images.githubusercontent.com/110991148/184102424-cc93c3e2-7248-4dfb-aacf-4d85c1079bfb.png">
</p>

## About iverilog 
Icarus Verilog is a simulator tool to check the design with the help of test bench. The design is nothing but the Verilog hardware description language code which specifies the functionality. The testbench is the setup to apply stimulus to test the functionality of the design. This simulator looks for the changes to the input. Upon changes to the input, the output is evaluated.

<p align="center">
  <img width="600" height="200" src="https://user-images.githubusercontent.com/110991148/188372955-34ad0c1b-9cfb-48b8-ba87-63d5f3520a2b.png">
</p>

## About GTKWave
GTKWave is a fully featured GTK+ v1. 2 based wave viewer for Unix and Win32 which reads Ver Structural Verilog Compiler generated AET files as well as standard Verilog VCD/EVCD files and allows their viewing.

<p align="center">
  <img width="700" height="300" src="https://user-images.githubusercontent.com/110991148/188373214-2daeec8f-9bad-4f8d-90ba-93c9d239dfcf.png">
</p>

## About yosys

Yosys is a framework for Verilog RTL synthesis. It currently has extensive Verilog-2005 support and provides a basic set of synthesis algorithms for various application domains.

<p align="center">
  <img width="700" height="300" src="https://user-images.githubusercontent.com/110991148/188373894-09aa0924-e6cb-4f7d-91b7-fb3282ace0b5.png">
</p>

### Installing iverilog and GTKWave

Open your terminal and type the following to install iverilog and GTKWave
```
$   sudo apt-get update
$   sudo apt-get install iverilog gtkwave
```
### Installating yosys

Follow the steps from the below git repository to install yosys on Ubuntu.
https://github.com/YosysHQ/yosys/blob/master/README.md#installation
```
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys-master
$ sudo apt install make (If make is not installed please install it)
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make
$ sudo make install
```
### Functional Simulation
To clone the Repository and download the Netlist files for Simulation, enter the following commands in your terminal.
```
$   sudo apt install -y git
$   git clone https://github.com/RamyaIIIT/iiitb_4bitrc
$   cd iiitb_4bitrc
$   iverilog iiitb_4bit_ring_counter.v iiitb_4bit_ring_counter_tb.v
$   ./a.out
$   gtkwave dump.vcd
```
### Pre Synthesis Simulation Results
<p align="center">
  <img width="1000" height="500" src="https://user-images.githubusercontent.com/110991148/184847119-04b0d4cf-a9e6-429c-9742-c6e50a2d298e.png">
</p>

### Synthesis

Synthesis transforms the simple RTL design into a gate-level netlist with all the constraints as specified by the designer. In simple language, Synthesis is a process that converts the abstract form of design to a properly implemented chip in terms of logic gates.

Synthesis takes place in multiple steps:
-   Converting RTL into simple logic gates.
-   Mapping those gates to actual technology-dependent logic gates available in the technology libraries.
-   Optimizing the mapped netlist keeping the constraints set by the designer intact.
 
 <p align="center">
  <img width="700" height="300" src="https://user-images.githubusercontent.com/110991148/188374162-79803996-5721-4e32-8384-b57866c61275.png">
</p>

Invoke ''yosys' and execute the below commands to perform the synthesis of the above circuit.
```
$   read_liberty -lib ./lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$   read_verilog iiitb_4bit_ring_counter.v
$   synth -top -top ring_counter
$   dfflibmap -liberty ./lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$   abc -liberty -lib ./lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$   show
$   stat
```
### Netlist Representation
<p align="center">
  <img width="1000" height="500" src="https://user-images.githubusercontent.com/110991148/184844858-0e402890-9f47-4009-b632-4f0175463fac.png">
</p>

### Statistics after Synthesis
<p align="center">
  <img width="600" height="300" src="https://user-images.githubusercontent.com/110991148/185354248-91910694-817b-4bb6-bd3d-b04858487bf4.png">
</p>

### Gate Level Simulation (GLS)

GLS implies running the testbench with netlist as the design under test. It is used to verify the logical correctness of the design after synthesis. It also ensures that the timing constraints are met.

Execute below commands in the project directory to perform GLS.
```
$   iverilog -DFUNCTIONAL -DUNIT_DELAY=#0 ./verilog_model/primitives.v ./verilog_model/sky130_fd_sc_hd.v
$   ./a.out
$   gtkwave dump.vcd
```

### Post Synthesis Simulation Results
<p align="center">
  <img width="1000" height="500" src="https://user-images.githubusercontent.com/110991148/184847580-1f5cde40-8194-43ae-bfd3-ef42fb4c948e.png">
</p>

### Python Installation
```
$ sudo apt install -y build-essential python3 python3-venv python3-pip
```
### Docker Installation
```
$ sudo apt-get remove docker docker-engine docker.io containerd runc (to remove the older version of docker if already installed)
$ sudo apt-get update
$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release 
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null 
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
$ apt-cache madison docker-ce (copy the version string you want to install)
$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io docker-compose-plugin (paste the version string copies in place of <VERSION_STRING>)
$ sudo docker run hello-world (If the docker is successfully installed u will get a success message here)
```

### OpenLane Installation
```
$ git clone https://github.com/The-OpenROAD-Project/OpenLane.git
$ cd OpenLane/
$ make
$ make test
```
### Magic Installation
Before installing Magic, the following softwares have to be installed first:
```
$ sudo apt-get install csh (to install csh)

$ sudo apt-get install x11 (to install x11/xorg)
$ sudo apt-get install xorg
$ sudo apt-get install xorg openbox

$ sudo apt-get install gcc (to install gcc)

$ sudo apt-get install build-essential (to install build-essential)

$ sudo apt-get install freeglut3-dev (to install OpenGL)

$ sudo apt-get install tcl-dev tk-dev (to install tcl/tk)

$ git clone https://github.com/RTimothyEdwards/magic (to install magic)
$ cd magic
$ ./configure
$ make
$ make install

$ sudo apt-get install klayout (to install klayout)

$ sudo apt-get install ngspice (to install ngspice)
```
# Creating Custom Inverter Cell
```
$ git clone https://github.com/nickson-jose/vsdstdcelldesign.git
$ cd vsdstdcelldesign
$  cp ./libs/sky130A.tech sky130A.tech
$ magic -T sky130A.tech sky130_inv.mag &
```
<p align="center">
  <img width="500" height="500" src="https://user-images.githubusercontent.com/110991148/188389306-2730a27b-a435-4dff-9a03-023520666d01.png">
</p>

## Physical Design using Openlane
```
$ make mount (if this command doesnot go through prefix it with sudo)
$ ./flow.tcl -interactive
% package require openlane 0.9
% prep -design iiitb_4bitrc
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
% run_synthesis
```
## Synthesis Reports
<p align="center">
  <img width="500" height="500" src="https://user-images.githubusercontent.com/110991148/187889381-9620ac5f-be37-45aa-aa9e-1f8ef9d9f439.png">
</p>

## Contributors 

- **Ramya S** 
- **Kunal Ghosh** 


## Acknowledgments

- Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.

## Contact Information

- Ramya S, Ph.D Student, International Institute of Information Technology, Bangalore. ramya.suriyarani@gmail.com
- Kunal Ghosh, Director, VSD Corp. Pvt. Ltd. kunalghosh@gmail.com

## References:
- https://www.electronicshub.org/introduction-to-counters/
- https://eevibes.com/digital-logic-design/what-are-the-synchronous-and-asynchronous-counters/
- https://www.geeksforgeeks.org/ring-counter-in-digital-logic/
- https://verilogcodes.blogspot.com/2015/10/verilog-code-for-4-bit-ring-counter.html
