---
layout: essay
type: essay
title: "Structuring better code"
# All dates must be YYYY-MM-DD format!
date: 2023-04-26
published: true
labels:
  - Design Patterns
  - Software Engineering
---

I'm not a very good programmer.

This is to be expected, after all. I am, after all, relatively new to programming, much less true team-based software development. What would I possibly know and speak about authoritatively?

Therefore, in full understanding of my lack of competency as a programmer, I *can* speak authoritatively on programming poorly, in the hopes that my amateurish code can serve as a lesson in planning code properly.

## The setup

I will be describing the code I used for a summer project I made, showing the code I wrote for a scrolling sensor display. This project would poll the sensors built into a computer, collecting the readings and sending them over a USB connection to a Teensy microcontroller, which would then display those readings on a continuously scrolling display.

I wrote the code for this project during the summer between my sophomore and junior years, when I transferred from Leeward Community College to the University of Hawaii at Manoa. I was excited to show off the concepts that I had learned in the Object-Oriented Programming class I had taken in that spring.

## Working from an example
Naturally, I didn't have much experience with programming displays using Arduino-like microcontrollers. I understood that doing so can be difficult and memory-intensive, so I looked for a display with a graphics library that could help me get started. I found the a display that would work for my purposes, and it came with a microcontroller-friendly graphics library.

![](https://www.crystalfontz.com/images/products/CFAF480128A0039TNA11/CFAF480128A0-039TN-A1-1_Front_On.jpg)

The display I chose was the [Crystalfontz 3.9\" Bar-Type EVE Display](https://www.crystalfontz.com/product/cfaf480128a0039tna11-480x128-eve-1u-display), [using the EVE display library.](https://github.com/crystalfontz/CFAF480128A0-039Tx-A1) Naturally, I downloaded the sample code and got to work testing it with the Teensy.

Here was my first mistake. The sample code was useful in understanding how the graphics library worked, but I for the most part worked within the given example, rather than starting fresh. Not only did this make the final code confusing, the examples and library were too complex and confusing for me to really work with.

Indeed, the main .ino file that holds the `setup()` and `loop()` code is overwhelmingly filled with the boilerplate example code, which only serves to complicate and confuse. I only really needed text and rectangles for my project, I didn't need access to the more advanced animation and bitmap features. For example, two of the lines in the below code snippet are actually mine.

```
void loop()
{
  //Get the current write pointer from the EVE
  uint16_t FWo;
  FWo = EVE_REG_Read_16(EVE_REG_CMD_WRITE);
  //Keep track of the RAM_G memory allocation
  uint32_t RAM_G_Unused_Start;
  RAM_G_Unused_Start = 0;
  while (1)
  {
    Sensor* sample;
    recvWithStartEndMarkers();
    FWo = Wait_for_EVE_Execution_Complete(FWo);
    // Start the display list
    FWo = EVE_Cmd_Dat_0(FWo,(EVE_ENC_CMD_DLSTART));
    // Set the default clear color to black
    FWo = EVE_Cmd_Dat_0(FWo, EVE_ENC_CLEAR_COLOR_RGB(0, 0, 0));
    // Clear the screen - this and the previous prevent artifacts between lists
    FWo = EVE_Cmd_Dat_0(FWo, EVE_ENC_CLEAR(1 /*CLR_COL*/, 1 /*CLR_STN*/, 1 /*CLR_TAG*/)); 
```

A solution to this would be using the design pattern of a Facade, where a simplified interface to complex library is provided. I could've written a simple interface that would set up and maintain an instance of the EVE library, providing access to the text and rectangle primitives. My code could then call the graphics library though this simplified interface, making the code more minimal and easier to read.

## A really, really, long constructor

Part of my plan involved creating `Sensor` objects, which would be stored in a linked list and updated over time. These `Sensor` objects could be of various types, storing sensor readings about the CPU, GPM or RAM of a computer. Here's the constructor:

```
Sensor::Sensor(char *newName, enum SensorType newSensorType, float newValue, int newOrderedSensorIndex, boolean newIsFirstCPUSensor, boolean newIsFirstGPUSensor, boolean newIsFirstRAMSensor){
  strcpy(Name, newName);
  sensorType = newSensorType;
  Value = newValue;
  OrderedSensorIndex = newOrderedSensorIndex;
  isFirstCPUSensor = newIsFirstCPUSensor;
  isFirstGPUSensor = newIsFirstGPUSensor;
  isFirstRAMSensor = newIsFirstRAMSensor;
  if(newOrderedSensorIndex < 4){
    isVisible = true;
    xpos = (newOrderedSensorIndex)*(rectwidth+padding);
  }
  else{
    isVisible = false;
    xpos = LCD_WIDTH;
  }
}
```

See the problem? The constructor is really long, with Boolean arguments stating whether that sensor is the first of its respective type. Consider that at most, one of these Booleans will be true, and most of the time they will be false.

This object is a good candidate for a Builder design pattern. In this design pattern, an object is built generically, with additional portions of the object built incrementally. So, a `Sensor` object could be built and initialized with a `SensorBuilder` class. Once per sensor type, the `SensorBuilder` class could also invoke a `makeFirst(sensorType)` function, which would set the appropriate field of the corresponding `Sensor` object Boolean true.

## Where to go from here
From these examples I can conclude that better code structure can lead to more readable, reusable code. Hopefully my mistakes can form an example to become a better programmer.

