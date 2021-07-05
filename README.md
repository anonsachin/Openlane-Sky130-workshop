Advance Physical Design using OpenLANE and SkyWater 130nm PDK
=============================================================

This workshop consisted of using the **OpenLANE** flow and the **Skywater 130nm PDK** to take a `verilog` design to **GDSII** which can then be used to tap-out the design.

![image](https://user-images.githubusercontent.com/79994584/114469850-7ff0e880-9c0b-11eb-9a06-cac7f32717ec.png)

----------------------------------------------------------

Contents
--------

- *Day 1*
    - How to talk to computers
    - SoC design and OpenLANE
    - Starting RISC-V SoC Reference design
    - Get familiar to open-source EDA tools

-  *Day 2*
    - Chip Floor planning considerations
    - Library Binding and Placement
    - Cell design and characterization flows
    - General timing characterization parameters

- *Day 3*
    - Labs for CMOS inverter ngspice simulations
    - Inception of Layout – CMOS fabrication process
Sky130 Tech File Labs

- *Day 4*
    - Timing modelling using delay tables
    - Timing analysis with ideal clocks using openSTA
    - Clock tree synthesis TritonCTS and signal integrity
    - Timing analysis with real clocks using openSTA

- *Day 5*
    - Routing and design rule check (DRC)
    - PNR interactive flow tutorial

------------------------------------------------------------

DAY1 - Introduction to openlane, the need and  requirement openlane
------------------------------------------------------------

### **ASIC**

ASIC (Application Specific integrated cicuit) are devices that built as the name suggests specific uses. The requirements to build them are as shown below

![ASIC](https://user-images.githubusercontent.com/79994584/114556720-9b4d0980-9c86-11eb-91b1-140c0859d758.png)

You need all three elements even if one them are missing you cannot completely develop it. The EDA tools and PDK's were till recently not opensource, but with the release of opensource have democratized the ASIC design space.

- RTL IP - RTL's opensourced with github and other places
- PDK Data - with the introduction [skywater pdk](https://github.com/google/skywater-pdk)
- EDA tools - tools and flows like qflow, openlane etc...

### **OpenLANE**

![openlane](Images/Day1/openlane.flow.png)

Openlane is a set of tools bundled together that facilitate the flow of **ASIC** design from **RTL to GDSII**. It consists of the following tools bundled in the form of a docker container.
```
    - OpenROAD
    - Yosys
    - Magic
    - Netgen
    - Fault
    - OpenPhySyn
    - CVC
    - SPEF-Extractor
    - CU-GR
    - Klayout
    - custom methodology scripts 
```
once you are in the docker container you can start using it by runnning

```
    // this will get you an interactive 
    // way of interfacing with the tool
    ./flow.tcl -interactive 
    // Specify the PDK_ROOT env to point to 
    // the pdk to be used.
```

![openlane-start](Images/Day1/op1.png)

### **Skywater-130 PDK**

PDK is what allows us to interface with fabs to get the IC's made, they provide the rules and other details required to make it happen. Google and Skywater foundry have worked together to opensource there `130nm` process.

![pdk](Images/Day1/op2-pdk.png)

Now we can load our designs into with 
```
    package require openlane 0.9 // to get the packages
    prep -design <name of you design>
```
for it to be read the design has to be located in a particular location of your current directory as shown below. This is just a barebones requirement.
```
designs
└── <name of your design>
    ├── config.tcl
    └── src
        └── < your filename>.v
```
- load design
![prep](Images/Day1/op3-prep.png)

- config of the picorv32a design used
![config](Images/Day1/op4-config.png)

- contents of a run
![runs](Images/Day1/op4-runs.png)

You can then generate the netlist of your design by running

```
    run_synthesis
```
- synthesis
![picorv32a](Images/Day1/opt6-synthesis-picorv32.png)

------------------------------------------------------------

DAY2 - Introduction to floorplaning and considerations
------------------------------------------------------------

For the floorplaning of the SoC, which is the process of defining which all elements need to be placed and where.

- Die - this is the complete encapsulation of the IC, including the logic gate, IP's and Pads

- Pre-Placed cells - These are like other entities that need to be placed in the cell for its functionality and once placed are not moved after.

- Decoupling capacitors - these are capacitors added to make sure that output of the logical function stays in a good range and does not fall below or above the noise margin

- Pin placement - the location of the pins that interface the outside world, there are different stratergies available for this

- Power planning - The way power lines are routed through the chip should be considered and not rely on a single power source, it will lead to the following problems.
    - Voltage drop
    ![floorplan](Images/Day2/day2-voltage-drop.png)
    - Ground Bounce
    ![floorplan](Images/Day2/day2-ground-bounce.png)
<!-- ![floorplan](Images/Day2/day2-modular.png) -->

You can generate the floor plan by running
```
    run_floorplan
```
- generated files in magic
![floorplan](Images/Day2/day2-floorplan.png)
![floorplan](Images/Day2/day2-magic-floor-plan.png)
- The pins in the floor plan
![floorplan](Images/Day2/day2-horzontal.png)
![floorplan](Images/Day2/day2-vertical.png)

### **Placement**

This is the process of creating the placement of our netlist on to the floor plan. There are two stages

- Global placement - where the elements are grouped together and there is a coarse placement.

- Detailed  placement - adds more details to the different groups of the coarse placement

we can run the following command for it
```
    run_placement
```
The placement viewed in magic

![placement](Images/Day2/day2-placemnet.png)
<!-- ![routing](Images/Day2/day2-routing.png) -->

------------------------------------------------------------

DAY3 - Introduction to custom cells and sky130tech file
------------------------------------------------------------

![magic](Images/Day3/day3-invertor-custom.png)
![extract to spice](Images/Day3/day3-extract.png)
![spice](Images/Day3/day3-spice-inv.png)

![floorplan](Images/Day2/day2-timing-variable.png)
![rise-delay](Images/Day3/day3-rise-delay.png) 
![fall-delay](Images/Day3/day3-fall-delay.png)
![fall-propagation](Images/Day3/day3-fall-propagation-delay.png)

![drc-poly](Images/Day3/day3-poly9.png)
![drc-metal](Images/Day3/m3-day3.png)

------------------------------------------------------------

DAY4 - Integration of custom cell into picorv32a synthesis and **STA**
------------------------------------------------------------

![magic-base](Images/Day4/day4-inv-placement.png)
![magic-place](Images/Day4/day4-expand-inv-placement.png)
![synthesis](Images/Day4/day4-inv-synthesis.png)

![to-lef](https://raw.githubusercontent.com/nickson-jose/vsdstdcelldesign/master/Images/layout_vs_LEF.JPG)

![setup](Images/Day4/skew.png)
![hold](Images/Day4/full-hold.png)

![sta-area](Images/Day4/day4-area-set.png)

------------------------------------------------------------

DAY5 - Introduction to routing and power grids
------------------------------------------------------------
[lee's algorithm](https://www.vlsisystemdesign.com/maze-routing-lees-algorithm/)
![lee's](https://www.vlsisystemdesign.com/wp-content/uploads/2016/12/least_derouted_path.jpeg)

![trionroute](Images/Day5/route-image.png)

![power-plan](Images/Day5/power_planning.png)

------------------------------------------------------------

Acknowledgements
----------------
1. Kunal Ghosh - Co-founder (VSD Corp)
2. Nickson Jose - Teaching Assistant
3. Mansi Mohapatra - Teaching Assistant
4. Mili Anand - Teaching Assistant