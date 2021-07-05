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

DAY1 - Introduction to the requirements and the openlane flow
------------------------------------------------------------

![ASIC](https://user-images.githubusercontent.com/79994584/114556720-9b4d0980-9c86-11eb-91b1-140c0859d758.png)

![openlane](Images/Day1/openlane.flow.png)

![openlane-start](Images/Day1/op1.png)

![pdk](Images/Day1/op2-pdk.png)

![prep](Images/Day1/op3-prep.png)

![config](Images/Day1/op4-config.png)

![runs](Images/Day1/op4-runs.png)

![picorv32a](Images/Day1/opt6-synthesis-picorv32.png)
------------------------------------------------------------
DAY2 - Introduction to floorplaning and considerations
------------------------------------------------------------
![floorplan](Images/Day2/day2-voltage-drop.png)
![floorplan](Images/Day2/day2-ground-bounce.png)
![floorplan](Images/Day2/day2-timing-variable.png)
![floorplan](Images/Day2/day2-modular.png)
![floorplan](Images/Day2/day2-floorplan.png)
![floorplan](Images/Day2/day2-magic-floor-plan.png)
![floorplan](Images/Day2/day2-horzontal.png)
![floorplan](Images/Day2/day2-vertical.png)
![placement](Images/Day2/day2-placemnet.png)
![routing](Images/Day2/day2-routing.png)
------------------------------------------------------------

DAY3 - Introduction to custom cells and sky130tech file
------------------------------------------------------------

------------------------------------------------------------

DAY4 - Integration of custom cell into picorv32a synthesis and **STA**
------------------------------------------------------------

------------------------------------------------------------

DAY5 - Introduction to routing and power grids
------------------------------------------------------------