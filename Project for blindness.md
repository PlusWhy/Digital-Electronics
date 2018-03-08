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
