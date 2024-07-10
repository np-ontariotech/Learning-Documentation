# Learning Notes for CPU Visual Simulator
**Link title:** CPU Visual Simulator  
**URL:** https://cpuvisualsimulator.github.io/

## Summary of website content 
#### Initial GUI, Simulation Experience
The initial website GUI provides a visual simulation of the basic components of a CPU and the RAM.
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/2bccc747-d693-444f-9793-515398789fce)

CPU components:
- Instruction Register
- Control Unit
- MUX
- Arithmetic Logic Unit
- Accumulator
RAM:
- Address in RAM
- Info stored at that address
Connectionsa between the CPU and RAM
- Data Bus
- Address Bus
- Control Bus
In addition to the simulatred CPU & RAM, the website provides a control panel at the bottom of the website which includes a control bar for the program, a box that allows you to toggle binary and simulation animatiions, and a text box which provides information on what the simulator is doing.
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/f9fcf46d-0f73-49bf-9d0b-93a9e441aba6)

#### Additional Features
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/c6727089-6b51-48e4-aa75-09596341e2cb)

The website provides additional features to modify the simulation experience. Such as:
1. Manual
  - Details information regarding the history and purpose of this tool; a description for each of the instruction set terms that the CPU simulator supports;  keyboard shortcuts; a guide on how to write, load, and save files that this visualization supports; and examples of pseudocode and their associated simulation instruction set.
2. Examples
  - Allows the user to select from three pre-defined popular programming operations. Selecting any of these options will edit the simulation to run the selected operation.
3. Load
  - Allows the user to load a .cpuvs file to populate the simulator.
4. Save
 -  Allows the user to save the current view of the simulation as either a URL or a .cpuvs file.
5. Settings
  - Allows the user to change various high-level settings of the simulation (such as language and the ability to see explanatory text in the control panel text box); configure text to speech settings; change the color of the various elements in the simultor.

## Key takeaways
#### Running a While Do Example
This section describes the use of the simulation to understand how a CPU processes a program.
1. First 3 steps: initializing the loop variables
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/f9004664-a3d8-4bae-b78f-ad9d852accec)
   - To run the while loop, the CPU first has to populate some ram addresses for the SUM and COUNT variables. To do this, the CPU first has to introduce integers into the equation. It does this by running the immediate LOD instruciton, so that the accumulator holds an integer that can be assigned to addresses within ram. Once the integer 0 is in the accumulator, it can be stored in other ram locations for SUM and COUNT using the direct STO instruction and specifying the SUM, then COUNT addresses in ram.
     ![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/ed903766-f593-48d5-8ce6-3cb0c3fa2fde)
     ![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/e7ca2c23-84c5-432f-9c66-994a1c0ab46a)

 2. Compare the current iteration of the loop to the max amount of iterations the loops wants to perform.
    ![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/7bdbb424-bd2a-4a84-8a63-410b5822ce7d)
    1. First, the CPU loads (LOD) the data stored at the MAX address (24) in memory. This is achieved by first retrieving the LOD instruction by accessing memory 6 in the address BUS, an enable signal being sent via the control BUS, then receiving the instruction via the data bus to the instruction register. The instruction register then decodes the instruction, signals address 26 in memory, then sends an enable signal via the control bus to retrieve the integer held at address 26 and load it into the ALU by first passing it into the MUX, then into the ALU. (**Descriptions of how the bus functions will be ommitted onwards, to avoid verbose repitition**) 
    2. D


#### Binary, bits, and the CPU
Talk about how bit size/length is relevant to how a CPU runs. E.g. going from 4 bit to 64 bit processors, and how that reflects in the length of the instruction binary that the CPU can process.

## Personal Insights or reflections
#### The limits of the CPU
I was under the impression that the CPU was in charge of doing a lot more work at its most fundamental level. However, this simulation has taught me that the CPU only performs arithmetic and logic functions on data expressed as binary. This has opened my eyes to the amount of abstractions that are required to turn this fundemtal binary processing into more complex instructions that need to be interpreted by devicies like the display. 


## Feedback and Reflections
