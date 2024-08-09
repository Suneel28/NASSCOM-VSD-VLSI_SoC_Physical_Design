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


Day 3 Design of Inverter cell using and transient chara of the designed cell using spice
We can see that the IO is placed diagonally equividistant in the floorplan.

<img width="592" alt="image" src="https://github.com/user-attachments/assets/ea5ebc5f-9a6a-4d97-8b98-fab6bab2dfea">

This is can be changed in the command present in config.tcl

In the next step we clone the inverter cell from the Github repository.

To Clone, run the following command in working directory: git clone https://github.com/nickson-jose/vsdstdcelldesign.git


<img width="620" alt="image" src="https://github.com/user-attachments/assets/3cbd1d96-c22c-4bd6-b7f6-f509bbf91fc3">


To open the layout in Magic tool, Use the command magic -T {absolute_path_of_the_tech_file_of_the_cell} {absolute_path_of_the_mag_file_of_the_cell}

The inverter std_cell which was cloned is opened as shown in the figure

<img width="616" alt="image" src="https://github.com/user-attachments/assets/62f12daf-0bea-4416-a759-7884d83865a9">

The files are generated as shown in the figure

<img width="609" alt="image" src="https://github.com/user-attachments/assets/a7681b82-e40b-4dce-b93d-c75171bf4fc9">


The following modifications are made in the spice file
<img width="599" alt="image" src="https://github.com/user-attachments/assets/1c90cab7-8ec6-43d1-bb0d-9f9cd53640b2">

<img width="271" alt="image" src="https://github.com/user-attachments/assets/ac1e892c-b14b-4ad4-97bf-2a17c91f2be7">

Next run the command plot y vs time a

<img width="602" alt="image" src="https://github.com/user-attachments/assets/887fe006-91fe-4b85-9aa8-53965dcd6b81">

Calculation of Rise time and Fall time Delay

Rise time is defined as the duration it takes for a signal to transition from 20% to 80% of its final value. The rise time can be calculated as [2.19 - 2.13[ x 10^-9 = 62.7 ps.

Zoom in to get the value of signal at 20% and 80% of VDD.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/0c4913cc-630f-4656-92f7-611cbb2e17f2">

The following values can also be obtained by the below method

<img width="588" alt="image" src="https://github.com/user-attachments/assets/a199ee5f-52d2-466f-b566-652f54d01d07">
Fall time is the duration it takes for a signal to transition from 80% to 20% of its final value. The fall time is calculated as [4.09 - 4.053] x 10^-9 = 41.97 ps.
<img width="581" alt="image" src="https://github.com/user-attachments/assets/bc54ced6-aee8-4146-b960-9b805b27e85c">
Calculation of Propagation Delay

Propagation delay is the time it takes for a signal to travel from the input to the output of a circuit. For instance, the propagation delay can be calculated as [2.15 - 2.10] x10^-9 = 48.9ps



The Screen shot of Propagation Delay

<img width="514" alt="image" src="https://github.com/user-attachments/assets/46e7b394-f14e-4c99-9be8-a138349fc5cb">


By Using command magic -d XR open the magic tool Open the met3.mag file

<img width="559" alt="image" src="https://github.com/user-attachments/assets/a7c655ee-0927-430e-8b02-1e1829ce248b">


To find the DRC Error, select the part containing the error and type the command why in the console

<img width="559" alt="image" src="https://github.com/user-attachments/assets/bb3a21b6-56b6-410e-84f8-87c00c38aa5e">


To see contact cuts execute the command cif see VIA2 in the console

<img width="526" alt="image" src="https://github.com/user-attachments/assets/4d488ba9-0382-4506-ad16-62f9be248a27">

There are many DRC errors found, to fix one of the error i.e, error poly.9 follow the follwing steps

nwell.mag is loaded

Find out why is the error occuring
<img width="602" alt="image" src="https://github.com/user-attachments/assets/bb76b18c-7240-4742-82b2-5a98b43c0432">


To fix this DRC error we make some changes in the sky130A.tech file





















