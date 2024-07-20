# Learning Notes for A Survey of Computer Architecture Simulation Techniques and Tools
**Paper Title:** A Survey of Computer Architecture Simulation Techniques and Tools  
**Authors:** Ayaz Akram; Lina Sawalha  
**URL:** https://ieeexplore.ieee.org/document/8718630  

**General Description:** This paper surveys and compares various popular computer simulators. The paper focuses more so on full-computer simulators that are primarily used in professional or academic research, as opposed to our previous simulators that focused mainly on the CPU and were comparatively elementary.  

## Article Summary
### Introduction
The purpose of the researchers in writing this article was to compile an extensive survey of the most widely available computer architecture tools to help other researchers determine which simulator if best for their research use case. It builds  on, but differs, to some other existing academic simulator surveys which are cited in the introduction segment of the paper.
The scope of this paper is on computer architectural and microarchitectural simulators and simulation models, as opposed to more specialized simulators. It is broken down into the following categories (shown as headings).
Useful image that represents the host (computer running sim), the target (the computer system being simmed) and the guest OS (workload simmed) and the relationship between them:  
![image](https://github.com/user-attachments/assets/d4dff094-318b-45be-b9d3-d4cdca7a9eb7)


### Classification of simulators
#### Details of simulation
I.e. the level of detail that the sim implements in its design.
1. Functional Simulators
	1. Simulates the architecture only , beavhing like an emulator, while not implementing the microarchitecture. an important goal is correctness in simulating the ISA. Focuses on the "what" not on the "how"
	2. e.g. Sim-fast
2. Timing Simulators
	1. Simulates the microarchitecture of processors. Models this lower level to better focus on the "how" of the processor instead of ensuring the correctness of the "what"
	2. 3 sub-types 
		1. Cycle-level simulators
			1. Imitates the operations of the processor for each cycle.
			2. Slow and use a lot of memory.
			3. E.g. Sim-fast
		2. Event-driven simulators
			1. Simulates based on events instead of cycles.
		3. Interval simulator
			1. 
3. Integrated Timing and FUnctional Simulators
	1. A mix of functional and timing sims to create more flexible and accurate sim. 
	2. 3 Sub-types ![image](https://github.com/user-attachments/assets/fce5f19d-ecf9-4265-ba77-21839a2fcfd2)

		1. Timing-Directed
			1. Uses the timing model to act as an interface and send directions to the functional model.
			2. Allows for more accurate modelling and modelling more complex architectures like multicore architectures
			3. e.g. Asim
		2. Functional First
			1. Functional model runs ahead of the timing model sending it traces to get data from the timing model, but with the functional model still leading the simulation.
			2. Easier to implement & can be faster than timing-direct, BUT can be less accurate.
			3. e.g. SimWattch
		3. Timing First
			1. Opposite to functional first: timing model runs first, simulating the microarchitecture and then using the functional model to verify the correctness.
			2. Its main advantage lies in its accuracy, combining the details from a timing model with the correctness of a timing model.
			3. e.g. GEMS

#### Scope of target
I.e. what, and to what extent, is the simulator trying to simulate.
1. Full-System Simulator
	1. Able to completely boot the OS it is simulating and run benchmarks as they would run on a real target implementation. 
	2. Can be timing sim (e.g. gem5) or functional sim (e.g. SimOS).
2. Application Level/User Mode Simulator
	1. More light-weight, designed to model the behaviour of an application running on the target without all the overhead in simulating the target as in a full-system simulation.
	2. e.g. SimpleScalar, SESC, SNiper, RSim

#### Input to the simulator
1. Traces-Input
	1. Inserts "traces" pre-recorded sequence of instructions on the memory. These traces can be very large files but the sim results are reproducible and often have greater speed.
	2. E.g. Cheeta
2. Executables-Input
	1. Takes direct executables in the format of input like binary. Often this sim is used for the performance of specific regions of code insread of entire benchmark applications.
	2. E.g. SimpleScalar

#### Other Sim Categories
- Multiprocessor/Multicore
	- Categorizes based on sequential (where all targets cores are simulated on a single thread) or parallel simulation (where multiple sim threads are utilized); i.e. representing multiple cores. 
- Energy and Power Simulators
	- An increasingly important goal of simulation is to measure the power and energy impacts of a computer (the author states this to be the case due to the end of Moore's law requiring us to work on optimizing from existing architecture instead of depending on more transistors being placed in chips)
	- e.g. Wattch
- Specialized Simulators
	- Used to simulate very specific parts of a specific target architecture.
	- e.g. Cachesim5, simulates just cache
- Modular SImulators
	- As the name hints, modular sims segment different parts of the target into modules that work together to sim.
	- e.g. Asim (modular representation of SimpleScalar)

### Evaluating Simulators
The author notes there are six trade-off metrics to observe in evaluating sims:
1. **Accuracy**: performance accuracy of target sim to real target.
2. **Performance**: How fast the sim can run in simulating the target architecture.
3. **Level of details**: The amount AND level of details in representing the target.
4. **Easiness of development**
5. **Flexibility**: Configurability of the sim AND its ability to have structures modified or added.
6. **User friendliness**: How easy it is for a user to learn and use the sim.


### Research Findings in Comparing Popular Modern Simulations
Methodology: Targeted a system based on core i7-4770. Using the different sims for this target, specific benchmarks were ran (SPEC-CPU2006 and some MiBench embeeded benchmarks)

The actual results from the findings are too numerous and complex to accurately depict in the scope of these notes. Refer to the final pages of the paper for in-depth results and graphics. Here are some excerpts:
- Sniper: produces minimum absolute error
- ZSim: fastest single-core sim
- Modular simulators combined with full documentation result in the most flexible and easy to use sims.
- There is a great need for innovation in how to validate sims, specifically regarding their accuracy to the target.


## Critical Analysis
### Major Advantages of Simulating Computing Applications
1. Accurate performance evaluation
	2. When operating on the specific architecture you want to analyse, it is very difficult to accurately measure evaluation in a means that is reproducible over time. Simulating enables us to solve this. 
2. Ability to optimize
	1. Having the ability to tinker with various aspects of the architecture before actually implementing it on a real system can allow for much greater optimization of a computing strategy. If Moore's law is dying, as suggested in the article, this specific advantage is very important, as optimization on current technology will be required.
3. Optimize the efficiency of resources
	1. Related to the second advantage, having the ability to simulate multiple target architectures allows the user of the simulator to understand how different architectures differ in targeting the benchmark the user cares about. As a result, the user can then use their resources (time, money, etc.) on implementing the architecture they know best addresses their use case

### Potential Limitations
For specific limitations related to any individual simulator or category (as described in the categories section) of simulators, please refer to the paper from which these notes are derived. The below looks at higher level limitations across most if not all simulations and for most use cases (keeping in mind different simulation goals will have more relevant limitations)
1. **Simulator Performance**, necessarily slow
	1. For sims that have reliable and accurate timings for the target it implements, it takes a long time to run even any single application (the paper states it could take hours to days). This is primarily due to how complex modern architecture has become (think of multiprocessor and multicore systems that require the tracking of shared resources and synchronization). In order to simulate that complex architecture on some host environment, billions or trillions of instructions are required to achieve accurate simulation details.
2. **Poor Accuracy**
	1. Similarly due to the increasingly complexity of modern computers, accuracy can become a major concern. In addition to the sheer difficulty in modelling all components of a modern complex architecture (formally referred to as modelling and specification errors), there are additional accuracy limitations that are introduced in trying to optimize the performance of the simulator. These latter specific errors in accuracy are called abstraction errors. One must then understand the inherent limitation in simulating modern architecture given the negative effects on accuracy that result in trying to improve performance. 

The paper also notes several strategies that are taken to try and address these limitations (e.g. sampling benchmarks to address performance).
## Application to Course
Without going into too much detail, the paper gave a good overview at the different components of a computer that are required to run an OS in a sim. This is a good overview to what are the most important parts of a real computer's architecture, the focus of this course.  
![image](https://github.com/user-attachments/assets/6cb77a91-e922-44e4-8eb0-5a50d6465ef1)


The article also provided a great intro into how to measure the success of simulators, with the 6 metrics of success and how they are traded off for each other.

The article introduced us to the idea of the end of Moore's law and its implications. Most relevant to this course and our careers is in the importance of optimizing existing software and hardware computing to continue seeing performance growth without having the ability to benefit from increasingly more compact chips. This highlights how important it is to better understand computer architecture as a anyone working in software, as the architecture lens will provide you with valuable skills to help optimize in a post Moore's-law world.

## Further Reading
- See citations 12 & 13, these papers seem to target memory simulators
- Investigate the reality of Moore's Law end
