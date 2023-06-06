# CSE 15L - Lab Report 5

## Part 1 - Debugging Scenario
### What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?

- HP ENVY 14x07
- Ubuntu Linux 16.02
- Java FIle

```
public class Main {
  private static int index = 0; // Shared variable

  public static void main(String[] args) {
    int[] array = {1, 2, 3, 4, 5};
    
    // Start two threads that race to increment the index
    Thread thread1 = new Thread(() -> {
      for (int i = 0; i < 1_000_000; i++) {
        incrementIndex();
      }
    });
    
    Thread thread2 = new Thread(() -> {
      for (int i = 0; i < 1_000_000; i++) {
        incrementIndex();
      }
    });
    
    thread1.start();
    thread2.start();
    
    try {
      thread1.join();
      thread2.join();
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
    
    // Access the array with the potentially incorrect index
    int element = array[index];
    System.out.println("Element at index " + index + ": " + element);
  }
  
  private static void incrementIndex() {
    // Simulate a race condition by introducing a delay
    try {
      Thread.sleep(1);
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
    
    // Increment the shared index variable
    index++;
  }
}
 ```

### Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.

I'm experiencing an race condition error while accessing an array with an index variable shared between multiple threads.
I encountered an error related to a race condition while accessing an array with an index variable shared between multiple threads. The code simulates a multi-threaded scenario where two threads race to increment the index, and then the main thread accesses the array using this index. However, the program produces unpredictable results and sometimes throws ArrayIndexOutOfBoundsException.

For example: 
```
Error: java.lang.ArrayIndexOutOfBoundsException: Index 10 out of bounds for length 5
```

But other times:

```
Error: java.lang.ArrayIndexOutOfBoundsException: Index 14 out of bounds for length 5
```

##### Symptom: When I execute the Java program, I get an "Unpredictable Index Access" error.

### Detail the failure-inducing input and context. That might mean any or all of the command you're running, a test case, command-line arguments, working directory, even the last few commands you ran. Do your best to provide as much context as you can.

I suspect the error might be occurring due to an incorrect synchronization mechanisms 

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

Hi there! It looks like you're encountering an "Unpredictable Index Access" error. To investigate further, could you please provide the output of the following command in your terminal:
```
java -version
```
### Student: 

```
java version "1.8.0_112"
```

### TA: Upon analyzing the code and the error message, it appears that the issue is caused by multiple threads trying to access and manipulate shared data concurrently, resulting in unpredictable outcomes due to the timing and interleaving of the threads. In your code, the index variable is shared between thread1 and thread2, and both threads increment it without proper synchronization. This can lead to unexpected values and index access.

In the given code snippet:
```
public class Main {
  private static int index = 0; // Shared variable
  private static final Object lock = new Object(); // Lock object for synchronization

  public static void main(String[] args) {
    int[] array = {1, 2, 3, 4, 5};

    Thread thread1 = new Thread(() -> {
      for (int i = 0; i < 1_000_000; i++) {
        incrementIndex();
      }
    });

    Thread thread2 = new Thread(() -> {
      for (int i = 0; i < 1_000_000; i++) {
        incrementIndex();
      }
    });

    thread1.start();
    thread2.start();

    try {
      thread1.join();
      thread2.join();
    } catch (InterruptedException e) {
      e.printStackTrace();
    }

    synchronized (lock) { // Synchronize the critical section
      // Access the array with the correct index
      int element = array[index];
      System.out.println("Element at index " + index + ": " + element);
    }
  }

  private static void incrementIndex() {
    synchronized (lock) { // Synchronize the critical section
      index++;
    }
  }
}
```
To correct the code and fix the race condition, you need to ensure proper synchronization when accessing the shared index variable. One way to achieve this is by using the synchronized keyword to create a synchronized block around the critical section of code where the shared variable is accessed.


### Student: Thanks for the response, TA! I tried running the code. And it works!


## Part 2 - Reflection

I gained valuable insights during this class, particularly in exploring the fascinating world of Vim. Vim's command-line editing capabilities proved invaluable, especially in server environments without graphical interfaces. Its versatility, efficiency, and cross-platform availability make it an essential tool for developers and system administrators. Using Vim not only enhanced my coding productivity but also cultivated a mindful approach to editing and attention to detail. It has become an indispensable part of my toolkit, revolutionizing my code interactions and boosting efficiency
