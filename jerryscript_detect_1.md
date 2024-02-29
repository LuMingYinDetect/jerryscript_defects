Affected Version:
jerryscript 2.4.0 bac7ee3acd0fa64b934a11c7d395c7f0b7820532

Vulnerability Description:
The vulnerability is a memory leak bug located at line 151 of the file /jerryscript/jerry-ext/util/sources.c. This vulnerability could potentially be exploited maliciously to cause resource exhaustion and denial of service attacks.

jerryscript download address:
https://github.com/jerryscript-project/jerryscript.git

Detailed Description of the Defect:

1.A pointer variable named line_p is defined on line 140 of the file sources.c in /jerryscript/jerry-ext/util. This variable is allocated a block of dynamic memory using the jerry_port_line_read function, as shown in the diagram below:

![image](https://github.com/LuMingYinDetect/jerryscript_defects/blob/main/jerryscript_1.png)

2.A variable named line_p is defined on line 66 of the jerry_port_line_read function. This variable is allocated a block of dynamic memory using the realloc function on line 73, and it is returned on line 95, as shown in the diagram below:

![image](https://github.com/LuMingYinDetect/jerryscript_defects/blob/main/jerryscript_2.png)

3.When the if condition on line 142 evaluates to false, it indicates that the memory area for line_p has been successfully allocated. However, when the if condition on line 149 evaluates to true, the program returns on line 151 without using or freeing the memory area pointed to by the variable line_p. This results in a memory leak defect, as shown in the diagram below:

![image](https://github.com/LuMingYinDetect/jerryscript_defects/blob/main/jerryscript_3.png)
