1-Aspects of our microcontroller. (20min)  
• What is AT, MEGA, 32.
• Main aspects of atmega32 (Read datasheet).
• How many pins we have.  (40 pin ---> 32 functional , rest need to be explained).

2-Digital input output. (30min)  
• What is digital signal mean (digital vs Analog).    
• DDRX, PORTX, and PINX as hardware circuit.  
• Address of DDRX, PORTX, and PINX from datasheet
• Led on and off in both memory & port mapped 
(in 20, 0x16 ----> copy content in memory address 0x16 to reg 20 )
• Make first code using AVR library
• Explain need of super loop
• Check AVR Kit
• make same code without AVR (using memory address / port address )
• Explain led 
[[led.PNG]]
[[led2.PNG]]
• Led forward & reverse connection
• pull up & pull down resistor 
• activate internal pull up
• Push button and led

• Task1: Connect push button and led.  
• Make the led high when the push button is pressed.  
• The project will be at first on proteus and then will burn  
the code on the kit


• Task2: Two push button and one led.  
• When the first push button is pressed the led will be ON.  
• When the second push button is pressed the led will be  
OFF

--------
• How the seven-segment work.  
• Wire connection with out decoder.  
• How we can implement it without decoder (main idea).  
• How the decoder helps to reduce numbers of pins used in  
seven-segment  
• How we can implement it with decoder (main idea).

-----
• Task1: implement the seven-segment function that’s take  
number between zero and nine present it on the sevensegment.

• The program is to count from zero to nine with delay 1  
second  
• Task2: implement the seven-segment function but the  
decoder concept that’s take number between zero to nine  
and present on the seven-segment.  
• The program is to count from zero to nine with delay 1  
second  
• Task3: connect 2 push button and the segment one for  
increasing the number on the seven segment and the  
other for decreasing the number.
•
•
