
Advantages:-
>abstracting timing information 
>maintainability  / Extensibility
>Modularity
  Team Development  **Task allow for easy development**
 Easier Testing
Improved efficiency           Code reuse 
Power management            Flexible Interrupt Handle
Mixed Processing Requirement <periodic, Continuous, Event driven>
can be built with more than 20 compiler & more than 30 arch
---------------------------------------------

**Data Types in RTOS** :
Ticktype_t is based on settings 16bits/32bits
Basetype_t is based on arch either 16bit/32bits
c : Char   x: Basetype_t   s: short  l:long   u:unsigned  p:pointer 
___
**FreertosConfig.h** : 
contains applications specific defination. it should be located in a directory that related to application code not directory that contains freertos
____
***queue.c***: provides queue & semaphor services required *Required*
*timer.c* : provides software timer functions required *Required*
*event_groups.c* : needed if event group are used  *Optional*
**croutine.c** : where intended for use on very small uc, Are rarely used now *Optional*
___
### Design types : 
1 - static design : 
- describe relation between files , how layer interact with each other , which component in each layer 
2-dynamic design : 
- Describe how component interact with each other in run time
- parameters for dynamic design are *Determanizm* & *Responsivness Time*
___
### Dynamic Design Types :
1- Super loop      2- Event-driven     3-Timer triggred

**OS** : is consist of Scheduler+dispatcher which present the core of system
Kernel ![[Kerenl-in-rtos.jpg]]

___
*Real-time Operating system* : means deliver exact task at exact time . 
*RTOS TYPES* : 
1- soft Real-time                             2-Hard Real-time
tolerance is up to 10 %                     tolerance is up to 5%

Task : is Function + TCB (Task Control Unit)

*TCB* : consist information such as  
1-Task priority       2-Task State   3-Stack region   4-function to be served       
5-periodicity 

*Scehduler* : arrange Tasks based on Schedule algorithm used [[Scheduling ALgorithms]]




From freertos v9.0.0 application can be statically located , and no need for  
 [[memMang]]. directory 
----------------------------------------------------------

