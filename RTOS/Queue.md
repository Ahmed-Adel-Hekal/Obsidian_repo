
* Queue is just FIFO stack that is used to synchronize data sent by other tasks.

Create Queue is simple 
```c

#define Timeout 100/portTICK_PERIOD_MS
// Create QueueHandle used to create Queue
QueueHandle_t  xQueue1 ; 

int main(){

	// Create Queue that holds pointers
	xQueue1 = xQueueCreate(QUEUE_LENGTH, sizeof(char *));
}

// Sender Task 

void SenderTask(void *ptr){
	// Note that if pointer decliration should be the same as 
	// Pointer used in reciver task otherwise it will cause 
	// Garbage Values
	const char *data = "Hello 1";
	BaseType_t state ; 
	while(1){
		state = xQueueSend(xQueue1, &data, Timeout);
		if(state == pdTrue){
		// IF Sender Succeed Do something
		}
	}
}

void ReciverTask (void *ptr){
	const char *data ; 
	BaseType_t state ;
	while(1){
		state = xQueueRecive(xQueue1, &data, Timeout)
		if(state == pdTrue){
		HLCD_vShowString(receivedMessage);
		// Do Something
		}
	}
	
}


```

-----
*QueueSet :
- **Usage**: QueueSets are used for monitoring multiple queues or other types of RTOS objects simultaneously.
    
- **Properties**: A QueueSet can monitor up to a specified number of queues or other objects.
    
- **Operations**: Tasks can wait for data from any of the monitored queues or resources using `xQueueSelectFromSet()`.
    
- **Blocking**: Tasks can block until data becomes available on any of the monitored queues or resources.

```c

// Create individual sensor queues
QueueHandle_t xQueueSensor1, xQueueSensor2;

// Create QueueSet
QueueSetHandle_t xQueueSet;

// Task prototypes
void Sensor1Task(void *pvParameters);
void Sensor2Task(void *pvParameters);
void MainControllerTask(void *pvParameters);

int main(void) {
    // Create sensor queues
    xQueueSensor1 = xQueueCreate(QUEUE_LENGTH, sizeof(Data_t));
    xQueueSensor2 = xQueueCreate(QUEUE_LENGTH, sizeof(Data_t));
    
    // Create QueueSet and add sensor queues
    xQueueSet = xQueueCreateSet(2);
    xQueueAddToSet(xQueueSensor1, xQueueSet);
    xQueueAddToSet(xQueueSensor2, xQueueSet);
    
    // Create tasks for sensor data processing
    xTaskCreate(Sensor1Task, "Sensor1Task", STACK_SIZE, NULL, 1, NULL);
    xTaskCreate(Sensor2Task, "Sensor2Task", STACK_SIZE, NULL, 1, NULL);
    
    // Create main controller task
    xTaskCreate(MainControllerTask, "MainControllerTask", STACK_SIZE, NULL, 2, NULL);
    
    // Start FreeRTOS scheduler
    vTaskStartScheduler();
    
    // Should not reach here
    return 1;
}

typedef struct {....}Data_t;
// Sensor task example
void Sensor1Task(void *pvParameters) {
    // Sensor task logic here
    while (1) {
        // Read sensor data
        Data_t sensorData;
        
        // Send data to queue
        xQueueSend(xQueueSensor1, &sensorData, portMAX_DELAY);
        
        // Other tasks processing...
    }
}

// Similar Sensor2Task implementation...

// Main controller task example
void MainControllerTask(void *pvParameters) {
	Data_t reciveddata ;
    while (1) {
        // Wait for sensor data from any sensor
        QueueSetMemberHandle_t xActivatedMember = xQueueSelectFromSet(xQueueSet, portMAX_DELAY);

		if(xActivatedMember == xQueueSensor1){
			xQueueReceive(xQueueSensor1, &reciveddata,0);
			// Do something if data come from sensor1
		}
		else if (xActivatedMember == xQueueSensor2){
			xQueueReceive(xQueueSensor1, &reciveddata,0);
				// Do something if data come from sensor1
		}

    }
}

```