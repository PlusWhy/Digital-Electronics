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
    //设置LCD1602的I2C地址为0x27，LCD1602为两行，每行16个字符的液晶显示器
    LiquidCrystal_I2C lcd(0x3F, 2, 1, 0, 4, 5, 6, 7); // set the LCD address to 0x27 for a 20 chars and 4 line display
    int GP2D12 = 0;//把夏普GP2D12红外测距传感器连接在模拟量端口0
    int val; //存储从GP2D12红外测距传感器读到的值
    float temp;//存储由传感器读取值，通过计算处理后的浮点型距离值
    int distance;//存储由传感器读取值，通过计算处理后的整数型距离值
    //初始化程序


    void setup() {
    lcd.begin (16, 2); // for 16 x 2 LCD module
    lcd.setBacklightPin(3, POSITIVE);
    lcd.setBacklight(HIGH);
    pinMode(LED_BUILTIN, OUTPUT);
    }
    //主程序
    void loop() {
    //读取GP2D12红外测距传感器模拟量数据
    val = analogRead(GP2D12);
    //通过以下算式，把传感器读取值处理成浮点型距离值
    temp = 2547.8 / ((float)val * 0.49 - 10.41) - 0.42;
    lcd.clear();//LCD清屏
    // 定位光标在LCD第0行、第0列
    lcd.setCursor(0, 0);
    //在LCD第0行第0列开始显示"Distance:"
    lcd.print("Distance:");
    // 定位光标在LCD第2行、第8列
    lcd.setCursor(7, 1);
    //如果传感器读取值大于80或者小于16，
    if (temp > 80 || temp < 10.)
    {
    //则在LCD第1行、第7列开始显示"OverRange"
    lcd.print("OverRange");


    }
    //如果传感器读取值在10到80之间，
    else
    {
    //把浮点型距离值取整
    distance = int(temp);
    //则在LCD第2行、第8列开始显示距离值
    lcd.print(distance);
    //在距离值后显示单位"cm"
    lcd.print("cm");
    digitalWrite(LED_BUILTIN, HIGH);
    delay(distance * 5);
    digitalWrite(LED_BUILTIN, LOW);
    delay(distance * 5);
    }
    }

# Final project

## Blindness Glove

It is a wearable device that helps blind people. Users can explore the world through it. Blindness glove can convert colors to sound frequencies and also convert distances to vibration frequencies. It can detect the distance of 10cm-20cm, and give the user vibration feedback. Also, it can detect rgb color and transfer to hsl(hue,s...,l...), and convert hue data to sound frequency. Because the limitation of hue, it cannot tell black and white to blindness.
### Image

![img_4018](https://user-images.githubusercontent.com/35580394/39659271-a0e0d324-4fd9-11e8-93e4-1760901facf6.JPG)

<img width="1596" alt="screen shot 2018-05-04 at 8 28 33 pm" src="https://user-images.githubusercontent.com/35580394/39659280-c512068c-4fd9-11e8-96d3-a734e61f2cd7.png">


![img_4020](https://user-images.githubusercontent.com/35580394/39659272-a481fce2-4fd9-11e8-84bd-ec9232d0ebf4.JPG)

### Video

https://youtu.be/fkrfpTzuxd0

### Paper reference(color to sound frequency)

[colorNsound_SoohyunPark.pdf](https://github.com/PlusWhy/Digital-Electronics/files/1976294/colorNsound_SoohyunPark.pdf)

[MarciaRojasPoster.pdf](https://github.com/PlusWhy/Digital-Electronics/files/1976295/MarciaRojasPoster.pdf)

<img width="698" alt="screen shot 2018-04-25 at 4 12 37 pm" src="https://user-images.githubusercontent.com/35580394/39659314-8d4c6070-4fda-11e8-9917-96dc751dc54a.png">


### Code

    #include <Wire.h>
    #include "Adafruit_TCS34725.h"

    #define commonAnode true
    #define MAX(a, b) (((a) > (b)) ? (a) : (b))
    #define MIN(a, b) (((a) < (b)) ? (a) : (b))

    int GP2D12=A0;
    int val;
    float temp;
    int distance;

    const int speaker = 9;



    byte gammatable[256];


    Adafruit_TCS34725 tcs = Adafruit_TCS34725(TCS34725_INTEGRATIONTIME_50MS, TCS34725_GAIN_4X);

    void setup() {
    Serial.begin(9600);
  
    while(!Serial){
    }
  
    Serial.println("Color View Test!");
    pinMode(GP2D12, INPUT);
    pinMode(LED_BUILTIN, OUTPUT);

    if (tcs.begin()) {
    Serial.println("Found sensor");
    } else {
    Serial.println("No TCS34725 found ... check your connections");
    while (1); // halt!
    }


    for (int i = 0; i < 256; i++) {
    float x = i;
    x /= 255;
    x = pow(x, 2.5);
    x *= 255;

    if (commonAnode) {
      gammatable[i] = 255 - x;
    } else {
      gammatable[i] = x;
    }
    //Serial.println(gammatable[i]);
     }
    }


    void loop() {

    Serial.println("Begin Loop");
  


    uint16_t clear, red, green, blue;



    delay(60);  // takes 50ms to read

    tcs.getRawData(&red, &green, &blue, &clear);


    // Figure out some basic hex code for visualization
    uint32_t sum = clear;
    float r, g, b;
    r = red; r /= sum;
    g = green; g /= sum;
    b = blue; b /= sum;
    r *= 256; g *= 256; b *= 256;


    //  Serial.print((int)r ); Serial.print(" "); Serial.print((int)g); Serial.print(" ");  Serial.println((int)b );
    float r1, g1, b1;
    r1 = r / 255;
    g1 = g / 255;
    b1 = b / 255;

    //  Serial.print(r1 ); Serial.print(" "); Serial.print(g1); Serial.print(" ");  Serial.println(b1);
    float hue;
    float saturation;
    float luminance;
    float fmax, fmin;
    fmax = MAX(MAX(r1, g1), b1);
    fmin = MIN(MIN(r1, g1), b1);
    luminance = fmax;
    if (fmax > 0)
    {
    saturation = (fmax - fmin) / fmax;
    }
    else
    {
    saturation = 0;
    }


    if (saturation == 0)
    {
    hue = 0;
    }
    else
    {
    if (fmax == r1)
    {
      hue = (g1 - b1) / (fmax - fmin);
    }
    else if (fmax == g1)
    {
      hue = 2 + (b1 - r1) / (fmax - fmin);
    }
    else
    {
      hue = 4 + (r1 - g1) / (fmax - fmin);
    }

    hue = hue / 6;
    if (hue < 0) {
      hue += 1;
    }
    }
    //Serial.println(hue);
    int hue1;
    hue1 = hue * 100;

    int thisPitch = map(hue1, 0, 100, 2000, 4000);
    //Serial.println(thisPitch);
    if (hue1 < 10) {
    noTone(speaker);
    }
    else
    {
    tone(speaker, thisPitch, 5000);
     }

  
    val = analogRead(GP2D12);
    //通过以下算式，把传感器读取值处理成浮点型距离值
    temp = 2547.8 / ((float)val * 0.49 - 10.41) - 0.42;

     if(temp>70||temp<13.)
      {
    digitalWrite(LED_BUILTIN, LOW);

    }

    else
    { 
    //把浮点型距离值取整
    distance=int(temp);
    //则在LCD第2行、第8列开始显示距离值    lcd.print(distance);
    //在距离值后显示单位"cm"    lcd.print("cm");

    digitalWrite(LED_BUILTIN, HIGH);
    delay(distance*5);
    digitalWrite(LED_BUILTIN, LOW);
    delay(distance*5);
    }
    Serial.println(distance);
    }



