[Home](../README.md)

### Thread  
**What is a Thread?**  
A thread is a path of execution within a process. A process can contain multiple threads.  
**Why Multithreading?**  
A thread is also known as lightweight process. The idea is to achieve parallelism by dividing a process into multiple
 threads. For example, in a browser, multiple tabs can be different threads. MS Word uses multiple threads: one thread
 to format the text, another thread to process inputs, etc. More advantages of multithreading are discussed below  
**Process vs Thread**  
The primary difference is that threads within the same process run in a shared memory space, while processes run in
 separate memory spaces. Threads are not independent of one another like processes are, and as a result threads
 share with other threads their code section, data section, and OS resources (like open files and signals). But, 
 like process, a thread has its own program counter (PC), register set, and stack space.
Advantages of Thread over Process
* **Responsiveness**: If the process is divided into multiple threads, if one thread completes its execution,
    then its output can be immediately returned.
* **Faster context switch**: Context switch time between threads is lower compared to process context switch. 
    Process context switching requires more overhead from the CPU.
* **Effective utilization of multiprocessor system**: If we have multiple threads in a single process, then we 
    can schedule multiple threads on multiple processor. This will make process execution faster.
* **Resource sharing**: Resources like code, data, and files can be shared among all threads within a process.
**Note**: stack and registers can’t be shared among the threads. Each thread has its own stack and registers.

* **Communication**: Communication between multiple threads is easier, as the threads shares common address space. 
    while in process we have to follow some specific communication technique for communication between two process.

* **Enhanced throughput of the system**: If a process is divided into multiple threads, and each thread function is 
    considered as one job, then the number of jobs completed per unit of time is increased, thus increasing the 
    throughput of the system.  
    
**Types of Threads**  
There are two types of threads.
* User Level Thread
* Kernel Level Thread


### Concurrency
Concurrency in computing refers to the idea that the OS breaks down execution into units of work and execution of these
 units of work has the same outcome no matter what order they are processed.  
In a multiprocessing system, a computer with multiple cores, we not only want to maximize concurrency but we want that 
 concurrency to safe being executed no just in any order but simultaneously.
 
Read more at
* [Medium](https://medium.com/@akhandmishra/operating-system-threads-and-concurrency-aec2036b90f8)
* [GeekforGeeks](https://www.geeksforgeeks.org/thread-in-operating-system/)
* [Quora](https://www.quora.com/What-is-concurrency-in-an-OS)