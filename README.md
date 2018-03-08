# week 2
# Digital-Electronics
CCADigitalElectronics_Spring2018

## Synthetic Pollenizer – Robotic interventions in the real-world ecological systems
http://www.creativeapplications.net/environment/synthetic-pollenizer-robotic-interventions-in-the-real-world-ecological-systems/
The project is is a conceptual intervention in real-world ecological systems using artificial flowers. It is made by different materials and auduino. Using 3D printer to create some complex structures.  Inspired by natural pollenizers, it imitates the process of bees gathering honey in nature, these robotic replicas artificially pollinate bees, integrating into the reproductive cycle of local flora; an initiative into a cybernetic ecology. 

## 3 of the sensors on the Adafruit Sensors guide
### PIR motion sensors
https://learn.adafruit.com/pir-passive-infrared-proximity-motion-sensor/
PIR motion sensors is for sense motion, almost always used to detect whether a human has moved in or out of the sensors range. PIRs are basically made of a pyroelectric sensor, which can detect levels of infrared radiation. So it only can be used to detect the human or other lifes. 

### Photocells
https://learn.adafruit.com/photocells
Photocells are sensors that allow you to detect light. It can be used to create switchs and be adjustable resistance.

### (FSRs) Force sensitive resister
https://learn.adafruit.com/force-sensitive-resistor-fsr
FSRs can be used to detect physical pressure. The principle of this device is a pressure-controlled resistor.

# week 3
## Idea: 
I want to create a daft funk's helmet.(only the part of displaying/from Thomas)
![maxresdefault](https://user-images.githubusercontent.com/35580394/35966318-592506fe-0c72-11e8-860f-24d3df0fa50f.jpg)

who are they?: https://en.wikipedia.org/wiki/Daft_Punk https://www.youtube.com/user/daftpunkalive

Helmet?: https://www.thedaftclub.com/features/a-visual-history-of-daft-punks-helmets/

## Why I wanna make it?

I'm a fan of daft punk. I dream to create it a long time. And in this class, I have an opportunity to do it. 

## what is the function of it?

It can show some motion graphic which is record in its memory.

Also it can receipt music signal in the environment, and show different image pair to the beat of music.

Plus: Connect to the bluetooth board, and Be controled by smart phone.

## Reference1: The MAX7219 and MAX7221 Led drivers
http://playground.arduino.cc/Main/MAX72XXHardware
## Reference2:  LED Matrix red 8x8 64 Led driven by MAX7219 (or MAX7221) and Arduino Uno
https://www.youtube.com/watch?v=WYaa8wE5oFQ
## Here is an example: HUGE LED matrix with Arduino/And successful example
https://www.youtube.com/watch?v=v1vRjOU_pGA
https://www.youtube.com/watch?v=DxjmQfeYztA

# Project for blindness

This is a wearable device designed for the blind. This is a ring. It can detect the distance of 10cm-20cm, and give the user vibration feedback. When the distance is shorter, its vibration will become faster. At the same time, I also connected a yellow-green display to show the distance, which facilitated my debugging equipment.

## image：

![img_6087](https://user-images.githubusercontent.com/35580394/37162350-dfbee4bc-22a9-11e8-80b5-aa9487658b82.JPG)
![img_5990](https://user-images.githubusercontent.com/35580394/37162352-e2552092-22a9-11e8-8dc4-6d1e7c16c35e.JPG)
![img_5989](https://user-images.githubusercontent.com/35580394/37162355-e385e776-22a9-11e8-8ea9-b7ca43e9b8eb.JPG)

## Code:


    #include <Wire.h>
    #include <LiquidCrystal_I2C.h>
    // Set I2C address of LCD1602 as 0x27, LCD1602 as two lines, 16 characters per line LCD
    LiquidCrystal_I2C lcd (0x3F, 2,1,0,4,5,6,7); // set the LCD address to 0x27 for a 20 chars and 4 line display
    int GP2D12 = 0; / / Sharp GP2D12 infrared ranging sensor connected to the analog port 0
    int val; // Stores the value read from the GP2D12 IR distance sensor
    float temp; // Stores the floating-point distance value computed by the sensor after reading the value
    int distance; / / stored by the sensor to read the value, through the calculation of the integer distance value
    // Initialize the program
    void setup () {
    lcd.begin (16,2); // for 16 x 2 LCD module
    lcd.setBacklightPin (3, POSITIVE);
    lcd.setBacklight (HIGH);
    pinMode (LED_BUILTIN, OUTPUT);
    }
    // main program
    void loop () {
    // read GP2D12 infrared ranging sensor analog data
    val = analogRead (GP2D12);
    // Process the sensor readings into floating-point distance values ​​using the following formula
    temp = 2547.8 / ((float) val * 0.49-10.41) -0.42;
    lcd.clear (); // LCD clear screen
    // Position the cursor on the LCD line 0, column 0
    lcd.setCursor (0, 0);
    // Display "Distance:" on the 0th row and 0th column of LCD
    lcd.print ("Distance:");
    // Position the cursor on the LCD line 2, column 8
    lcd.setCursor (7, 1);
    // If the sensor reading is greater than 80 or less than 16,
    if (temp> 80 || temp <10.)
    {
    // Then LCD displays "OverRange" in row 1 and column 7
    lcd.print ("OverRange");

  
    }
    // If the sensor reads between 10 and 80,
    else
    {
    // Round floating-point distance value
    distance = int (temp);
    // The second line in the LCD, the beginning of the eighth column distance value
    lcd.print (distance);
    // Display the unit "cm" after the distance value
    lcd.print ("cm");
    digitalWrite (LED_BUILTIN, HIGH);
    delay (distance * 5);
    digitalWrite (LED_BUILTIN, LOW);
    delay (distance * 5);
    }
    }

