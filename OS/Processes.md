## Processes
A process is an execution environment with restricted rights, it essentially consists of:
* **Address Space**
*  **[[OS Threades]] Of Control** executing in that address space
* **System State** associated with open files, open sockets...

A process is always created by another process, and the the first process is always called by the kernel.

### Trade-offs
There is a fundamental trade-off between protection and efficiency, communication is easier within a process but harder between processes.

### Multi-threaded Processes Advantages   
* **[[Concurrency And Parallalism#Parallelism|Parallelism:]]** take advantage of actual hardware parallelism(multi-core processor) 
* **[[Concurrency And Parallalism|Concurrency:]]** ease of handling I/O and other simultaneous events.

## Process APIs
### Exit
Exits the process essentially ending it, and returns an exit code to the parent process (the process that created it), where only _0_ is a successful code. 
```c
int main(){
//...
exit(0);
}
```

### Fork
Copy the whole current process to a new address space, resulting into two identical processes running in the same time. The new process has only one thread.
Return value from fork is:
* **> 0:** then the process it the parent process and return value is pid of the new child. 
*  **=0:** then the process is running in the new child. 
* **<0:** then there is an error and the process is running in the parent process.  

```c
int main(){
pid_t cpid;
cpid = fork();
}
```

### Wait 
A function that waits for the child process to end, takes a pointer to an integer that gets filled for a return code of the child process id.
```c
int status;
pid_t tcpid;

cpid = fork();
if(cpid>0){
tcpid = wait(&status);
}
```

