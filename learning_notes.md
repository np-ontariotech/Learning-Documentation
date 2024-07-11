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
In addition to the simulated CPU & RAM, the website provides a control panel at the bottom of the website which includes a control bar for the program, a box that allows you to toggle binary and simulation animations, and a text box which provides information on what the simulator is doing.
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/f9fcf46d-0f73-49bf-9d0b-93a9e441aba6)

#### Additional Features
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/c6727089-6b51-48e4-aa75-09596341e2cb)

The website provides additional features to modify the simulation experience. Such as:
1. Manual
  - Details information regarding the history and purpose of this tool; a description for each of the instruction set terms that the CPU simulator supports; keyboard shortcuts; a guide on how to write, load, and save files that this visualization supports; and examples of pseudocode and their associated simulation instruction set.
2. Examples
  - Allows the user to select from three pre-defined popular programming operations. Selecting any of these options will edit the simulation to run the selected operation.
3. Load
  - Allows the user to load a .cpuvs file to populate the simulator.
4. Save
 -  Allows the user to save the current view of the simulation as either a URL or a .cpuvs file.
5. Settings
  - Allows the user to change various high-level settings of the simulation (such as language and the ability to see explanatory text in the control panel text box); configure text to speech settings; change the color of the various elements in the simulator.

## Key takeaways
#### Running a While Do Example
This section describes the use of the simulation to understand how a CPU processes a program.
1. First 3 steps: initializing the loop variables
   
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/f9004664-a3d8-4bae-b78f-ad9d852accec)
   - To run the while loop, the CPU first has to populate some ram addresses for the SUM and COUNT variables. To do this, the CPU first has to introduce integers into the equation. It does this by running the immediate LOD instruction, so that the accumulator holds an integer that can be assigned to addresses within ram. Once the integer 0 is in the accumulator, it can be stored in other ram locations for SUM and COUNT using the direct STO instruction and specifying the SUM, then COUNT addresses in ram.
     ![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/ed903766-f593-48d5-8ce6-3cb0c3fa2fde)
     ![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/e7ca2c23-84c5-432f-9c66-994a1c0ab46a)

 2. Compare the current iteration of the loop to the max amount of iterations the loops wants to perform.
    
    ![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/7bdbb424-bd2a-4a84-8a63-410b5822ce7d)
    1. Address 6: the CPU loads (LOD) the data stored at the MAX address (24) in memory. This is achieved by first retrieving the LOD instruction by accessing memory 6 in the address BUS, an enable signal being sent via the control BUS, then receiving the instruction via the data bus to the instruction register. The instruction register then decodes the instruction, signals address 26 in memory, then sends an enable signal via the control bus to retrieve the integer held at address 26 and load it into the ALU by first passing it into the MUX, then into the ALU. This is the start of each iteration. (**Descriptions of how the bus functions will be omitted onwards, to avoid verbose repetition**) 
    2. Address 8: The CPU then loads the integer stored at the max address in RAM into the ALU. This performs a CMR instruction, which will result in the Z or N flag switching to indicate whether the previously loaded value in the ALU is equal to the value stored at MAX (computed via subtracting value at max from value currently in accumulator). Because the count is 0 and the max is 5 in the first iteration, the Z flag is update to 0, to indicate the values were not equal. 
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/01ea4068-e5f0-4978-ac35-2cb9cd1e643c)

    3. Address 10: The CPU is then given the JZ instruction, which will jump to the ending condition of the loop (stored at memory address 22 in the form of a HLT instruction). This is the portion of the loop that checks before the start of each iteration to determine if the end condition has been met or not. Because the first iteration does not have the Z flag set, the next address in memory is passed to the CPU.

![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/12ddec0e-a879-4871-bc40-f8d13784b115)
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/cf289431-82dc-4f26-8e4c-69f5b4a028d3)

 3. Execute the desired instructions to be followed in each iteration.

    ![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/678e7c2f-f4e8-4a86-9064-a1d548961812)
    1. The first step of the iteration is to update the count variable by 1, to indicate a new iteration has been performed. This is achieved using the ADD instruction then the STO instruction to update count + 1 to the count address in memory.


    2. The next step in the iteration is to take the previously loaded and computed current iteration number, and add the integer held in the sum address. This new value is then stored in the sum address, where it will be re-retrieved in every iteration. Once this has been achieved, the loop then resets by passing a JMP instruction that brings the CPU back to the memory address where the initial instruction for each iteration is held (6, labeled "WHILE:"). The above-described loop then repeats until count is equal to the integer held at MAX address in memory (26: 5). For this program, execution ends with a final sum of 15, and the Z flag set to 1 last, where it would have jumped to the HLT instruction.

    
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/6202a0b9-60c9-4fe8-a363-171540c06b95)
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/03b1d536-78d3-49b7-8eb9-a6a1bfc59983)
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/b7d0b9f5-76af-4f48-a861-db28b1baa680)



#### Binary, bits, and the CPU
It is important to note that the CPU only works with binary. In the above description, we described the CPU in human-readable conversions of binary (10-based numbers and strings for instructions and ram labels). This is extremely important in considering the CPU architecture. Specifically, the number of bits that the CPU components are able to process. In a 4-bit CPU, this would range from 0000 to 1111. Whereas for a 64-bit CPU, this range is in binary 64-digits long. This architecture is key in describing not only what the ALU and other components can process, but in the required width of the bus so that it is able to transmit the 64 bit wide data. From this understanding, it is much easier to interpret how important advances were in CPU bit size to be able to interpret more complex instructions. 

## Personal Insights or reflections
#### The limits of the CPU
I was under the impression that the CPU was in charge of doing a lot more work at its most fundamental level. However, this simulation has taught me that the CPU only performs arithmetic and logic functions on data expressed as binary. This has opened my eyes to the amount of abstractions that are required to turn this fundamental binary processing into more complex instructions that need to be interpreted by devices like the display. 

#### The key role of RAM
Prior to this course, I almost never paid attention to RAM or considered RAM in my programming, only ever a concern when an out of memory error was raised. I had always been under the impression that the RAM served a role of storage similar to a HHD storage but faster. However, I am now much more aware of the crucial role RAM serves with respect to the CPU. From now on, I will directly imagine how source code is processed through the RAM and into the CPU. 

## Feedback and Reflections
