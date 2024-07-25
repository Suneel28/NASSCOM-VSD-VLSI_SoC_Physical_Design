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




