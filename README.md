# Detection-Lab
By using several GNU tools like strace, gdb,netstat,lsof, and EDB

## Objective
In this lab, I will use the GNU toolchain, including strace, gdb, and other utilities, to analyze a simple network application. The application is a simple TCP server that accepts client connections, reads their messages, and responds until it receives a 'quit' message. The goal is to compile and run the program, debug it using various tools, and understand its behavior during execution.

### Introduction
On an Ubuntu virtual machine, we are experimenting with a simple network server application. The server listens for TCP connections, reads messages from clients, and returns them. Our task is to compile and run this server while ensuring debugging symbols are included, and then analyze its behavior using tools such as netstat, strace, and gdb.

### The tools I will use include:

- Netstat: To inspect active network connections.
- Strace: To trace system calls made by the server.
- GDB: For interactive debugging of the server’s execution.
- Lsof: To examine open files used by the server.
- EDB (Evan's Debugger): A graphical debugger that makes it easier to visualize and control program execution.
- These tools will help us better understand the inner workings of network applications and provide experience with debugging and analyzing software on Linux.



## Steps and Results

*1: Using netstat*

The first step is to examine the network connections with the netstat -tuln command. This shows all TCP and UDP connections that are either active or listening. We can also see the ports the server is listening on and check if the server is properly bound to a port.
Example output from netstat -tuln:

![Screenshot 2024-04-29 140428](https://github.com/user-attachments/assets/daf1ddfe-14e7-4b96-8dfe-32a662e4bee1) 

*2: Using strace*

To see the system calls made by the server, I attached strace to the process using its process ID (PID). The command strace -p <pid> allows me to track file system interactions, network connections, and other important system-level actions in real-time.
This helps us observe the interactions between the server and the operating system, such as accepting connections or reading/writing to files.

![Screenshot 2024-04-29 141034](https://github.com/user-attachments/assets/7ecabb17-96e7-415c-a3e5-f42a360c45f1)

*3: Using gdb*

I then used gdb -p <pid> to attach the GNU Debugger to the running server process. This allows us to inspect the internal state of the program, such as variable values and the call stack. The primary benefit here is the ability to step through the code, set breakpoints, and inspect the execution at any point, which is critical for debugging complex issues. By doing this, I can examine the flow of execution and troubleshoot any unexpected behaviors in the server.

![gdb 1](https://github.com/user-attachments/assets/774f7bc2-0678-40a1-9830-898b26fc050b)

![gdb3](https://github.com/user-attachments/assets/ca2c6388-efc3-4775-b825-5fa8501773c5)

*4: Using lsof*

The command sudo lsof -p <pid> displays all files opened by the server process. This includes network sockets, configuration files, and other resources. It also shows information about the access modes for these files (whether they are opened for reading, writing, or both). Example output:

![lsof -p tool](https://github.com/user-attachments/assets/e6b88fa2-6bcb-47a0-9dc1-b472ddd931b5)

*5: Using lsof -t -p <pid>*

The -t option outputs only the process IDs of the open files for the specified PID. This simplified output format is useful for scripting or when you need to process a list of PIDs. For example, I can use this output to send signals to the server or kill a specific process based on its PID.

![lsof -i -p (1)](https://github.com/user-attachments/assets/179a5aae-086c-441e-aa3e-fbb297476a49)

![lsof -i -p (2)](https://github.com/user-attachments/assets/69fade1b-1385-4fb4-badf-accd9412ee38)

*6: Using EDB (Evan's Debugger)*

Finally, I used EDB, a graphical debugger, which provided a user-friendly interface for inspecting the server's execution. EDB made it easier to step through the program, set breakpoints, and explore memory, registers, and stack traces. This tool is particularly useful for understanding complex, multi-threaded applications.

![edb pic1](https://github.com/user-attachments/assets/c75e5ff1-3946-4a86-be47-dde1d980db0e)

### Conclusion

Through this assignment, I gained valuable insights into how network applications interact with the operating system. Using tools like strace, gdb, lsof, and EDB, I was able to track system calls, debug execution, and monitor the server’s file and network activity. EDB provided a graphical interface that made it easier to understand the server’s behavior at a granular level.

Additionally, this project helped reinforce the importance of debugging tools in understanding and analyzing the behavior of software systems, especially networked applications. The skills and techniques learned in this assignment are crucial for ensuring the proper functioning of software and for identifying potential issues such as memory leaks, performance bottlenecks, or security vulnerabilities.

Finally, I learned that understanding the execution flow of an application can be further enhanced with sandboxing approaches and security tools. By utilizing these tools, we can assess and safeguard software systems from various risks in real-world environments.
