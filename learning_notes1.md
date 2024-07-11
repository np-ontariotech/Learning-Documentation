# Learning Notes for Compiler Explorer
**Link title:** Compiler Explorer  
**URL:** https://godbolt.org/

## Summary of website content 
At its highest level, Compiler Explorer allows you to see the compiled code of any given source code for almost any programming language. The features offered by this program are very numerous, but some of the most important are:
#### The source code window
  -	This window is where you insert source code for the selected language to be compiled. You can write your own source code, or load from various examples.
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/44a80083-dc83-41bd-bb4f-865748210c8a)

####	The compiler window
  -	This window is where you can see the compiled code for the source code entered in the source code window. You can select between multiple different interpreters. Code in the source code window and the compiler window are highlighted by differing colours to indicate where the highlighted code is represented by compiled code. An other useful feature is the ability to choose the optimization level (or other compiler options) of the compiler, allowing you to see different representations of the source code in compiled assembly code.
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/96d9adf9-f70f-4b8b-96e8-410b6d1ae66c)

 #### The conformance window
-	Allows you to check which compilers are able to compile the specified source code. This is especially useful for seeing how interpretable a given source code is. For example, imagine you are using the newest release of C++ to code a program. If your coworkers are using earlier releases, it is possible that the code you send them fails to compile successfully in their environment.
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/a05bea7f-cb4f-47e6-9572-83b8810837af)

####	Control flow graph window
-	Displays a graphical view to how the compiled assembly code will run. This graph view uses assembly labels to separate the code for better readability, allowing the user to visually see when certain assembly labels are jumped to based on conditionals in early code.
![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/30eaec72-80d0-4d26-8582-ec46265fa68b)

## Key takeaways
Prior to this class, the internal operations of a computer were a black box and of no concern to my programming. Now, with an understanding of how the CPU works, I am able to see the direct flow from my source code to compiled assembly code which is then turned into machine code that can be executed by the CPU in the fashion we explored with the CPU visualisation simulator.  
The ability to switch between different languages in this tool gives me a much better understanding of how different languages interact with the computer. For example, if we look at python, we can see the interpreted code for the same function is compiled in a vastly different way. This is because of Python’s interpreted nature, where it is “compiled” into bytecode (in a .pyc file) which is then ran on the Python Virtual Machine.

![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/ad7e81b9-b124-40e9-abfb-b02163226866)

On a similar note, this tool allows you to further understand languages which sit at the cross roads of interpreted and compiled languages, like Java. In Java, source code needs to be compiled, unlike in python where code is ran directly. However, this compiled code is not in the same assembly code that is compiled from C++ code. Instead, it is compiled into bytecode that is ran on the Java Virtual Machine where it is interpreted and ran as machine code.

![image](https://github.com/np-ontariotech/Learning-Documentation/assets/175245621/8bab6df1-1560-476e-a4fe-24f811c13f9c)


## Personal Insights or reflections
In my current job as a data analyst, I code quite frequently in SQL, Scala, and Python. This code is often re-used by coworkers who perform similar data analysis. The Compiler Explorer’s conformance window feature has opened my eyes to just how important it is to understand the conformance limitations of the code I produce. From now on I will make it an essential first step in my programming to document all the variables that can cause conformance issues for my coworkers, such as the programming language version and the library version.




## Feedback and Reflections
