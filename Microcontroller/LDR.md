The LDR gets less resistive when more light shines on it, so we’ll see a direct relationship between the light level and the voltage sent to the AVR.resistance that decreases as more and more light falls on them


we will need to use voltage divider circuit.

#### Facts to Know:
• LDRs vary a lot from one to the next in terms of their maximum resistance in the dark, so don’t expect any two to have exactly the same resistance in the same conditions. If you’ve got an ohmmeter, measure a few in the dark to see what I mean. 
• Lesser-known fact: LDRs also exhibit a temperature-dependent resistance.
• You can burn an LDR out if you run too much current through it. And because the resistance drops as the light hitting it gets brighter, the fixed resistor can’t be too small: keep it above 200 ohms at 5 V. 
• If your sensor saturates in bright light, try decreasing the fixed resistor in the voltage divider. If you need more dark sensitivity, increase the fixed resistor. 
• LDRs are slow relative to microcontrollers, but faster than the human eye: they take between tens and hundreds of milliseconds to react to changes in light. My example LDR circuit is fast enough to detect the flicker in incandescent light bulbs that results from alternating current.
• LDRs are most sensitive to light in the red-green wavelength range, so they pair up beautifully with red LEDs or lasers. Some even see into the infrared. They’re a little weaker in the blue-purple range. Their response curve is actually a lot like the human eye’s


**Voltage Divider Law**
Vout = Vin × R2 / (R1 + R2).