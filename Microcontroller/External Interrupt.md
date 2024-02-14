
In AVR can be triggered by pin from INT0:INT2 note that if you enable those pins as output event will trigger.

#### Event Trigger : 
1. Low Level                         2. Raising edge                  3. Falling edge           4. Any logical change 

#### How to do it :
1. in MCUCR select Trigger mode
2. in GICR Enable correspond interrupt 
3. Enable global interrupt in your main program



#### How to write your ISR 
```c

void __vector_(vector_number) (void)  __attribute__((signal)) ; 
main()
{
.....
}
void __vector_(vector_number) (void){
.....
}
```


#### How to Call ISR :
```c

void __vector_(vector_number) (void)  __attribute__((signal)) ; 
main()
{
.....
}
void __vector_(vector_number) (void){
.....
}
```
this code has a problem that a part of EXTI Driver is implemented in Application code.
So we have to move 
``` c
void __vector_(vector_number)(void);
```
to EXTI_Driver. if we did that  we  cannot call this function from CAL layer as passed on rules we cannot call functions from higher layer. 

so we need to have work around. 

***Call-back Function***  : 
In our EXTI_prog.c we can define global pointer to function. in our ISR that is defined in our EXTI Driver instead of call fun that defined in our application we can pass address to our pointer and call function throw our pointer in ISR.

```c
// EXTI_prog.c
static void (*pointer_to_function) (void);
void __vector_(vector_number) (void){
pointer_to_function(); 
}
```

problem now is how to pass  address to this function. we can create another function that take pointer to function as argument and assign our global pointer to this function.

```c
// EXTI_prog.c
static void (*pointer_to_function) (void);
u8 EXTI_u8SetCallBack(void(*ptofunction)){
pointer_to_function = ptofunction ; 
}
void __vector_(vector_number) (void){
pointer_to_function(); 
}
```

this function that we created is call-backs. this way application can have what ever ISR routine to be performed and pass it to ISR function in EXTI_driver 

```c
void toggle_led (void);
main(){
DIO_voidInit();
GI_Enable();
EXTI_u8SetCallBack(&toggle_led); 
EXTI_u8EnableInterrupt(EXTI_u8_INT0, EXTI_RAISING_EDGE);
}
```

if we have multiple interrupt instead of global pointer to function. 
we can use array of pointers to function. 
```c
static void(*pointer_to_function)(void);--> static void (*pointer_to_function[3])(void);
```

don't forget to make guards for dangling pointer.