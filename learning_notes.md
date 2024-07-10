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
**Running a While Do Example**
This section describes the use of the simulation to understand how a CPU processes a program.
1. First 3 steps: initializing the loop variables

**Binary and Bits**
Talk about how bit size/length is relevant to how a CPU runs. E.g. going from 4 bit to 64 bit processors, and how that reflects in the length of the instruction binary that the CPU can process.

## Personal Insights or reflections
**The limits of the CPU**
I was under the impression that the CPU was in charge of doing a lot more work at its most fundamental level. However, this simulation has taught me that the CPU only performs arithmetic and logic functions on data expressed as binary. This has opened my eyes to the amount of abstractions that are required to turn this fundemtal binary processing into more complex instructions that need to be interpreted by devicies like the display. 


## Feedback and Reflections
