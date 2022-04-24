## Operating Systems
An OS is a set of programs that provide clean, easy-to-use abstractions of physical resources for other programs running on the system. Also manages protection, isolation and sharing of resources with user programs. And provides common services for user programs like windowing, networks...
### Protection
Operating system must protect itself from user programs, for multiple reasons:
* **Reliability:** compromising the operating system generally causes it to crash
* **Security:** limit the scope of what [[Threads|threads]] can do
* **Privacy:** limit each thread to the data it is permitted to access
* **Fairness:** each thread should be limited to its appropriate share of system resources (CPU time, memory, I/O, etc).

## Dual Mode Operation
Hardware provides at least two modes:
1. **Kernel Mode** (superuser mode)
2. **User Mode**
Certain operations are prohibited when running in user mode, like changing the page table pointer or disabling interrupts, interacting directly with the hardware, writing to kernel memory.... And there are controlled transitions between user mode and kernel mode like system calls, interrupts, exceptions...

### Switching Modes
Switching from user mode to system mode happens on multiple events like:
* **Syscall:** Process requests a system service, like a function call but outside the process
* **Interrupt:** External asynchronous event triggers context switch like a timer or I/O device
* **Trap or Exception:** Internal synchronous event in process triggers context switch.

### Virtual Machines
Provides addition layers of protection through virtual machines or containers which run complete operating system in a virtual machine, and packages all the libraries associated with an app into a container for execution.

## Syscalls
A way in which a computer program requests a service from the kernel of the operating system on which it is executed.

### OS Library
User programs usually have OS libraries that have linked to them, which allow them to contact the operating system using Library call. The standard is lib-C.

POSIX relates to glibc in that POSIX defines the standard API which is going to be called by glibc to implement the C convention.

