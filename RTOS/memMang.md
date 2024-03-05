this directory contains 5 files .c  you need to pick only one for your os

In RTOS there is 2 ways to manage memory :
#### 1- Statically              
#### 2- Dynamically 

if you want to use dynamic allocation you have to set  **configSupport_Dynamic_Allocation**  to 1 
_____
1. **Heap_1.c:**
    
    - **Fixed Size Allocation:** `heap_1.c` provides a simple, fixed-size allocation scheme.
    - **Allocating Task Stacks:** In `heap_1.c`, task stacks are allocated from a statically allocated array defined by the `configTOTAL_HEAP_SIZE` parameter in the FreeRTOS configuration file.
    - **Static Allocation:** Memory is allocated statically at compile time, and the size of the heap is fixed.
    - **Simple Implementation:** `heap_1.c` is a simple and efficient implementation suitable for systems with limited resources or where the heap size is known and fixed.
    - **Limited Flexibility:** It does not support freeing memory or dynamic resizing of the heap.
2. **Heap_2.c:**
    
    - **Variable Size Allocation:** `heap_2.c` provides a variable-size allocation scheme.
    - **Allocating Task Stacks:** Task stacks are allocated from the heap created by `heap_2.c`.
    - **Dynamic Allocation:** Memory is allocated dynamically at runtime using `malloc()` and `free()` functions provided by the C standard library.
    - **Dynamic Resizing:** `heap_2.c` allows for dynamic resizing of the heap at runtime, enabling flexibility in managing memory.
    - **More Overhead:** Compared to `heap_1.c`, `heap_2.c` may have slightly more overhead due to the use of standard library functions for memory allocation.
    - **Supports Freeing Memory:** It supports freeing memory, allowing tasks to release memory when no longer needed.
    - *Example* : Heap contains 3 blocks with sizes of 5 , 25, 100 bytes and 20 bytes is requested heap2.c will use the nearest free block to required block size so it will choose 25 byte block to use and will divide it to 20byte and free 5 bytes  
1. **Heap_3.c:**
    
    - **Allocating Task Stacks:** Task stacks are allocated from a statically allocated array defined by the `configTOTAL_HEAP_SIZE` parameter in the FreeRTOS configuration file.
    - **Fixed-Size Allocation:** Similar to `heap_1.c`, `heap_3.c` provides a simple fixed-size allocation scheme.
    - **Static Allocation:** Memory is allocated statically at compile time, and the size of the heap is fixed.
    - **Simple Implementation:** It is a simple and efficient implementation suitable for systems with limited resources or where the heap size is known and fixed.
    - **Limited Flexibility:** Like `heap_1.c`, it does not support freeing memory or dynamic resizing of the heap.
4. **Heap_4.c:**
    
    - **Variable Size Allocation:** `heap_4.c` provides a variable-size allocation scheme.
    - **Allocating Task Stacks:** Task stacks are allocated from the heap created by `heap_4.c`. giving ability to add address from which heap will be created at.
    setting  *APPLICATION_ALLOCATEHEAP* to 1 will give you ability to add your  custom address where heap created at 
    in GCC 
    ```c 
    uint8_t ucHeap[configTOTALHEAP_SIZE] __ attribute__((section(".my_heap"))) 
    
    // in IAR 
    uint8_t ucHeap[configTOTALHEAP_SIZE]@0xaddress
    
    ```

    - **Dynamic Allocation:** Memory is allocated dynamically at runtime using `malloc()` and `free()` functions provided by the C standard library.
    - **Dynamic Resizing:** `heap_4.c` allows for dynamic resizing of the heap at runtime, enabling flexibility in managing memory.
    - **Supports Freeing Memory:** It supports freeing memory, allowing tasks to release memory when no longer needed.
    - **Configurable Memory Regions:** `heap_4.c` allows the heap to be split into multiple memory regions, each with its own size and allocation strategy.
5. **Heap_5.c:**
    Allows defining the heap across multiple non-contiguous memory regions. This is useful if you have memory available in different parts of the address space.
    - **Configurable Memory Allocator:** `heap_5.c` is a memory allocator that provides several allocation schemes, including segregated memory pools and thread-safe memory allocators.
    - **Fine-Grained Control:** It offers more fine-grained control over memory allocation and allows customization of memory allocation behavior.
    - **Thread-Safety:** `heap_5.c` includes thread-safe memory allocation algorithms, making it suitable for use in multi-threaded applications.
    - **Advanced Features:** It may include features such as memory tagging, statistics collection, and memory protection.
    - **Complexity:** `heap_5.c` may be more complex to configure and use compared to `heap_3.c` and `heap_4.c`, requiring a deeper understanding of memory management concepts.


| Feature                  | `heap_1.c` | `heap_2.c` | `heap_3.c`           | `heap_4.c`            | `heap_5.c`            |
| ------------------------ | ---------- | ---------- | -------------------- | --------------------- | --------------------- |
| Static/Dynamic           | Static     | Static     | Static               | Dynamic               | Dynamic               |
| Task Stack Allocation    | N/A        | N/A        | Statically allocated | Dynamically allocated | Dynamically allocated |
| Fixed-Size Allocation    | Yes        | No         | Yes                  | No                    | No                    |
| Variable-Size Allocation | No         | Yes        | No                   | Yes                   | Yes                   |
| Dynamic Resizing         | No         | No         | No                   | Yes                   | Yes                   |
| Supports Freeing Memory  | No         | No         | No                   | Yes                   | Yes                   |
| Memory Regions           | N/A        | N/A        | N/A                  | Configurable          | Configurable          |
| Thread-Safety            | N/A        | N/A        | N/A                  | N/A                   | Yes                   |
| Complexity               | Simple     | Simple     | Simple               | Moderate              | Complex               |
  
**1. Task Stack Allocation:**

In FreeRTOS, each task requires a dedicated **stack** to store its local variables, function return addresses, and other information needed for execution. This stack grows downwards towards lower memory addresses (on most architectures) during function calls and unwinds upwards when functions return.

**2. Fixed-Size Allocation:**

- **Description:** The most common approach. The stack size for each task is statically defined at compile time using a constant value.
- **Example:**

```c
#define TASK1_STACK_SIZE 2048
static StackType_t task1Stack[TASK1_STACK_SIZE];

TaskHandle_t xTask1;
xTaskCreate(task1Function, "Task 1", TASK1_STACK_SIZE, NULL, 1, &xTask1);
```
- **Advantages:**
    - Simple and efficient.
    - Guarantees deterministic memory usage at compile time.
- **Disadvantages:**
    - May lead to wasted memory if tasks don't utilize the entire allocated stack.
    - Can be inflexible if stack requirements change dynamically.

**3. Variable-Size Allocation:**

- **Description:** Less common, but allows defining the stack size dynamically at runtime based on the task's needs.
- **Example:**
- 
```c
#include "stdlib.h"

void taskFunction(void *pvParameters) {
    // ... task code ...
}

TaskHandle_t xTask2;
int stackSize = 3072;
void *stack = pvPortMalloc(stackSize);
if (stack != NULL) {
    xTaskCreate(taskFunction, "Task 2", stackSize / sizeof(StackType_t), NULL, 1, &xTask2);
} else {
    // Handle memory allocation failure
}
```
- **Advantages:**
    - More efficient memory usage by allocating only the necessary amount.
- **Disadvantages:**
    - Introduces runtime overhead for memory allocation and deallocation.
    - Requires careful management to prevent memory leaks.

**4. Dynamic Resizing (Not Supported by FreeRTOS Core):**

- **Description:** Not directly supported in FreeRTOS.
- **Explanation:** Some external libraries or custom implementations might claim to dynamically resize stacks during runtime, but this is generally discouraged.
- **Reasons:**
    - Resizing stacks during execution can be complex and error-prone, potentially leading to data corruption, stack overflows, or system crashes.
    - FreeRTOS relies on well-defined stack sizes for its scheduling and context switching mechanisms.

**5. Supports Freeing Memory:**

- **Description:** FreeRTOS does not support freeing the memory allocated for a task's stack directly.
- **Reason:** Task stacks are considered part of the kernel's memory management and are not intended for user-controlled freeing. Once a task is deleted using `vTaskDelete()`, the FreeRTOS kernel automatically reclaims the associated stack memory.

**6. Memory Regions:**

- **Description:** FreeRTOS allows you to specify different memory regions for various purposes, including the heap and task stacks. This can be useful for isolating FreeRTOS data structures and achieving specific memory management strategies.
- **Configuration:** Achieved through configuration options provided by your port (hardware/compiler combination) or a separate memory management unit (MMU) if available.
- **Example:** (Configuration details may vary depending on your port)

```c
#if defined(configMEMORY_REGION)
static StaticTask_t xTask3Static;
static StackType_t xTask3Stack[TASK3_STACK_SIZE] __attribute__((at(0x20000000))); // Allocate stack in a specific memory region
TaskHandle_t xTask3 = xTaskCreateStatic(task3Function, "Task 3", TASK3_STACK_SIZE, NULL, 1, xTask3Stack, &xTask3Static);
#else
#error "configMEMORY_REGION not defined"
#endif
```
- **Remember:** Consult your port documentation for specific instructions on configuring memory regions.

By understanding these concepts, you can make informed decisions about task stack allocation strategies in your FreeRTOS applications, improving memory efficiency and reducing the risk of stack-related issues.