
- *Round robin* : When tasks has same priority and try to share microprocessor between them . 
- Freertos has no grantee time is shared equally between tasks of equal priority
- *Fixed Priority* : 
	- this scheduler doesnot change the priority of the task bein gscheduled, but also doesnot premeet task from changing it priority 

*Premeptive* :  scheduler will preemet the running task , if task that has a priority higher than the running priority , task enterss the ready state.

***NOTE*** if oy use pre-emptive without time slicing , only  one of the highest priority task will work . 

**NOTE** : `TaskYIELD()`  task tells the scheduler that it done and can do context 
switch.

___
*OS definitions*:
1- *Throughput* : Tasks Completed per unit time
2- *Turnaround Time* : Time for each task to be completed from time it started till it is completely served  including time where task where in block state
3- *Response time* : time from request to first response 
___
- [*] *Scheduler objective* :
- [ ] Maximize throughput  
- [ ] Maximize Cpu-utilization
- [ ] minimize Turnaround time
- [ ] minimize Responsiveness
- [ ] minimize scheduling Overhead
___
 *Scheduling Techniques*  :
First come First serve ( non-preemptive) / Round robin / Weighted Round robin / Shortest job first / priority based 
___
- [*] *Task State* :
- [ ] Dorminant
- [ ] Ready
- [ ] Running
- [ ] Waiting
- [ ] Suspended
___
### Reentrant Function:
A reentrant function is one that can be safely called by multiple tasks or interrupt service routines (ISRs) simultaneously without causing unexpected behavior. Reentrant functions typically do not use global or static variables, or they use them in a way that ensures thread safety.
**Example:**
```c

// Reentrant function example 
int add(int a, int b) {     return a + b; }
```

In this example, the `add` function is reentrant because it only uses local variables `a` and `b`, and it does not rely on any global or static variables.


### Non-Reentrant Function:
A non-reentrant function is one that is not safe to be called simultaneously from multiple threads or ISRs. Calling a non-reentrant function from multiple contexts can lead to unexpected behavior or data corruption due to shared state.

**Example:**

```c
// Non-reentrant function example
int counter = 0;  
int incrementCounter(int value) 
{ counter += value; 
 return counter; }
```

In this example, the `incrementCounter` function is non-reentrant because it modifies the global variable `counter` without any protection against concurrent access. If called simultaneously from multiple threads or ISRs, it can lead to data corruption.
___
### CMSIS-RTOS : 
it is wrapper layer above rtos api there is 2 version of generic api :
1- POSIX : Portable Operating System interface                 
2- CMSIS-RTOS : cortex microcontroller software interface RTOS