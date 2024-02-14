
#### LCD Types:
1- character LCD        2- Graphical LCD        3- colored Graphical LCD

#### How it work :

2 polarizer are used to control light direction and contrast 
if the 2 polarizers are parallel light will fully pass 
if the 2 polarizers are perpendicular no light will pass 
other wise depend on the angle of second polarizer with first polarizer the contrast will change 

we control the angle of second polarizer by apply voltage to Liquid crystal material that holds the second polarizer.

#### LCD Hardware:
LCD is divided into 3 groups :
a) Power Pins : 
                     1- Vss pin ---> GND               2- Vdd ---> 5V                    3- V0 ---> Contrast Control
b) Control Pins : 
					1- RS (Regiter Selection) : 0 --> Use Command to LCD
															  1 --> Use Data to LCD
					2- RW (Read/Write Reg) : 0 --> Write data to LCD
															  1 --> Read Data from LCD
					3- Enable Pin                   : Signal to be send to LCD to Process Data 
c ) Data Pins :
					8 pins to send data in 8-bit mode. you can select either 4-bit or 8-bit mode.



#### Types of RAM in LCD :

**1 - DDRAM** :
The Display Data RAM (DDRAM) is a RAM that stores the ASCII code for the characters that we send to the LCD module. The DDRAM can store up to 80 characters (it has a capacity of 80×8 bits). However, only some of these 80 characters are displayed on the LCD. For example, in the case of a 16×2 LCD, only 32 of these memory locations are displayed.
![[ddram.webp]]

you can write data to all 80 character but you will need to shift LCD. 
To go to a particular address of the DDRAM, we can write the desired address to the Address Counter (AC). Moreover, the AC determines the position on the LCD that a character entered by a write operation goes to.
to write Data to LCD in first line you need to send command (0x80+position_needed).
to write Data to LCD in second line you need to send command (0xC0+position_needed). 

**2 - CGRAM** :
The character generated ram this is area where you can create your Custom characters. you have 64 bytes with width of 5 bits. 
So you only have 8 Characters to generate. you send data 8-bits by 8-bits .
you need to send command (0X40+(location * 8)) then start to send your character as Data.
your Special character can be used by send command to print character and pass your character location. LCD_u8SendCharacter(0).
  ![[CGRAM.PNG]]
**3 - CGROM** :
**CGROM** stands for Character Generator [ROM](https://www.crystalfontz.com/blog/glossary/rom/).
The CGROM stores the font that is displayed on a character [LCD](https://www.crystalfontz.com/blog/glossary/lcd/). When you tell a character LCD to display the letter ‘A’, it needs to know which dots to turn on so that we see an ‘A’. This information is stored in the CGROM.

By definition, (since it is a ROM) the font that is stored in the CGROM cannot be changed. Be sure to check the datasheet of the character LCD module to make sure that it can display the characters you need.


#### Commands That needed : 
![[Pasted image 20230820070052.png]]

Please refer to this ![[LCD.pdf]]

# IMPORTANT NOTES :
1- Before Sending Command or Character Please check ***Busy flag***
2- Write data or command to port before change RS , RW and send Enable Signal 

```c
void LCD_voidSendChar(u8 copy_u8Char){

    // /*Check if LCD is busy*/
    LCD_u8CheckFlag();
    /*Send Command*/
    DIO_u8SetPortValue(LCD_DATA_PORT, copy_u8Char);
    /*RS = 1*/
    DIO_u8SetPinValue(LCD_CONTROL_PORT, LCD_RS_PIN, DIO_HIGH);
    /*RW = 0*/
    DIO_u8SetPinValue(LCD_CONTROL_PORT, LCD_RW_PIN, DIO_LOW);
    /*Enable pin = 1*/
    DIO_u8SetPinValue(LCD_CONTROL_PORT, LCD_ENABLE_PIN, DIO_HIGH);
    /*delay*/
    _delay_us(1);
    /*Enable pin = 0*/
    DIO_u8SetPinValue(LCD_CONTROL_PORT, LCD_ENABLE_PIN, DIO_LOW);
}
```

```c
u8 LCD_u8CheckFlag(void){

    u8 port = 0 ;
    /*Set Data Port to Input*/
    DIO_u8SetPortDirection(LCD_DATA_PORT, DIO_INPUT);
    /*Set R/W to HIGH*/
    DIO_u8SetPinValue(LCD_CONTROL_PORT,LCD_RW_PIN, DIO_HIGH);
    /*Set RS to LOW*/
    DIO_u8SetPinValue(LCD_CONTROL_PORT,LCD_RS_PIN, DIO_LOW);
    /*Get Flag in port value*/
    while (PINC == 0x80)
    {asm volatile ("nop");
    asm volatile ("nop");}
    DIO_u8SetPortDirection(LCD_DATA_PORT, DIO_OUTPUT);
}
```