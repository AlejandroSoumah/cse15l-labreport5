# CSE 15L - Lab Report 5

## Part 1 - Debugging Scenario
### What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?

- HP ENVY 14x07
- Ubuntu Linux 16.02
- Java FIle

```
public class Main {
 public static void main(String[] args)
 { 
 int[] array = {1, 2, 3, 4, 5};
  int index = 5; // Invalid index causing the error
  int element = array[index]; 
  System.out.println("Element at index " + index + ": " + element); } 
  }
 ```

### Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.

I'm experiencing an issue while running my Java program. I've attached a description of the symptom and a guess at the possible bug. I'd appreciate any help in resolving this.

##### Symptom: When I execute the Java program, I get an "IndexOutOfBoundsException" error.

### Detail the failure-inducing input and context. That might mean any or all of the command you're running, a test case, command-line arguments, working directory, even the last few commands you ran. Do your best to provide as much context as you can.

I suspect the error might be occurring due to an incorrect array index assignment in my code.

- Directory: /home/user/project/
- Java file: /home/user/project/Main.java
- Bash script: /home/user/project/run.sh

I'm running the following command:

./run.sh

This command executes the following bash file:

```
#!/bin/bash 
javac Main.java 
java Main
```
### TA: 

Hi there! It looks like you're encountering an "IndexOutOfBoundsException" error. To investigate further, could you please provide the output of the following command in your terminal:
```
java -version
```
### Student: 

```
java version "1.8.0_112"
```

### TA: Upon analyzing the code and the error message, it appears that the issue is caused by attempting to access an element of  array using an invalid index. To fix the bug, you need to ensure that the index is within the valid range of the array.

In the given code snippet:
```
int[] array = {1, 2, 3, 4, 5};
int index = 5; // Invalid index causing the error

int element = array[index];
System.out.println("Element at index " + index + ": " + element);
```
The index the variable is assigned a value of 5, which exceeds the valid index range for the array (which has indices from 0 to 4). To fix this, you need to adjust the value of index to a valid index within the bounds of the array.


### Student: Thanks for the response, TA! I tried running the code. And it works!


## Part 2 - Reflection

I gained valuable insights during this class, particularly in exploring the fascinating world of Vim. Vim's command-line editing capabilities proved invaluable, especially in server environments without graphical interfaces. Its versatility, efficiency, and cross-platform availability make it an essential tool for developers and system administrators. Using Vim not only enhanced my coding productivity but also cultivated a mindful approach to editing and attention to detail. It has become an indispensable part of my toolkit, revolutionizing my code interactions and boosting efficiency
