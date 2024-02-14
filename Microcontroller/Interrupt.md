
**IRQ** : Stands for Interrupt request 
**ISR**: Stands for Interrupt service routine


##### What is interrupt :
interrupt is hardware setup that force microcontroller to execute specific commands when an event happens.
Used by a lot of peripheral like Timer, ADC and UART where we can continue code execution and not wait Flag from our peripheral.  

so instead of pooling we use interrupt.

any peripheral that use interrupt has 2 Flags : 
**a-**  PIF (peripheral Interrupt Flag)    **b-** PIE (peripheral Interrupt Enable)   
##### Interrupt Types : 

|      | Vectored     | Non-Vectored     |
|:-----|:-----|:-----|
|      | Vector interrupts are a more sophisticated and structured form of interrupt handling. In a vector interrupt system, each interrupt source has a dedicated location in memory called an interrupt vector. When an interrupt occurs, the microcontroller uses the interrupt vector to determine the appropriate interrupt service routine (ISR) to execute     |Non-vector interrupts, sometimes called simple interrupts or level-triggered interrupts, do not have a dedicated memory location for each interrupt source. Instead, they are often handled in a more sequential manner. When an interrupt occurs, the microcontroller typically checks all the interrupt sources to determine which one caused the interrupt      |
|**Priority Handling**      | Vector interrupts often come with a built-in priority mechanism. When multiple interrupts are pending, the microcontroller can automatically execute the ISR associated with the highest-priority interrupt.     |Non-vector interrupts might not have built-in priority handling mechanisms. The microcontroller has to manually check and compare interrupt sources to determine which one to handle first.      |
|**Response Time**      |Vector interrupts generally have a faster response time because the microcontroller can directly jump to the appropriate ISR without needing to search through a list of pending interrupts.      |Due to the need to compare and determine the source of the interrupt, non-vector interrupts might have a slightly slower response time compared to vector interrupts.      |
|**Structured Handling**      |Since each interrupt has a designated location in memory, the code organization is more structured and easier to manage      |Since there is no dedicated vector for each interrupt source, the code for handling non-vector interrupts can be less structured and may require more manual handling.      |
|      |Some machines reserve part of memory for interrupt vector those location cannot be changed by programmer . programmer can only change data at each vector location. each location of interrupt vector table contain location of ISR      |      |
|      |      |      |
|      |      |      |

IVT (interrupt Vector table) Contains :
1 - IRQ number 
2 - Vector Address 
3 - IRQ address

##### How interrupt is handled :
1 - microcontroller finish recent instruction that currently executed 
2 - Start Context switching : 
address of next instruction to be executed is pushed with all processor GPRs to stack. 
This operation has fixed time known as interrupt latency 
3 - Program counter is loaded with the address pointed to by IRQ vector table and execute instruction in ISR till finish.
4 - All CPU register are restored from stack and Program counter loaded with next instruction from stack 

###### Interrupt latency Vs Interrupt response

Interrupt latency time needed by CPU to finish recent instruction and checking interrupt flag.
Interrupt response Time needed by CPU to start execute ISR code (Interrupt Latency + context switching)

##### Multiple interrupt :
1. **Interrupt Priority Mechanism:** Most modern microcontrollers use an interrupt priority mechanism. When a higher-priority interrupt occurs while a lower-priority interrupt is being executed, the following can happen:
    
    - **Priority Preemption:** The microcontroller halts the execution of the lower-priority interrupt and immediately switches to executing the higher-priority interrupt. Once the higher-priority interrupt is completed, the microcontroller resumes the execution of the lower-priority interrupt from where it was interrupted. This mechanism ensures that critical interrupts with higher priority are handled promptly.
        
    - **Nesting Depth:** Some microcontrollers support multiple levels of interrupt nesting. This means that if a lower-priority interrupt is already being executed and another interrupt with an intermediate priority occurs, the current interrupt can be paused, the intermediate-priority interrupt is executed, and then the execution returns to the lower-priority interrupt.
        
2. **Interrupt Latency:** The time it takes to switch from one interrupt to another is known as interrupt latency. This latency can vary depending on the microcontroller's architecture and interrupt handling mechanisms. Interrupt latency is critical in real-time systems, as longer latencies can affect the system's responsiveness.
    
3. **Stacking and Unstacking:** In systems that support interrupt nesting, the microcontroller might have dedicated hardware to manage the saving and restoring of the CPU context (registers, program counter, etc.) for each level of nesting. This is often done using a stack. When an interrupt occurs, the CPU pushes the current context onto the stack and loads the context for the new interrupt. Once the interrupt is handled, the CPU pops the previous context from the stack to resume execution.


#### Types of interrupt  :

1. Asynchronous / interrupt Hardware :
- Happen by External Source such as I/O devices
- Not related to instruction being executed


2. Synchronous interrupts :
- Processor detected exception    -Fault    -Traps      -Aborts
- Programmed Exception              - request from kernel 
- Software Interrupt                        caused by either exceptional condition or special instruction in ISA   Like : divide by Zero            Software interrupt works like subroutine call 
----------------------------------------------------
Fault : instruction illegal to executed     Like write to read-only segment 
Traps : CPU maybe programmed to automatically switch to debug mode after certain instruction
Error : Like divide by zero (have dedicated circuit to detect dived by zero and raise interrupt)

----------------------------------------

I/O devices have (unique or shared) interrupt request IQRs
IQRs are mapped using PIC (programmable Interrupt Controller) to interrupt vectors and passed to CPU 
PIC handles Interrupt masking/priority and send this data to the CPU

--------------------------------------
***Systick***
is a timer in ARM that generate interrupt request on regular basis. this allow OS to have multiple tasking.
