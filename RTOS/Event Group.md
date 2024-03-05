Event groups in FreeRTOS are a synchronization primitive that allows tasks to synchronize based on the state of multiple event flags. Each event group has a set of flags, and tasks can wait for specific combinations of flags to be set or cleared before proceeding. Event groups are useful for coordinating tasks based on various conditions or events in the system.

Here's a detailed explanation of event groups with example code:

### Event Group Creation

First, you need to create an event group using the `xEventGroupCreate()` function:


```c
EventGroupHandle_t xEventGroup;
xEventGroup = xEventGroupCreate();
```
### Setting Event Bits
You can set individual bits within the event group using the `xEventGroupSetBits()` function. For example:
```c
// Set bit 0 and bit 2 
xEventGroupSetBits(xEventGroup, BIT(0) | BIT(2));
```
### Clearing Event Bits
Similarly, you can clear individual bits within the event group using the `xEventGroupClearBits()` function. For example:
```c
// Clear bit 1
xEventGroupClearBits(xEventGroup, BIT(1));
```
### Waiting for Event Bits
Tasks can wait for specific combinations of event bits to be set or cleared using the `xEventGroupWaitBits()` function. This function suspends the task until the specified bits match the desired pattern. For example:
```c
`EventBits_t uxBits; 
const EventBits_t xBitsToWaitFor = BIT(0) | BIT(1);
// Wait until both bit 0 and bit 1 are set 
uxBits = xEventGroupWaitBits(xEventGroup, xBitsToWaitFor, pdTRUE, pdFALSE, portMAX_DELAY);
```
### Complete Example
Here's a complete example demonstrating the usage of event groups:

```c
#include "FreeRTOS.h"
#include "task.h" 
#include "event_groups.h"  
#define BIT_0 (1 << 0)
#define BIT_1 (1 << 1)
#define BIT_2 (1 << 2) 
EventGroupHandle_t xEventGroup;
void Task1(void *pvParameters) 
{    
// Wait until bit 0 and bit 1 are set
EventBits_t uxBits;
const EventBits_t xBitsToWaitFor = BIT_0 | BIT_1;
uxBits = xEventGroupWaitBits(xEventGroup, xBitsToWaitFor, pdTRUE, pdFALSE, portMAX_DELAY);
// Both bits are set, continue task execution 
} 
void Task2(void *pvParameters)
{    
// Set bit 0 and bit 1 after a delay
vTaskDelay(pdMS_TO_TICKS(1000)); 
xEventGroupSetBits(xEventGroup, BIT_0 | BIT_1); 
}  

int main(void) { 
// Create the event group
xEventGroup = xEventGroupCreate();
// Create Task1 and Task2 
xTaskCreate(Task1, "Task1", configMINIMAL_STACK_SIZE, NULL, tskIDLE_PRIORITY + 1, NULL);
xTaskCreate(Task2, "Task2", configMINIMAL_STACK_SIZE, NULL, tskIDLE_PRIORITY + 2, NULL); 
// Start the FreeRTOS scheduler
vTaskStartScheduler();     
return 0;
}

```

In this example:

- `Task1` waits until both bit 0 and bit 1 are set in the event group.
- `Task2` sets bit 0 and bit 1 after a delay of 1000 milliseconds.

Feel free to modify this example according to your requirements. Event groups are versatile and can be used in various scenarios to synchronize tasks based on specific conditions or events.