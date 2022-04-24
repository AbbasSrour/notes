## Threads
Thread is a single unique execution context, with its own program counter, registers, execution flags, stacks, memory state...
A thread executes on a processor (core) when it's resident  in the processor registers.

### Resident
It means that the register holds the root state of the thread including program counter register, currently executing instructions, intermediate values for ongoing computations, and the Stack pointer which holds the address of the top of stack in a memory.

### Suspended Thread 
A thread is suspended when its state is not loaded into the processor registers, i.e. the processor state is pointing at some other thread or the program counter register is not pointing at the next instruction from this thread. 

### Thread Control Block 
Holds contents of registers when thread not running, and is stored in the kernel.

### States
A thread all times can be in one of these states:
* **Running:** being executed by the CPU
* **Ready:** eligible to run, but not currently running
* **Blocked:** ineligible to run

### I/O Block
If a thread is waiting for an I/O to finish, the OS marks it as blocked, once the I/O finally finishes, the OS marks it as Ready.

### Thread State
1. State shared by all threads in process/address space:
	* Content of memory (global variables, heap)
	* I/O State (file descriptors, network connections...)
2. State private to each thread
	* Data kept in *TCB*
	* CPU registers 
	* Execution Stack: Parameters, temporary variables, return PCs are kept while calling procedures are executing.

## Pthreads Library
The pthread library is the posix library that provide syscalls for  the programmer to create and handle threads in an application. 

### Pthread Create
Creates a new thread executing `start_routine` with `arg` as its sole argument, and returns an implicit call to pthread_exit.

```c
int pthread_create(pthread_t *thread, const pthread_attr_t *attr, void *(*start_routine)(void*), void *arg);

```

### Pthread Exit
Terminates the thread makes `value_ptr` available any successful join 

```C
void pthread_exit(void *value_ptr);
```

### Pthread Join
Suspends the execution of the calling thread until the target thread terminates, it returns a non-Null `value_ptr` which is passed to **pthread_exit()** by the terminating thread and is made available in the location referenced by the `value_ptr`.

```c
int pthread_join(pthread_t thread, void **value_ptr);
```

### Pthread Mutex
Locking infrastructure that allows different threads in the process to lock acquire and release locks.
```c
int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutexattr_t *attr);
```

### Pthread Mutex Lock
Allows a thread to acquire the lock and prevent other threads from accessing the shared state
```c
int pthread_mutex_lock(pthread_mutex_t *mutex);
```

### Pthread Mutex Unlock
Allows a thread to release the lock 
```c
int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

## Fork-Join Pattern 
Main thread creates _forks_ collection of sub-threads passing them args to work on and then joins with them collecting the results.

## Correctness with Concurrent Threads
* **Node-determinism:**
	* Scheduler can run threads in any order
	* Scheduler can switch threads at any time
	* This can make testing very hard
* **Independent Threads:**
	* No state shared between threads
	* Deterministic and reproducible conditions
* **Cooperating Threads:**
	* Shared state between multiple threads

### Synchronization: 
Coordination among threads, usually regarding shared data

### Mutual Exclusion
Ensuring only one thread does a particular thing at a time 

### Critical Section
Code exactly one thread can execute at once

### Lock 
An object one thread can hold at a time
* **Lock.aquire():** wait until lock is free then mark it as busy
* **Lock.release():** mark the lock as free, no longer holding the lock


##  Semaphores 
Semaphores are kind of a generalized lock, first defined by Dijkstra in late 60s and is the main synchronization primitive used in original UNIX (&Pintos).
Semaphore has a non-negative value and support two operations:
* `P()` or `down()` : atomic operation that waits for semaphore to become positive, then decrements it by 1
* `V()` or `up()` : an atomic operation that increments the semaphore by 1, waking up a waiting P, if any.