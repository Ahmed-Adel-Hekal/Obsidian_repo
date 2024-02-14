

is the way we use to convert our analog data to digital. 

any Analog sensor needs [[Transducer]] to convert change in sensor read to analog output.
Transducer output can be change in Ohm, voltage or Amp.

#### ADC Steps:
1 -**[[Sampling]]**                           2 - **[[Quantization]]**            3 - **[[Encoding]]** 

##### Sampling :
The continuous analog signal is sampled at regular intervals
##### Quantization :
The sampled analog value is quantized into a discrete digital value.
##### Encoding :
The quantized value is encoded into binary using the ADC's resolution

**ADC Characteristics**:

- **Resolution**: The number of bits used to represent the digital output. A higher resolution results in finer quantization and better accuracy.
- **Sampling Rate**: The rate at which the ADC samples the analog signal per second.
- **Input Range**: The range of analog voltage that the ADC can convert.
- **Conversion Time**: The time required to complete a single conversion.
- **Accuracy**: The ability of the ADC to accurately represent the input signal's amplitude.
- **Reference Voltage**: The voltage against which the input signal is measured.
- **Step Size** : refers to the smallest change in the analog input signal that results in a change in the digital output code


to calculate resolution equals **2^n** where n is number of bits used to present analog value.
to calculate **Step Size** 
**Step_Size** = (max_voltage - min_voltage) / resolution 

Calculation of step size for constant vref :

|n-bits|number of steps |step_size(mv) |binary code|
|:-----|:-----|:-----|:-----|
|8-bits      |256      |5/256=19.61      |      |
|10-bits      |1024      |5/1024=4.89      |      |
|12-bits      |4096      |5/4096=0.076      |      |


**Quantization Error**
Example we have sensor with Vmax  = 4 volt and resolution of 2 bits so
Step size = 4/2^2  = 1 volt.
so every change by 1 volt will result increase in quantizer by one

|input volt      |digital value      |      |      |
|:-----|:-----|:-----|:-----|
|0 -->.99 | 0      |      |      |
|1--> 1.99|1      |      |      |
|2--> 2.99 |2      |      |      |
|3-->4      | 3     |      |      |

if we try to convert digital result to analog voltage (step_size * digital value) we will found that :

|Digital value      |analog voltage      |
|:-----|:-----|
|0      |0 volt      |
|1      |1 volt       |
|2      |2 volt      |

which means that for Digital Value of 0 that originally holds values from 0 to .99 is now present 0 voltage signal.
this kind of error called Quantization error in our case equals  .99 volt.

##### How to reduce Quantization error :
by 1- increase resolution                 2- decrease Vref 

#### What if input signal exceed ref voltage :
any signal that exceed Saturation voltage it will produce one.
Saturation Voltage = Vref - one step. 



-----
# ADC Types :


1. [[Flash ADC]]
2. Digital to Analog converter based design ([[Ramp ADC]]- [[SAR ADC]])
3. Integrator based design 
4. Sigma-delta design



--------

### ADC IN AVR :
The ADC module can’t run at the full CPU clock speed, though, so it needs its own clock source. The good news is that it’s equipped with a clock prescaler (like the timers are) that can subdivide the CPU clock down to a usable speed. The bad news is that because you can change the CPU clock speed, it’s also your responsibility to figure out an appropriate prescaler for the ADC clock.

the ADC even draws power from its own separate power supply pin, AVCC!


[[LDR]]

So you’re not getting output from the ADC or it’s not changing? Here’s a quick troubleshooting checklist: 
1. Did you hook up AVCC? The ADC needs power, and it needs to be within around 0.6 V of the AVR’s VCC. 
2. Did you set a voltage reference with the REFSx bits in ADMUX? By default the AVR is looking for an external voltage reference on the AREF pin. If you’d like to use the AVCC as AREF, you have to set REFS0 in ADMUX. 
3. Did you set the ADC prescaler? The ADC needs a clock source. 
4. Did you set the ADEN bit to enable the ADC? 
5. Do you have the correct channel selected in the multiplexer? Remember that they’re referenced by binary value rather than bit value.
6. Finally, if you’re reading the ADC values out independently, make sure that you read the low byte, ADCL, before you read the high byte, ADCH. For whatever reason, the ADCH bytes aren’t updated until ADCL is read in 10-bit mode. (I just avoid this snafu by reading ADC, and letting the compiler take care of the ordering for me.) And if none of this is working, are you sure that your sensor is working? Try outputting the ADC data over the serial port and connecting the ADC pin to AREF and GND, respectively, to make sure that the problem lies in your code and not in a broken sensor. Or if you can, hook the sensor up to a voltmeter or oscilloscope. Is it behaving as you expect?
-----
#### HOW TO CONVERT ADC READING :

voltage_value_converted_by_ADC = (ADC_reading * Vref ) / 2^n   
where n is number of bits used by adc (adc resolution)
to a void using float we convert Vref from volt to millivolt 


according to datasheet you can know how much step size of your sensor(smallest change in voltage that change your sensor read)




-------------
#Note  if you are using proutos simulation please know that adc only work with external Aref what ever you choose it is always work on voltage that connected on Aref.





