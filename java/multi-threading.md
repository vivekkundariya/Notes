# Multi Threading in Java

## OS Fundamentals

### Program vs Process vs Thread

**Program:** A program is a set of instructions and associated data that resides on the disk and is loaded by the OS to perform some task. An executable file or a python script file are examples of programs. In order to run a program, the OS's kernel is first asked to create a new process, which is an environment in which a program executes.

**Process:** A process is a program in execution. A process is an execution environment that consists of instructions, user-data, and system-data segments, as well as lots of other resources such as CPU, memory, address-space, disk and network I/O acquired at runtime. A program can have several copies of it running at the same time but a process necessarily belongs to only one program.

**Thread:** Thread is the smallest unit of execution in a process. A thread simply executes instructions serially. A process can have multiple threads running as part of it. Usually, there would be some state associated with the process that is shared among all the threads and in turn each thread would have some state private to itself. The globally shared state amongst the threads of a process is visible and accessible to all the threads, and special attention needs to be paid when any thread tries to read or write to this global shared state. There are several constructs offered by various programming languages to guard and discipline the access to this global state, which we will go into further detail in upcoming lessons.


| **Aspect**      | **Program**                                     | **Process**                                            | **Thread**                                           |
|-----------------|-------------------------------------------------|--------------------------------------------------------|------------------------------------------------------|
| **Definition**  | Passive entity, a set of instructions on disk   | Active instance of a program, with its own memory      | Smallest unit of execution within a process          |
| **State**       | Static                                          | Dynamic                                                | Dynamic                                              |
| **Components**  | Code                                            | PC, process stack, data section, heap, registers       | Thread ID, PC, register set, stack                   |
| **Memory**      | Stored on disk or in source code                | Has its own memory space                               | Shares memory space with other threads in the process|
| **Isolation**   | Not executing                                   | Isolated from other processes                          | Not isolated from other threads in the same process  |
| **Overhead**    | No execution overhead                           | Higher overhead due to resource management             | Lower overhead, shares resources with threads        |
| **Concurrency** | Not applicable                                  | Can run concurrently with other processes              | Can run concurrently with other threads in the process|
| **Communication**| Not applicable                                 | Inter-process communication mechanisms (e.g., pipes)   | Direct communication via shared memory               |
| **Use Cases**   | Static code ready for execution                 | Independent tasks/applications running on an OS        | Parallel execution in multi-threaded applications    |

#### Use Cases
| **Use Case**                 | **Program**                                    | **Process**                                          | **Thread**                                          |
|------------------------------|------------------------------------------------|------------------------------------------------------|-----------------------------------------------------|
| Development Phase            | Writing and storing code                       | Running different applications (e.g., browser, editor)| Handling user interactions, background computations|
| Static Code                  | Source code, executables                       | Running independent tasks                            | Managing multiple connections in server applications|
| Execution                    | Not executing                                  | Independent applications or tasks                    | Parallel execution within a single application      |


#### Note:- 
- A program or a process are often used interchangeably but most of the times the intent is to refer to a process.
- concept of "multiprocessing" systems, where multiple processes get scheduled on more than one CPU. Usually, this requires hardware support where a single system comes with multiple cores or the execution takes place in a cluster of machines. Processes don't share any resources amongst themselves whereas threads of a process can share the resources allocated to that particular process, including memory address space. However, languages do provide facilities to enable inter-process communication.

---

### Multithreading vs. Multitasking

#### Multithreading:
Multithreading is the ability of a CPU (or a single core in a multi-core processor) to execute multiple threads concurrently, where each thread is a small unit of a process. Threads within the same process share the same data and resources but execute independently.

**Key Characteristics**:
- **Concurrent Execution**: Multiple threads can run simultaneously within the same application.
- **Shared Memory Space**: Threads share the same memory space and resources of their parent process, which allows for efficient data sharing.
- **Lightweight**: Creating and managing threads is typically less resource-intensive than processes because they share the same memory and resources.
- **Inter-thread Communication**: Easier and faster due to the shared memory space, but requires careful synchronization to avoid issues like race conditions.

**Advantages**:
- **Improved Performance**: Can significantly boost performance in multi-core systems by utilizing multiple cores effectively.
- **Responsive Applications**: Helps in keeping applications responsive (e.g., GUI applications) by offloading long-running tasks to background threads.
- **Efficient Resource Usage**: Threads are more efficient in resource usage compared to processes since they share the same memory space.

**Challenges**:
- **Synchronization**: Requires careful handling of shared resources to avoid concurrency issues such as race conditions and deadlocks.
- **Complex Debugging**: Multithreaded programs can be more difficult to debug and test due to potential timing issues and non-deterministic behavior.

**Use Cases**:
- **GUI Applications**: To keep the user interface responsive while performing background tasks.
- **Real-time Systems**: Where tasks need to be performed simultaneously without interfering with each other.
- **Web Servers**: Handling multiple client requests concurrently.


#### Multitasking:
Multitasking is the ability of an operating system to execute multiple programs (processes) simultaneously. It involves switching between different tasks so quickly that it gives the appearance of parallel execution.

**Key Characteristics**:
- **Process-based**: Multitasking deals with processes, each having its own memory space and resources.
- **Context Switching**: The OS switches between processes, saving and restoring their state, which allows multiple programs to share a single CPU.
- **Isolation**: Each process runs in its own isolated memory space, providing better stability and security.

**Advantages**:
- **Isolation and Stability**: Crashes in one process do not affect other processes due to their isolated memory spaces.
- **Security**: Processes are isolated, making it easier to enforce security policies and prevent unauthorized access to memory and resources.
- **Resource Allocation**: The OS can allocate resources dynamically among processes based on priority and need.

**Challenges**:
- **Overhead**: Context switching between processes is more resource-intensive than switching between threads.
- **Resource Usage**: Processes do not share memory space, which can lead to higher memory and resource usage.
- **Inter-process Communication (IPC)**: Communication between processes is more complex and slower compared to threads, often requiring mechanisms like pipes, sockets, or shared memory.

**Use Cases**:
- **Operating Systems**: Running multiple applications simultaneously (e.g., text editor, web browser, and email client).
- **Servers**: Running multiple services (e.g., web server, database server) on the same machine.
- **Background Processes**: Running system-level tasks such as backups, updates, and monitoring services.

---

#### Comparison Table

| **Aspect**                    | **Multithreading**                                                   | **Multitasking**                                                     |
|-------------------------------|----------------------------------------------------------------------|----------------------------------------------------------------------|
| **Definition**                | Multiple threads within a single process                             | Multiple processes running concurrently                              |
| **Memory Space**              | Shared among threads in the same process                             | Separate memory space for each process                               |
| **Resource Sharing**          | Threads share resources like memory and files                        | Processes do not share memory, may share other resources like files  |
| **Creation Overhead**         | Lower, as threads are lightweight                                    | Higher, as each process has its own memory space                     |
| **Context Switching**         | Faster and less resource-intensive                                   | Slower and more resource-intensive                                   |
| **Communication**             | Easier through shared memory                                         | More complex, using IPC mechanisms                                   |
| **Isolation**                 | Less isolated, potential for data corruption if not synchronized     | Highly isolated, reducing risk of data corruption                    |
| **Concurrency**               | Multiple threads can run in parallel on multiple cores               | Multiple processes can run in parallel on multiple cores             |
| **Use Cases**                 | GUI applications, real-time systems, web servers                     | Operating systems, server environments, background processing        |
| **Challenges**                | Synchronization issues, complex debugging                            | Higher overhead, complex IPC                                         |
| **Advantages**                | Improved performance, responsiveness, efficient resource usage       | Stability, security, dynamic resource allocation                     |

---

### Concurrency vs Parallelism
Concurrency and Parallelism are often confused to refer to the ability of a system to run multiple distinct programs at the same time.

#### Concurrency
A system capable of running several distinct programs or more than one independent unit of the same program in overlapping time intervals is called a concurrent system.
A concurrent system can have two programs in progress at the same time where progress doesn't imply execution. One program can be suspended while the other executes. Both programs are able to make progress as their execution is interleaved. In concurrent systems, the goal is to maximize throughput and minimize latency. 
Concurrent systems achieve lower latency and higher throughput when programs running on the system require frequent network or disk I/O.
The classic example of a concurrent system is that of an OS running on a single core machine. Such an OS is concurrent but not parallel. It can only process one task at any given point in time but all the tasks being managed by the OS appear to make progress because the OS is designed for concurrency. Each task gets a slice of the CPU time to execute and move forward.

#### Parallelism
A parallel system is one which necessarily has the ability to execute multiple programs at the same time.
Usually, this capability is aided by hardware in the form of multicore processors on individual machines or as computing clusters where several machines are hooked up to solve independent pieces of a problem simultaneously.
In parallel systems the emphasis is on increasing throughput and optimizing usage of hardware resources. The goal is to extract out as much computation speedup as possible.
Example problems include matrix multiplication, 3D rendering, data analysis, and particle simulation.

#### Note
- Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.
- Concurrency is a property of a program or a system whereas parallelism is a runtime behaviour of executing multiple tasks.

---

### Cooperative Multitasking vs Preemptive Multitasking
A system can achieve concurrency by employing either Cooperative or Preemptive multitasking model

#### Cooperative Multitasking model
Cooperative Multitasking involves well-behaved programs to voluntarily give up control back to the scheduler so that another program can run. The program running is in control. A malicious program can bring the entire system to a halt by busy waiting or running an infinite loop and not giving up control.

#### Preemptive Multitasking Model
In preemptive multitasking, the OS preempts a program to allow another waiting task to run on the CPU. The OS’s scheduler decides which thread or program gets to use the CPU next and for how much time. 
A thread or program once taken off of the CPU by the scheduler, can't determine when it will get on the CPU next. As a consequence, if a malicious program initiates an infinite loop, it only hurts itself without affecting other programs or threads


Early versions of both Windows and Mac OS used cooperative multitasking. Later on preemptive multitasking was introduced in Windows NT 3.1 and in Mac OS X. However, preemptive multitasking has always been a core feature of Unix based systems.

---

### Synchronous vs Asynchronous
**Synchronous:** Synchronous execution refers to line-by-line execution of code. If a function is invoked, the program execution waits until the function call is completed. Synchronous execution blocks at each method call before proceeding to the next line of code.

**Asynchronous:**

Wikipedia definition: `Asynchronous programming is a means of parallel programming in which a unit of work runs separately from the main application thread and notifies the calling thread of its completion, failure or progress.`

An asynchronous program doesn’t wait for a task to complete and can move on to the next task.
Async execution can invoke a method and move onto the next line of code without waiting for the invoked function to complete or receive its result. Usually, such methods return an entity sometimes called a future or promise that is a representation of an in-progress computation, can query for the status of the computation via the returned future or promise and retrieve the result once completed. Another pattern is to pass a callback function to the asynchronous function call which is invoked with the results when the asynchronous function is done processing.

---

### I/O Bound vs CPU Bound

Programs utilize various resources of the computer systems on which they run. For instance a program running on your machine will broadly require:
- CPU Time
- Memory
- Networking Resources
- Disk Storage
Depending on what a program does, it can require heavier use of one or more resources.

**CPU Bound:**
Programs which are compute-intensive i.e. program execution requires very high utilization of the CPU (close to 100%) are called CPU bound programs. Such programs primarily depend on improving CPU speed to decrease program completion time.

**I/O Bound:**
I/O bound programs are the opposite of CPU bound programs. Such programs spend most of their time waiting for input or output operations to complete while the CPU sits idle. I/O operations can consist of operations that write or read from main memory or network interfaces. 

#### Note
Both types of programs can benefit from concurrent architectures. If a program is CPU bound we can increase the number of processors and structure our program to spawn multiple threads that individually run on a dedicated or shared CPU. For I/O bound programs, it makes sense to have a thread give up CPU control if it is waiting for an I/O operation to complete so that another thread can get scheduled on the CPU and utilize CPU cycles. Different programming languages come with varying support for multithreading.

---

### Throughput vs Latency
**Throughput** is defined as the rate of doing work or how much work gets done per unit of time.
**Latency** is defined as the time required to complete a task or produce a result. Latency is also referred to as response time. 
 
---

### Race Condition and Critical Section
**Critical section** is any piece of code that has the possibility of being executed concurrently by more than one thread of the application and exposes any shared data or resources used by the application for access.

**Race conditions** happen when threads run through critical sections without thread synchronization. The threads "race" through the critical section to write or read shared resources and depending on the order in which threads finish the "race", the program output changes. 