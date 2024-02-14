

Instruction cycle can be de composed into a sequence of elementry micro-operations.
![[instruction_cycle.png]]
The _Indirect Cycle_ is always followed by the _Execute Cycle_. The _Interrupt Cycle_ is always followed by the _Fetch Cycle_. For both fetch and execute cycles, the next cycle depends on the state of the system.
![[instruction_cycle_flow_chart.png]]


At the end of the each cycles, the ICC is set appropriately

##### **The Fetch Cycle –**
![[fetch0.png]]
****
![[fetch1.png]]     
***
![[fetch2.png]]
***
![[fetch3.png]]
***
![[fetch4.png]]


## The decode Cycle
during the decode stage, the CPU may determine that an instruction requires data from memory. When this happens, the CPU enters an indirect cycle to fetch the required data from memory.

## The Execute cycle 




-----
[[[Computer Organization | Different Instruction Cycles - GeeksforGeeks](https://www.geeksforgeeks.org/different-instruction-cycles/)]]
