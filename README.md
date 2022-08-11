# iiitb_4bit_ring_counter

This project simulates the designed 4 bit ring counter. 

## Introduction
A ring counter is a digital sequential circuit that recirculates the same data throughout the circuit. It is one of the applications of shift register. 
<p align="center">
  <img width="800" height="500" src="/Images/pwm.jpeg">
</p>

## Applications

Pulse Width Modulated Wave Generator can be used to 

- control the brightness of the LED
- drive buzzers at different loudnes
- control the angle of the servo motor
- encode messages in telecommunication
- used in speed controlers of motors

## Blocked Diagram of PWM GENERATOR

This PWM generator generates 10Mhz signal. We can control duty cycles in steps of 10%. The default duty cycle is 50%. Along with clock signal we provide another two external signals to increase and decrease the duty cycle.


<p align="center">
  <img width="800" height="400" src="/Images/BasicBlockedDeagram.jpeg">
</p>

In this specific circuit, we mainly require a n-bit counter and comparator. Duty given to the comparator is compared with the current value of the counter. If current value of counter is lower than duty then comparator results in output high. Similarly, If current value of counter is higher than duty is then comparator results in output low.
As counter starts at zero, initially comparator gives high output and when counter crosses duty it becomes low. Hence by controlling duty, we can control duty cycle.

<p align="center">
  <img width="800" height="300" src="/Images/BlockDiagram.jpeg">
</p>

As the comparator is a combinational circuit and the counter is sequential, while counting from 011 to 100 due to improper delays there might be an intermediate state like 111 which might be higher or lower than duty. This might cause a glitch. To avoid these glitches output of the comparator is passed through a D flipflop.

## About iverilog 
Icarus Verilog is an implementation of the Verilog hardware description language.
## About GTKWave
GTKWave is a fully featured GTK+ v1. 2 based wave viewer for Unix and Win32 which reads Ver Structural Verilog Compiler generated AET files as well as standard Verilog VCD/EVCD files and allows their viewing

### Installing iverilog and GTKWave

#### For Ubuntu

Open your terminal and type the following to install iverilog and GTKWave
```
$   sudo apt-get update
$   sudo apt-get install iverilog gtkwave
```


### Functional Simulation
To clone the Repository and download the Netlist files for Simulation, enter the following commands in your terminal.
```
$   sudo apt install -y git
$   git clone https://github.com/sanampudig/iiitb_pwm_gen
$   cd iiitb_pwm_gen
$   iverilog iiitb_pwm_gen.v iiitb_pwm_gen_tb.v
$   ./a.out
$   gtkwave pwm.vcd
```

## Functional Characteristics
Simulation Results while increasing Dutycycle
<p align="center">
  <img width="800" height="300" src="/Images/incPWM.jpeg">
</p>

Simulation Results while decreasing Dutycycle
<p align="center">
  <img width="800" height="300" src="/Images/decPWM.jpeg">
</p>



## synthesis of verilog code

#### About Yosys
Yosys is a framework for Verilog RTL synthesis. It currently has extensive Verilog-2005 support and provides a basic set of synthesis algorithms for various application domains.

- more at https://yosyshq.net/yosys/

To install yosys follow the instructions in  this github repository

https://github.com/YosysHQ/yosys

- note: Identify the .lib file path in cloned folder and change the path in highlighted text to indentified path

<img width="1119" alt="image" src="https://user-images.githubusercontent.com/110079648/182905357-064fec34-3c2b-4997-a0b7-30453f505ddd.png">



#### to synthesize
```
$   yosys
$   yosys>    script yosys_run.sh
```

#### to see diffarent types of cells after synthesys
```
$   yosys>    stat
```
#### to generate schematics
```
$   yosys>    show
```


## Contributors 

- **Sanampudi Gopala Krishna Reddy** 
- **Kunal Ghosh** 



## Acknowledgments


- Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.

## Contact Information

- Sanampudi Gopala Krishna Reddy, Postgraduate Student, International Institute of Information Technology, Bangalore  svgkr7@gmail.com
- Kunal Ghosh, Director, VSD Corp. Pvt. Ltd. kunalghosh@gmail.com

## References:
- FPGA4Student
 https://www.fpga4student.com/2017/08/verilog-code-for-pwm-generator.html
