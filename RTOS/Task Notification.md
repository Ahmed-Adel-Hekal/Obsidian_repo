
allows task to intercommunicate directly with need to special types like Queue,semaphor, eventGroup .

Notification has 2 states :
- Pending : if task recive notification
- Not pending : if task consume the notification 

Advantages : 
- require less ram compare to Queue , semaphore and event group .

Disadvantaged :
- cannot be used to send notification to ISR (send notification from isr is allowed)
- Only one - one relation cannot work one to many relation 

Code :
```c
/*
 * main.c
 *
 * Created: 3/4/2024 5:50:31 PM
 *  Author: ahmed
 */ 

#include "std_types.h"
#include "bit_math.h"
#include "FreeRTOS.h"
#include "task.h"
#include "EXTI_INTERFACE.h"
#include "LCD_interface.h"
// #include "DIO_Private.h"

TaskHandle_t task_h ; 

void task1(void *ptr);
int main(void)
{
	HLCD_vInit();
	EXTI0_init();
	xTaskCreate(task1,NULL,80,NULL,2,&task_h);
	vTaskStartScheduler();
}

void task1(void *ptr){
	
	while(1){
		if (ulTaskNotifyTake(pdTRUE, 0) != 0 )
		{
			HLCD_vsendData('H');
		}
	}
}

void task1(void *ptr){
	
	while(1){
		if (ulTaskNotifyTake(pdTRUE, 0) != 0 )
		{
			HLCD_vsendData('H');
		}
	}
}

void __vector_1(void) __attribute__((signal)) ; 
void __vector_1(void){
	vTaskNotifyGiveFromISR(task_h, pdFALSE);
} 
```



***NOTE*** : 
In FreeRTOS, `taskYIELD_FROM_ISR()` is typically called at the end of an ISR to ensure that a context switch occurs if a higher-priority task becomes ready to run during the ISR execution. This is important for maintaining real-time responsiveness and prioritizing tasks effectively. Let's go through an example to understand why it's necessary:

Consider a scenario where you have two tasks, Task A and Task B, with Task A having a higher priority than Task B. Additionally, there's an ISR that can occur at any time and may trigger a context switch if certain conditions are met.

Here's the sequence of events in this scenario:

1. Task A is running, and Task B is in the Blocked state waiting for an event.
2. An interrupt occurs, and the ISR is executed.
3. During the ISR execution, it determines that Task B should be unblocked because the event it was waiting for has occurred. Task B becomes ready to run.
4. The ISR completes its execution and returns.
5. Without `taskYIELD_FROM_ISR()` at the end of the ISR, Task A continues to run because the context switch hasn't been triggered yet.
6. Task A continues to run until it voluntarily yields or its time slice expires, even though Task B, which has a higher priority, is now ready to run.

To ensure that Task B (the higher-priority task) gets a chance to run as soon as possible after becoming ready, `taskYIELD_FROM_ISR()` is used at the end of the ISR. This function signals to the FreeRTOS scheduler that a context switch should occur before the ISR returns. If Task B is of higher priority than the currently running task (Task A), Task B will preempt Task A immediately after the ISR completes.