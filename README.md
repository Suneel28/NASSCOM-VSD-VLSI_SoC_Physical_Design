#DAY 1 Introduction to SoC Design Flow and Running Synthesis
#OPENLANE Flow
OpenLane is an open-source digital ASIC (Application-Specific Integrated Circuit) design flow that integrates a comprehensive set of tools for designing and implementing digital circuits. It is part of the broader effort to make VLSI (Very-Large-Scale Integration) design accessible and affordable by leveraging open-source tools and methodologies.

<img width="605" alt="image" src="https://github.com/user-attachments/assets/0a4aeaca-d697-4efc-8f81-412f4d32b5a0">
        
DESIGN PREPARATION

Open the OPENLANE Docker by using the command docker from the directory of 'openlane' inside 'openlane_working_dir' directory.

Then run the opelane in interactive mode using ./flow.tcl -interactive and run the command prep -design picorv32a to merge the lef file.

![Screenshot from 2024-07-25 22-50-22](https://github.com/user-attachments/assets/1ae5b3f6-e21f-41df-800e-ff8854d084f9)

After Design Preparation run the Synthesis command run_synthesis and Synthesis is Successful

![Screenshot from 2024-07-25 22-47-23](https://github.com/user-attachments/assets/735e6d43-6221-429c-bfab-627a6e599dc9)

Chip area after running the Synthesis is 147712.984 

![Screenshot from 2024-07-25 23-15-39](https://github.com/user-attachments/assets/92aaa87a-3acd-4dc5-b8a8-09d28def0910)

To calculate the flop ratio

Flop Ratio = Number of flops / Number of cells = 1613/14876 = 0.108 = 10.8%

![Screenshot from 2024-07-25 23-16-09](https://github.com/user-attachments/assets/a3352849-d084-4a2c-ad59-b0f9cdf1a14e)

![Screenshot from 2024-07-25 23-45-52](https://github.com/user-attachments/assets/a6ca43df-8098-4f94-a9e3-42953ae43ae3)

DAY2 Floorplan and Placement
Floorplan
There are various floorplan configurations that can be modified based on the requirement

![Screenshot from 2024-07-27 23-54-07](https://github.com/user-attachments/assets/7568b790-c96c-4cc6-ad35-5b464f338404)

Run the floorplan using run_floorplan

<img width="611" alt="image" src="https://github.com/user-attachments/assets/515e5ee9-24ed-4f2f-b580-e945a153a2d0">

The Configurations of floorplan are :-

![Screenshot from 2024-07-29 22-11-59](https://github.com/user-attachments/assets/8157e9d7-f968-440f-8b8c-0c455ae49e23)

MAGIC Tool
The Magic tool is an open-source layout editor used for VLSI design. It provides a graphical interface for viewing and editing IC layouts, allowing designers to inspect and modify the floorplan, placement, and routing of their designs. Magic is widely used for its ease of use and integration with other tools in the ASIC design flow.

To open the magic window use the command :
magic -T home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def & 


<img width="612" alt="image" src="https://github.com/user-attachments/assets/f39a9821-26a2-439c-8484-4ee9b4648966">

The cells in the layout can be identified by selecting the cell and typing the command what in the console

![Screenshot from 2024-07-29 22-29-12](https://github.com/user-attachments/assets/70f9cf61-cc7a-4459-8fc6-1d8c91a01939)

Placement

To run the placement type the command run_placement

![Screenshot from 2024-07-29 22-03-53](https://github.com/user-attachments/assets/8ed3d879-eb06-482d-b72e-85d0f07b3504)

We perform the global placement first which is used to achieve less wire length.

To Open the layout after placement type the command magic -T home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def & 

![image](https://github.com/user-attachments/assets/dedea326-04c7-47fe-ba75-2d3977926e00)











