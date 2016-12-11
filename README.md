# Linux-Based-Per-process-System-Call-Vectors
1.Introduction
Linux prohibits a loadable module from changing the global system call vector/table.  Linux makes it hard to change system calls, either globally or on a per process (or process group) basis.  Having different syscalls per process is useful for various scenarios.  For example, to add tracing/printf messages for certain syscalls; to override the default behavior of a system call (e.g., to encrypt/decrypt file names); to prevent certain processes from invoking syscalls they shouldn't (e.g., a Web server typically has no business invoking mkdir(2), unless it was hijacked).
	
2.Functionalities
List of functionalities implemented are as below.
2.1. Import a new System Call Vector
A new system call vector is loaded as a module. It registers with the global system vector table the new system calls supported. Every system call vector is a functionality, like tracing, sandboxing etc. On a per process level it can be decided, that which process should use which system vector to support the new user desired functionality.
2.2. Pass Parent process vector to Child process 
It is possible to handle if the child process should use the system vector of its parent or have another system vector of its own. This is done with the help of a flag while cloning a function. This enables to have different behavior for both parent and child process.
2.3. Adding multiple System Call Vectors
 User may require multiple flavors of existing system calls or any organization may write their own implementation for existing system calls. This system calls can be further grouped based on their usage, e.g: Set of existing system calls that having added tracing functionality, set of sandboxing system calls. So, such system call groups represented by vectors can exist.     
2.4. Assign new System Call Vector to Process
We can assign an individual system vector to a particular process. The hooked process honors the modified implementation of the system calls specified by the vector.
2.5. Change Process System Vector:
System vector of a process can be replaced with a new system vector. This allows dynamic change of behavior of a process executing this system call.
