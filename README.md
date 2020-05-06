# Faust - Kadenze Course Notes

​​by Michael Curtis

## ​​Session 1: Faust Overview & Language

### ​​Intro & First Faust Program

​​Don’t forget semicolon on the end of each line to terminate it

`​​import(“stfaust.lib”);`

​​  


​​Imports all the standard libraries. Collection of all the pre-made circuits in Faust.

​​  


​​Organized into environments \(pm., no., os, etc.\)

​​  


​​A primitive is a pre-defined element of the language

​​  


​​Button - is a circuit that appears as an element in the graphic user interface, 0 when not press, 1 when pressed.

​​  


​​Documentation of any pre-defined element can be done by placing your mouse over part of the code and pressing Ctrl + D

​​  


​​Here is a djembe!

`​​import("stdfaust.lib");`

`​​process = button("gate") : pm.djembe(120,0.5,0.5,1);`

​​

​​The current code, the first four inputs are function arguments. The last one is connected to the gate button through the colon operator. Colon is a sequential composition operator, connecting the inputs of the thing on the left to the thing on the right.

​​

​​Here is an alternative notation for the same result:

​​  


`​​import("stdfaust.lib");`

`​​process = 60, 0.5, 0.5, 1, button("gate") : pm.djembe;`

​​  


​​Commas are used to place circuits in parallel.

### ​​Adding a Reverb & Using ba.pulsen

​​  


​​Make sure and match the number of inputs and outputs for sequential devices. Use the split &lt;: to make one to two outputs. Example: an oscillator is “mono”, a verb that’s built into the Faust standard library is dm.freeverb\_demo. That has two inputs and needs a split &lt;: to work.

​​  


`​​// the gate, which triggers the djembe, is being multiplied by pulsen`

`​​// this triggers ba.pulsen where the first value is length of pulse`

`​​// the second value for pulsen is period as number of samples`

`​​// then we run it into a reverb : )`

`​​`  


`​​import("stdfaust.lib");`

`​​process = button("gate")*ba.pulsen(1,4410*2) : pm.djembe(60,0.5,0.5,1) <: dm.freeverb_demo;`

​​  


​​Could add a polyrhythm like this:

​​  


`​​import("stdfaust.lib");`

`​​process = button("gate")*(ba.pulsen(1,4410*2) + ba.pulsen(1,4410*1.3)) : pm.djembe(60,0.5,0.5,1) <: dm.freeverb_demo;`

​​  


### ​​Using a Sawtooth Oscillator

​​  


`​​// make gain, set gain to 0.5 so we don't blow ourselves out`

`​​// this is infix notation, making the circuits in parallel`

