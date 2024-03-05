
- schedule the execution of a function at set time in the future or periodically with a fixed frequency.
- Function executed by the software timers is called the software timer call back 
- they are implemented under RTOS Kernel 
- **Require no hardware timer**

### Types of Software timer :
1- Auto reload timer                            2- One shot timer

### Timer states : 
1- Dominant                          2- running 

**Timer Call back shouldn't have while loop in task**


```c
/*
Description : Software Timers in Freertos
*/

#include "std_types.h"
#include "bit_math.h"
#include "FreeRTOS.h"
#include "task.h"
#include "timers.h"
#include "LCD_interface.h"


TimerHandle_t oneShot, autoReload ;
BaseType_t    oneShot_started,autoRelaod_started ;


void OneshotTask(TimerHandle_t t){
	HLCD_vShowString("One");
}


void AutoReloadTask(TimerHandle_t t){
	HLCD_vShowString("Auto");
}

int main(void)
{
	HLCD_vInit();
	oneShot = xTimerCreate("OneShot",
	1000/portTICK_PERIOD_MS,
	pdFALSE,
	NULL,
	OneshotTask);
	
	autoReload = xTimerCreate("AutoReload",
	500/portTICK_PERIOD_MS,
	pdTRUE,
	NULL,
	AutoReloadTask);
	
	oneShot_started = xTimerStart(oneShot,0);
	autoRelaod_started = xTimerStart(autoReload,0);

	vTaskStartScheduler();
}


```