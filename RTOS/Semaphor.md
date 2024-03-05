

types :-
> 1- Binary           2- Counting            3-Mutex
> 

Binary API :-
xSemaphorCreateBinary() , xSemaphorGive(),  xSemaphorTake()

Counting API :-
xSemaphorCreateCounting() , xSemaphorGive(),  xSemaphorTake()

Mutex API :-
xSemaphorCreateMutex() , xSemaphorGive(),  xSemaphorTake()

______
GateKeeper Task 
task taht has sole ownership of a resource . is allowed to access the resource directly . anyother task needing to access the resource can do so Only by using services of that task . 
By using Queue between tasks and gatekeeper task 
