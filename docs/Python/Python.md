# **Python Tutorial**

## Getting Started With Python

**Copy Example Code Folder to Raspberry Pi**

Place example code folder to the pi folder of Raspberry Pi. and extract the example code from pythonCode_A zip file, as shown below:

![](media/e7b577a013d27250449f6a6062f2a692.png)

![](media/ceeca4fcc724fe5da3f118cd9776d640.png)

![](media/f71231eb68d53af8e9c75404b72957c6.png)

Double-click the pythonCode_A folder to look through compiled files, as shown below:

![](media/acfe333ae490c46137d33767276a39b1.png)

Set the default editor of file with .py

Right-click“Open with...”

![](media/356fd7db62ab9386b2ae35c8cfdf17b0.png)

Click Programming to select Geany Programmer’s Editor

![](media/32fb8fddb6b983ff07ec3e23ea3c993a.png)

Then, we can directly double-click Geany Programmer’s Editor to open .py files.

**Run \_HelloWorld.py file to print“Hello World”**

One is to double-click 1_HelloWorld.py and tap ![](media/f89bd2694f774f46c67ccb4e413da8c5.png)to compile code and check grammar errors. After successful compilation, tap ![](media/08d144c345509313cf1abe21c9d14683.png) to run the code. At same time, terminal appears and prints“hello world”

![](media/3fb5441497bc964a18790a139fed11fb.png)

![](media/a48b5e2f9823e1f066273fc4acd38dcb.png)

![](media/97663e45e8df08b6edb5143176e849ad.png)

The other way is to open terminal directly, input the following commands and press“Enter”to print“hello world！”

cd pythonCode_A python 1_HelloWorld.py

![](media/2773d0c5a1f43379c9ba887beaf2c334.png)

![](media/02792a61a9f23c015aa84fcc739a72fc.png)



## Projects：

**Note**: 

G, - and GND marked on sensors and modules are so-called negative, which are connected to GND of GPIO extension board or “-” of breadboard; 

V、+、VCC are known as positive, which are interfaced 3V3 or 5V on extension board and“+”on breadboard.

### Project 1：Python3 Shell

Use windows remote desktop connection to enter the page of Raspberry Pi, then open its terminal.

![](media/00f6bd6f6051a710d7ad079dbe71bdf1.png)

Input python3 in terminal and enter the python3 shell interface, then input print(“hello,world!”) and press“Enter”, “hello,world ! will be output.

![](media/aaba2bff9c7b39c37eecb24db34302c1.png)

You may find function print() is used to print data.

You could print other type data, like Mathematical formula:

print(1+5)

Variable a = 2 b = 5

print(a\*b)

As shown below:

![](media/208c155326c0223a9c8ae287c8f82201.png)

Input exit() to exit python3 shell

![](media/8eca404792bd60a4a7f190ce0e44dfb8.png)

### Project 2：LED Blink

Description:

Let’s start from a rather basic and simple experiment----LED Blink

Components:

| ![image-20230421150007807](media/image-20230421150007807.png) | ![image-20230421150012185](media/image-20230421150012185.png) | ![image-20230421150016553](media/image-20230421150016553.png) | ![image-20230421150020697](media/image-20230421150020697.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40pin Colorful Jumper Wires*1                                | Breadboard*1                                                 |
| ![image-20230421150024897](media/image-20230421150024897.png) | ![image-20230421150030046](media/image-20230421150030046.png) | ![image-20230421150034681](media/image-20230421150034681.png) |                                                              |
| LED - Red *1                                                 | 220Ω Resistor*1                                              | Jumper Wires                                                 |                                                              |



Component Description:

**LED**:

A light-emitting diode, the current is connected when anode(long pin) is connected to VCC, and cathode(short pin)is connected to GND. Its brightness is 2V and current is 6mA. LED must be connected to a resistor in the circuit, otherwise, the components will be burned.

**Resistor**: 

we use a carbon film resistor, 220Ωand its accuracy is 5%, why choose 220Ω resistor?

Since the high-level output voltage of GPIO pin of the Raspberry Pi is 3.3V, and the voltage of the LED is about 2V, and the current is about 6mA, we need to use a resistor to bear the voltage (3.3V-2V) = 1.3V, according to ohm The law: U/I = R knows: (3.3-2)/6 \* 1000 ≈ 217Ω.

**Breadboard**: 

Below is a short instruction of breadboard. The holes on the board are connected. The inner board is structure diagram.

![](media/49dc0f2393ed6f04d8f4cc1239e96995.png)

Schematic Diagram：

![](media/9d31d0ea6821d91e18f1360d36c3c742.png)

**Connection Diagram:**

![](media/cff6263dc30aba5782cb38f7e8c0fe2e.png)

Since the PIN numbers of GPIO Extension Board and RPi GPIO are same, the part of breadboard and GPIO Extension Board is only shown on further connection diagram.

![](media/86e444ee07fd33bfa2ca8d896e571117.png)

Working Principle：

The positive pole of LED is connected to GPIO18, when the pin of GPIO18 outputs 3.3V, LED will be on; when its pin outputs 0V, LED will be off.



Run Example Code

Input the following commands in the terminal and press“Enter”

cd /home/pi/pythonCode_A

python 2_Led_Blink.py

![](media/c43775582b8e9ca6e07c7050c4593356.png)

Test Result：

Terminal prints and LED flashes.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO

import time

 

ledPin = 18  #define led pin

 

GPIO.setmode(GPIO.BCM)     # use BCM numbers

GPIO.setup(ledPin,GPIO.OUT)  #set the ledPin OUTPUT mode

GPIO.output(ledPin,GPIO.LOW)  # make ledPin output LOW level

 

while True:   #loop

  GPIO.output(ledPin,GPIO.HIGH)  #turn on led

  print("turned on the led")  #Print in the terminal

  time.sleep(1)        #wait for 1 second

  GPIO.output(ledPin,GPIO.LOW)  #turn off led

  print("turned off the led")

  time.sleep(1)

 

GPIO.cleanup()   #release all GPIO
```



Explanation：

**While**

While is the loop statement of python，when the condition is true, the program will be executed always be executed.

**import RPi.GPIO as GPIO**

Import RPi.GPIO library，which can be used to control the digital output of Raspberry Pi and PWM output.

GPIO.setmode(GPIO.BCM)

There are many definitions about pins of Raspberry Pi, on this condition, we definite pin as BCM digital pin

More resource：

https://sourceforge.net/p/raspberry-gpio-python/wiki/Examples/

**import time**

Import time library, time.sleep(1) means waiting for a second

More resource：

https://sourceforge.net/p/raspberry-gpio-python/wiki/Examples/



### Project 3：SOS Light

Description：

S.O.S is a Morse code distress signal , used internationally, that was originally established for maritime use. We will present it with flashing LED

Components:

| ![image-20230421150430459](media/image-20230421150430459.png) | ![image-20230421150434733](media/image-20230421150434733.png) | ![image-20230421150439436](media/image-20230421150439436.png) | ![image-20230421150443630](media/image-20230421150443630.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230421150448205](media/image-20230421150448205.png) | ![image-20230421150455276](media/image-20230421150455276.png) | ![image-20230421150500206](media/image-20230421150500206.png) |                                                              |
| LED - Red *1                                                 | 220ΩResistor*1                                               | Jumper Wires                                                 |                                                              |



Schematic Diagram：

![](media/9d31d0ea6821d91e18f1360d36c3c742.png)

Connection Diagram

![](media/86e444ee07fd33bfa2ca8d896e571117.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 3_LED_SOS.py



Test Result：

LED flashes quickly for three times, three times slowly and quickly three times, the terminal prints ... \_ \_ \_ ...

![](media/ee4276aee81e439e8ba7697500118797.png)

Note: Press Ctrl + C on keyboard to exit code running

Example Code:

```python
import RPi.GPIO as GPIO
import time

ledPin = 18  #define led pin
i1 = 0
i2 = 0
i3 = 0

GPIO.setmode(GPIO.BCM)        # use BCM numbers
GPIO.setup(ledPin,GPIO.OUT)   #set the ledPin OUTPUT mode
GPIO.output(ledPin,GPIO.LOW)  # make ledPin output LOW level

while True:    #loop
    while(i1<3):
        GPIO.output(ledPin,GPIO.HIGH)  #turn on led
        time.sleep(0.1)              #wait for 1 second
        GPIO.output(ledPin,GPIO.LOW)   #turn off led
        time.sleep(0.1)
        print(".")
        i1 += 1
    
    while(i2<3):
        GPIO.output(ledPin,GPIO.HIGH)  #turn on led
        time.sleep(1)              #wait for 1 second
        GPIO.output(ledPin,GPIO.LOW)   #turn off led
        time.sleep(1)
        print("_")
        i2 += 1
    
    while(i3<3):
        GPIO.output(ledPin,GPIO.HIGH)  #turn on led
        time.sleep(0.1)              #wait for 1 second
        GPIO.output(ledPin,GPIO.LOW)   #turn off led
        time.sleep(0.1)
        print(".")
        i3 += 1
    time.sleep(3)
    i1 = 0
    i2 = 0
    i3 = 0
    

GPIO.cleanup()    #release all GPIO
```

### Project 4：Breathing LED

Description：

A“breathing LED”is a phenomenon where an LED's brightness smoothly changes from dark to bright and back to dark, continuing to do so and giving the illusion of an LED“breathing.”This phenomenon is similar to a lung breathing in and out. So how to control LED’s brightness? We need to take advantage of PWM.

Components：

| ![image-20230421150755798](media/image-20230421150755798.png) | ![image-20230421150801118](media/image-20230421150801118.png) | ![image-20230421150805816](media/image-20230421150805816.png) | ![image-20230421150810222](media/image-20230421150810222.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230421150815263](media/image-20230421150815263.png) | ![image-20230421150821038](media/image-20230421150821038.png) | ![image-20230421150825224](media/image-20230421150825224.png) |                                                              |
| LED - Red *1                                                 | 220ΩResistor *1                                              | Jumper Wires                                                 |                                                              |



Working Principle：

We use the PWM output of GPIO, PWM outputs analog signals and output value is 0\~100 which is equivalent to output voltage 0\~3.3V from GPIO port.

According to Ohm's law: U/R = I, the resistance is 220Ω, and the value of voltage U changes, so does the value of current I, which can control the brightness of the LED lamp.

PWM (Pulse Width Modulation) is the control of the analog circuit through the digital output of microcomputer and a method that making digital coding on analog signal levels.

It sends square waves with certain frequency through digital pins, that is, high level and low level are output alternately for a period of time. Total time of each group high and low level is fixed, which is called cycle.

The time of high level output is pulse width whose percentage is called Duty Cycle. The longer that high level lasts, the larger the duty cycle of analog signals is, the corresponding voltage as well

Below chart is pulse width 50%, then the output voltage is 3.3 \* 50% = 1.65V，the brightness of LED is medium.

![](media/1ce12a5fbfdb0ea129bbbe0d2ffb9f2d.png)

Schematic Diagram：

![](media/9d31d0ea6821d91e18f1360d36c3c742.png)

**Connection Diagram**

![](media/86e444ee07fd33bfa2ca8d896e571117.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 4_Led_Breath.py



Test Result：

LED gradually brightens then darkens

Note: Press Ctrl + C on keyboard to exit code running



Example Code：

```python
import RPi.GPIO as GPIO
import time

ledPin = 18  #define led pin

GPIO.setmode(GPIO.BCM)  # use BCM numbers
GPIO.setup(ledPin,GPIO.OUT) #set the ledPin OUTPUT mode
GPIO.output(ledPin,GPIO.LOW)  # make ledPin output LOW level
pwm = GPIO.PWM(18,100)  #create a PWM instance
pwm.start(0)   #start PWM

def brighten():  #define function
    for i in range(0,100,+1):
        pwm.ChangeDutyCycle(i)  #change the frequency,To lighten gradually
        time.sleep(0.01)
        
def darken(): 
    for i in range(100,0,-1):
        pwm.ChangeDutyCycle(i) #To darken gradually
        time.sleep(0.01)
    
while True:     #loop
    brighten()  #call function
    darken()

pwm.stop()  #stop PWM

GPIO.cleanup()    #release all GPIO
```



### Project 5：Traffic Lights

Description：

In this lesson, we will learn how to control multiple LED lights and simulate the operation of traffic lights.

Traffic lights are signaling devices positioned at road intersections, pedestrian crossings, and other locations to control flows of traffic.

Green light on: Allows traffic to proceed in the direction denoted, if it is safe to do so and there is room on the other side of the intersection.

Red light: Prohibits any traffic from proceeding. A flashing red indication requires traffic to stop and then proceed when safe (equivalent to a stop sign).

Amber light (also known as 'orange light' or 'yellow light'):

Warns that the signal is about to change to red, with some jurisdictions requiring drivers to stop if it is safe to do so, and others allowing drivers to go through the intersection if safe to do so.

Components：

| ![image-20230421151012801](media/image-20230421151012801.png) | ![image-20230421151017775](media/image-20230421151017775.png) | ![image-20230421151022176](media/image-20230421151022176.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230421151033665](media/image-20230421151033665.png) | ![image-20230421151038415](media/image-20230421151038415.png) | ![image-20230421151043279](media/image-20230421151043279.png) |
| Breadboard*1                                                 | LED - Red *1                                                 | Jumper Wires                                                 |
| ![image-20230421151057429](media/image-20230421151057429.png) | ![image-20230421151101215](media/image-20230421151101215.png) | ![image-20230421151104896](media/image-20230421151104896.png) |
| LED - Green*1                                                | LED - Yellow*1                                               | 220Ω Resistor*3                                              |



Schematic Diagram：

![](media/cfee321c7d9cb39f2327c2577b3332f9.png)

![](media/78414f7f1aa3081a54b9ea7e4e679b5f.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 5_traffic_light.py



Test Result：

Red light is on 5s and off, yellow light flashes 3s and turn off, green light is lit for 5s and off, in loop way.

Note: Press Ctrl + C on keyboard to exit code running



Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep

#LED pin
red = 18
yellow = 23
green = 24

GPIO.setmode(GPIO.BCM)  # use BCM numbers
GPIO.setup(red,GPIO.OUT)  #set the ledPin OUTPUT mode
GPIO.setup(yellow,GPIO.OUT)
GPIO.setup(green,GPIO.OUT)

GPIO.output(red,GPIO.LOW)
GPIO.output(yellow,GPIO.LOW)
GPIO.output(green,GPIO.LOW)

while True:
    GPIO.output(red,GPIO.HIGH)
    sleep(5)
    GPIO.output(red,GPIO.LOW)
    GPIO.output(yellow,GPIO.HIGH) #turn on yellow_led
sleep(0.5)
GPIO.output(yellow,GPIO.LOW) #turn off yellow_led
sleep(0.5)
GPIO.output(yellow,GPIO.HIGH)
sleep(0.5)
GPIO.output(yellow,GPIO.LOW) 
sleep(0.5)
GPIO.output(yellow,GPIO.HIGH) 
sleep(0.5)
GPIO.output(yellow,GPIO.LOW) 
sleep(0.5)

GPIO.output(green,GPIO.HIGH)  #turn on green_led
sleep(5)     #delay 5s
GPIO.output(green,GPIO.LOW)   #turn off green_led
    
GPIO.cleanup()   #release all GPIO
```



### Project 6：RGB Light

Description：

In this chapter, we will demonstrate how RGB lights show different colors via programming

Components：

| ![image-20230421151238793](media/image-20230421151238793.png) | ![image-20230421151242977](media/image-20230421151242977.png) | ![image-20230421151246529](media/image-20230421151246529.png) | ![image-20230421151250817](media/image-20230421151250817.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin ColorfulJumper Wires*1                                | Breadboard*1                                                 |
| ![image-20230421151308219](media/image-20230421151308219.png) | ![image-20230421151313408](media/image-20230421151313408.png) | ![image-20230421151317344](media/image-20230421151317344.png) |                                                              |
| RGB - LED *1                                                 | 100Ω Resistor*3                                              | Jumper Wires                                                 |                                                              |



Component Knowledge：

We use common cathode RGB lights.

**Working Principle：**

RGB LED integrated three LEDs emitting red,green and blue light. It has 4 pins，long pin (-) is a shared pin, that is, the negative port of 3LED, as shown below, we control three LEDs to emit light with different brightness to make RGB show different colors.

![](media/b5101c5335953ef0e2127da47c1823f0.png)

Red, green and blue are three primary colors. They could produce all kinds of visible lights when mixing them up. Computer screen, single pixel mobile phone screen, neon light work under this principle.

![](media/9dc453addddb19e4fd5914dd14e51702.png)

Next, we will make a RGB LED displaying all kinds of colors

Schematic Diagram：

![](media/04d2937217700e739cd0c1febdd42351.png)

![](media/c342422f2ba2b27f6158e6163a3ccdaf.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 6_RGB_led.py



Test Result：

RGB lights show colors randomly

Note: Press Ctrl + C on keyboard to exit code running



Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep
import random

#define RGB pin
pin_R = 24
pin_G = 23
pin_B = 18
GPIO.setmode(GPIO.BCM)  # use BCM numbers
#set the RGB Pin OUTPUT mode
GPIO.setup(pin_R,GPIO.OUT)
GPIO.setup(pin_G,GPIO.OUT)
GPIO.setup(pin_B,GPIO.OUT)

#makeRGB Pin output LOW level
GPIO.output(pin_R,GPIO.HIGH)
GPIO.output(pin_G,GPIO.HIGH)
GPIO.output(pin_B,GPIO.HIGH)

#set pwm frequence to 1000hz
pwm_R = GPIO.PWM(pin_R,100)
pwm_G = GPIO.PWM(pin_G,100)
pwm_B = GPIO.PWM(pin_B,100)
#set inital duty cycle to 0
pwm_R.start(0)
pwm_G.start(0)
pwm_B.start(0)

#function. receive the value to display different colors
def setColor(val_R,val_G,val_B):
    pwm_R.ChangeDutyCycle(val_R)
    pwm_G.ChangeDutyCycle(val_G)
    pwm_B.ChangeDutyCycle(val_B)

while True:
    # get a random in 0~100
    R = random.randint(0,100)
    G = random.randint(0,100)
    B = random.randint(0,100)
    setColor(R,G,B)  #set the color value
    print('Red=%d, Green = %d, Blue = %d' %(R, G, B))
    sleep(0.2)
    
#stop pwm
pwm_R.stop()
pwm_G.stop()
pwm_B.stop()

GPIO.cleanup()  #release all GPIO
```



### Project 7：Flow Light

Description：

What is flow light? Maybe you see it on the wall of buildings and billboards. It is a scene that LED gradually brightens then darkens one by one.

Components：

| ![image-20230421151437328](media/image-20230421151437328.png) | ![image-20230421151456242](media/image-20230421151456242.png) | ![image-20230421151443218](media/image-20230421151443218.png) | ![image-20230421151447266](media/image-20230421151447266.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | Breadboard*1                                                 | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230421151518610](media/image-20230421151518610.png) | ![image-20230421151525628](media/image-20230421151525628.png) | ![image-20230421151529763](media/image-20230421151529763.png) |                                                              |
| LED - Red *8                                                 | 220Ω Resistor*8                                              | Jumper Wires                                                 |                                                              |



Schematic Diagram：

![](media/ce96ac0e062033019ef22efed248d112.png)
![](media/510afde336376c085736faf14e74a83a.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 7_LED_Chasing_Effect.py



Test Result：

Eight LED lights change from light to dark then back to dark, one by one.

Note: Press Ctrl + C on keyboard to exit code runningExample Code：



Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep

#LED pin
led1 = 18
led2 = 23
led3 = 24
led4 = 25
led5 = 12
led6 = 16
led7 = 20
led8 = 21


GPIO.setmode(GPIO.BCM) # use BCM numbers
#set the ledPin OUTPUT mode
GPIO.setup(led1,GPIO.OUT)
GPIO.setup(led2,GPIO.OUT)
GPIO.setup(led3,GPIO.OUT)
GPIO.setup(led4,GPIO.OUT)
GPIO.setup(led5,GPIO.OUT)
GPIO.setup(led6,GPIO.OUT)
GPIO.setup(led7,GPIO.OUT)
GPIO.setup(led8,GPIO.OUT)

while True:
    #Led lights are lit one by one
    GPIO.output(led1,GPIO.HIGH)
    sleep(0.2)   # the delay size to control the speed of the water lamp 
    GPIO.output(led2,GPIO.HIGH)
    sleep(0.2)
    GPIO.output(led3,GPIO.HIGH)
    sleep(0.2)
    GPIO.output(led4,GPIO.HIGH)
    sleep(0.2)
    GPIO.output(led5,GPIO.HIGH)
    sleep(0.2)
    GPIO.output(led6,GPIO.HIGH)
    sleep(0.2)
    GPIO.output(led7,GPIO.HIGH)
    sleep(0.2)
    GPIO.output(led8,GPIO.HIGH)
    sleep(0.2)
    #Led lights go out one by one
GPIO.output(led8,GPIO.LOW)
sleep(0.2)
GPIO.output(led7,GPIO.LOW)
sleep(0.2)
GPIO.output(led6,GPIO.LOW)
sleep(0.2)
GPIO.output(led5,GPIO.LOW)
sleep(0.2)
GPIO.output(led4,GPIO.LOW)
sleep(0.2)
GPIO.output(led3,GPIO.LOW)
sleep(0.2)
GPIO.output(led2,GPIO.LOW)
sleep(0.2)
GPIO.output(led1,GPIO.LOW)
sleep(0.2)

GPIO.cleanup()  #release all GPIO
```



### Project 8: Doorbell

**Description：**

In this project, we will demonstrate how a doorbell works.

**Components：**

| ![image-20230421151829004](media/image-20230421151829004.png) | ![image-20230421151832580](media/image-20230421151832580.png) | ![image-20230421151839844](media/image-20230421151839844.png) | ![image-20230421151843268](media/image-20230421151843268.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230421151853189](media/image-20230421151853189.png) | ![image-20230421151856836](media/image-20230421151856836.png) | ![image-20230421151901140](media/image-20230421151901140.png) | ![image-20230421151904709](media/image-20230421151904709.png) |
| Active Buzzer *1                                             | Jumper Wires                                                 | 10KΩ Resistor*1                                              | Button Switch *1                                             |



**Components Knowledge:**

**Active buzzer：**

An active buzzer will generate a tone using an internal oscillator, so all that is needed is a DC voltage. A passive buzzer requires an AC signal to make a sound. It is like an electromagnetic speaker, where a changing input signal produces the sound, rather than producing a tone automatically.

As a type of electronic buzzer with integrated structure, buzzers, which are supplied by DC power, are widely used in computers, printers, photocopiers, alarms, electronic toys, automotive electronic devices, telephones, timers and other electronic products for voice devices. 

Buzzers can be categorized as active and passive ones (see the following picture). Turn the pins of two buzzers face up, and the one with a green circuit board is a passive buzzer, while the other enclosed with a black tape is an active one.

Button switch: it can control circuit. Before pressed, the current can’t pass from one end to the other end. Both ends are like two mountains. There is a river in between. We can't cross this mountain to another mountain. When pressed, my internal metal piece is connecting the two sides to let the current pass, just like building a bridge to connect the two mountains.

Inner structure:![](media/16f4251f460613a7df58a30cfde2a158.png)

1 and 1 , 2 and 2 are connected , however, 1 and 2 are disconnected when the button is not pressed; 1 and 2 are connected when pressing the button.

**10KΩ resistor**：

It is pull-up resistor. The high and low levels of Raspberry Pi will be unstable if connecting only GPIO pins instead of resistors.

Resistor could stabilize the electronic signal and protect circuit.

The circuit will be shorten and components will be burnt if without wiring 10kΩ resistor, as shown below;

Schematic Diagram：

![](media/c32ca6a87be4a8615bd30fb54892f3d5.png)

![](media/b45c9fa077f46f2c55b662a37ac2adca.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 8_active_buzzer.py



Test Result：

The buzzer will emit sounds and terminal will print 0 if the button is pressed; otherwise, buzzer will keep quiet and terminal will output 1.

Note: Press Ctrl + C on keyboard to exit code running



Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep

#active buzzer pin
buzPin = 27
#button pin
btnPin = 18

GPIO.setmode(GPIO.BCM) # use BCM numbers
GPIO.setup(buzPin,GPIO.OUT)  #set buzPin OUTPUT mode
GPIO.setup(btnPin,GPIO.IN,GPIO.PUD_UP)  # set btnPin INPUT mode

while True:
    val = GPIO.input(btnPin)
    print(val);
    if(val == 0):  #Judge whether the button is pressed
        GPIO.output(buzPin,GPIO.HIGH)  #Buzzer ring
    else:
        GPIO.output(buzPin,GPIO.LOW)   #buzzer off
        
GPIO.cleanup() # Release all GPIO
```



### Project 9：Passive Buzzer

Description：

We will conduct an interesting experiment-----control passive buzzer to compose a song.

Components：

| ![image-20230421151951467](media/image-20230421151951467.png) | ![image-20230421151955813](media/image-20230421151955813.png) | ![image-20230421151959174](media/image-20230421151959174.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230421152005077](media/image-20230421152005077.png) | ![image-20230421152008773](media/image-20230421152008773.png) | ![image-20230421152012166](media/image-20230421152012166.png) |
| Breadboard*1                                                 | Passive Buzzer *1                                            | Jumper Wires                                                 |



Component Knowledge

**Passive buzzer**：

Passive buzzer is a type of electronic buzzer with integrated structure.

Buzzers can be categorized as active and passive ones (see the following picture).

An active buzzer has a built-in oscillating source, so it will make sounds when electrified. But a passive buzzer does not have such source, so it will not tweet if DC signals are used; instead, you need to use square waves whose frequency is between 2K and 5K to drive it. 

The active buzzer is often more expensive than the passive one because of multiple built-in oscillating circuits.

Turn the pins of two buzzers face up, and the one with a green circuit board is a passive buzzer, while the other enclosed with a black tape is an active one, as shown：

![](media/2b43a77b1b9792fc8b902f0b24c0f004.png)

Passive buzzer provides alternating current to sound coils to make electronic magnet and permanent magnet attraction or repulsion so as to push vibration film to emit sound, according to electromagnetic induction.

Only certain frequency with high and low levels can make passive buzzer emit sound, since DC current only makes vibration film vibrated continuously rather than producing sound.

Schematic and Connection Diagram

![](media/fa845f49ab735773573c648b3ad9eaac.png)

![](media/4bcd2163458dbec4afb3f0ca73c40a97.png)

Run Example Code1：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 9.1_passive_buzzer.py

Test Result1：

Passive emits“tick, tick”sounds.

Note: Press Ctrl + C on keyboard to exit code running

Example Code1：

```python
#!/usr/bin/env python

-*- coding: utf-8 -*-

import time
import RPi.GPIO as GPIO

buzPin = 18
i1 = 0
i2 = 0
GPIO.setmode(GPIO.BCM)
GPIO.setup(buzPin, GPIO.OUT)

try:
    while 1:  #loop
        while(i1<50):
            GPIO.output(buzPin,GPIO.HIGH)
            time.sleep(0.001)              #wait for 1 ms
            GPIO.output(buzPin,GPIO.LOW)
            time.sleep(0.001)
            i1 = i1 + 1
        time.sleep(0.3)
        while(i2<50):
            GPIO.output(buzPin,GPIO.HIGH)
            time.sleep(0.001)              #wait for 1 ms
            GPIO.output(buzPin,GPIO.LOW)
            time.sleep(0.001)
            i2 = i2 + 1
        time.sleep(1)
        i1 = 0
        i2 = 0
except KeyboardInterrupt:
    pass
p.stop()  #stop pwm
GPIO.cleanup() #release all GPIO
```

Run Example Code2：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 9.2_passive_buzzer.py

Test Result2：

Passive buzzer plays a“Happy Birthday”song.

Note: Press Ctrl + C on keyboard to exit code running

Example Code2：

```python
-*- coding: utf-8 -*-

import RPi.GPIO as GPIO
import time

Buzzer = 18  # set the Pin

Happy birthday

Do = 262  
Re = 294  
Mi = 330  
Fa = 349  
Sol = 392  
La = 440  
Si = 494  
Do_h = 523  
Re_h = 587  
Mi_h = 659  
Fa_h = 698  
Sol_h = 784  
La_h = 880  
Si_h = 988

The tune

song_1 = [ 
    Sol,Sol,La,Sol,Do_h,Si,
    Sol,Sol,La,Sol,Re_h,Do_h,
    Sol,Sol,Sol_h,Mi_h,Do_h,Si,La,
    Fa_h,Fa_h,Mi_h,Do_h,Re_h,Do_h
]

delay

beat_1 = [
    0.5,0.5,1,1,1,1+1,
    0.5,0.5,1,1,1,1+1,
    0.5,0.5,1,1,1,1,1,
    0.5,0.5,1,1,1,1+1,
]


def setup():
    GPIO.setmode(GPIO.BCM)       # Numbers GPIOs by physical location
    GPIO.setup(Buzzer, GPIO.OUT)    # Set pins' mode is output
    global Buzz                     # Assign a global variable to replace GPIO.PWM 
    Buzz = GPIO.PWM(Buzzer, 440)    # 440 is initial frequency.
    Buzz.start(50)                  # Start Buzzer pin with 50% duty ration

def loop():
    while True:
        print('\n    Playing song 3...')
        for i in range(0, len(song_1)):     # Play song 1
            Buzz.ChangeFrequency(song_1[i]) # Change the frequency along the song note
            time.sleep(beat_1[i] * 0.5)     # delay a note for beat * 0.5s

def destory():
    Buzz.stop()                 # Stop the buzzer
    GPIO.output(Buzzer, 1)      # Set Buzzer pin to High
    GPIO.cleanup()              # Release resource

if __name__ == '__main__':      # Program start from here
    setup()
    try:
        loop()
    except KeyboardInterrupt:   # When 'Ctrl+C' is pressed, the child program destroy() will be  executed.
        destroy()
```



### Project 10：1-Digit 7 Segment LED Display

Description：

To make LED display numbers, human being invented digital display, in this lesson, we will learn how to control digital display.

Components：

| ![image-20230421152421856](media/image-20230421152421856.png) | ![image-20230421152426184](media/image-20230421152426184.png) | ![image-20230421152429512](media/image-20230421152429512.png) | ![image-20230421152432792](media/image-20230421152432792.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230421152437321](media/image-20230421152437321.png) | ![image-20230421152442888](media/image-20230421152442888.png) | ![image-20230421152446376](media/image-20230421152446376.png) |                                                              |
| 1-digit 7-seg LED*1                                          | 220ΩResistor*8                                               | Jumper Wires                                                 |                                                              |



Component Knowledge：

**LED display：**

LED segment display is a semiconductor light-emitting device. Its basic unit is a light-emitting diode (LED).

For the common anode display, connect the common anode (COM) to +5V. When the cathode level of a certain segment is low, the segment is on; when the cathode level of a certain segment is high, the segment is off.

For the common cathode display, connect the common cathode (COM) to GND. When the anode level of a certain segment is high, the segment is on; when the anode level of a certain segment is low, the segment is off.

Each segment of the display consists of an LED. So when you use it, you also need to use a current-limiting resistor. Otherwise, LED will be burnt out.

When using 1-digit 7-segment display please notice that if it is common anode, the common anode pin connects to the power source; if it is common cathode, the common cathode pin connects to the GND.

Each of the LEDs in the display is given a positional segment with one of its connection pins led out from the rectangular plastic package. These LED pins are labeled from “a” through to “g” representing each individual LED.

**Below is the seven-segment pin diagram.**

![](media/92ec4bc2d10f37ebf330be7fd8a5039a.png)

Schematic Diagram：

![](media/39b141d4edac1d530838bc7866b18272.png)

![](media/158db67c75e043234a73bad906dfdb87.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 10_one-digital-LED.py

Test Result：

LED display shows0\~9，in loop way.

Note: Press Ctrl + C on keyboard to exit code runningExample Code：

Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep

#led pin
a = 23
b = 18
c = 6
d = 13
e = 19
f = 24
g = 25
dp = 5

GPIO.setmode(GPIO.BCM)  #use BCM numbers
#set the Pin OUTPUT mode
GPIO.setup(a,GPIO.OUT)  
GPIO.setup(b,GPIO.OUT)  
GPIO.setup(c,GPIO.OUT)  
GPIO.setup(d,GPIO.OUT)  
GPIO.setup(e,GPIO.OUT)  
GPIO.setup(f,GPIO.OUT)  
GPIO.setup(g,GPIO.OUT)  
GPIO.setup(dp,GPIO.OUT)  

#display 0
def d_0():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.HIGH)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.LOW)
    GPIO.output(dp,GPIO.LOW)
def d_1():  # display 1
    GPIO.output(a,GPIO.LOW)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.LOW)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.LOW)
    GPIO.output(g,GPIO.LOW)
    GPIO.output(dp,GPIO.LOW)
def d_2():  # display 2
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.LOW)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.HIGH)
    GPIO.output(f,GPIO.LOW)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_3():  # display 4
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.LOW)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_4():
    GPIO.output(a,GPIO.LOW)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.LOW)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_5():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.LOW)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_6():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.LOW)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.HIGH)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_7():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.LOW)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.LOW)
    GPIO.output(g,GPIO.LOW)
    GPIO.output(dp,GPIO.LOW)
def d_8():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.HIGH)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_9():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)

print("test...")
while True:
    d_0()  #Call function showing 0
    sleep(1) #delay 1s
    d_1()
    sleep(1)
    d_2()
    sleep(1)
    d_3()
    sleep(1)
    d_4()
    sleep(1)
    d_5()
    sleep(1)
    d_6()
    sleep(1)
    d_7()
    sleep(1)
    d_8()
    sleep(1)
    d_9()
    sleep(1)

GPIO.cleanup()  #release all GPIO
```



### Project 11：4-Digit Segment LED Display

Description：

In previous lesson, the LED display only shows 1 digit number, whereas, we could try to operate 4-digit segment LED display.

Components：

| ![image-20230421152605103](media/image-20230421152605103.png) | ![image-20230421152608687](media/image-20230421152608687.png) | ![image-20230421152612451](media/image-20230421152612451.png) | ![image-20230421152622526](media/image-20230421152622526.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230421152627421](media/image-20230421152627421.png) | ![image-20230421152640292](media/image-20230421152640292.png) | ![image-20230421152647836](media/image-20230421152647836.png) |                                                              |
| 4-digit 7-seg LED*1                                          | 220Ω Resistor*8                                              | Jumper Wires                                                 |                                                              |



Component Knowledge

**digit LED display:**

The 4-digit LED display is divided into common anode and common cathode. Similar to 1-digit segment LED display, it is controlled display segment by 8 GPIO ports(8 LED lights). However, this is 4 digit display, 4 GPIO ports are required to control the bit selection terminal.

Ours is common cathode

4-digit LED Display Pinout

Pin 1, 2, 3 and 4 are control pin of control bit

![](media/fca69e08fa315b81ccb1c6105f8fd28c.png)

**Schematic Diagram**

![](media/ea75d1b7414bf6f8c187fb32fea9bc83.png)



![](media/ffb32bb47a0af62c21b9f77de90af93e.png)

![](media/15c8eee5e555dfc413f34b7ecf16fab2.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 11_four-digital-LED.py

Test Result：

4-digit LED display firstly shows“0000”, then plus 1 every time until it reaches“9999”, however, when “9999” adds 1, the value changes into“0000”.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
-*- coding:utf-8 -*-

import RPi.GPIO as GPIO
from time import sleep
from threading import Timer  #Library files for introducing timers

d_num = 0
b_num = 0
#Pin of each section of nixie tube
a = 24
b = 18
c = 6
d = 19
e = 26
f = 23
g = 5
dp = 13
#Pin of each digit of nixie tube
d1 = 4
d2 = 17
d3 = 27
d4 = 22

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)
#set as output
GPIO.setup(a,GPIO.OUT)  
GPIO.setup(b,GPIO.OUT)  
GPIO.setup(c,GPIO.OUT)  
GPIO.setup(d,GPIO.OUT)  
GPIO.setup(e,GPIO.OUT)  
GPIO.setup(f,GPIO.OUT)  
GPIO.setup(g,GPIO.OUT)  
GPIO.setup(dp,GPIO.OUT)  
#set as output
GPIO.setup(d1,GPIO.OUT)  
GPIO.setup(d2,GPIO.OUT)  
GPIO.setup(d3,GPIO.OUT)  
GPIO.setup(d4,GPIO.OUT)  

#Set to high level, turn off the nixie tube
GPIO.output(d1,GPIO.HIGH)
GPIO.output(d2,GPIO.HIGH)
GPIO.output(d3,GPIO.HIGH)
GPIO.output(d4,GPIO.HIGH)

def d_0():  #display 0
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.HIGH)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.LOW)
    GPIO.output(dp,GPIO.LOW)
def d_1(): #display 1
    GPIO.output(a,GPIO.LOW)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.LOW)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.LOW)
    GPIO.output(g,GPIO.LOW)
    GPIO.output(dp,GPIO.LOW)
def d_2(): #display 2
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.LOW)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.HIGH)
    GPIO.output(f,GPIO.LOW)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_3():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.LOW)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_4():
    GPIO.output(a,GPIO.LOW)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.LOW)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_5():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.LOW)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_6():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.LOW)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.HIGH)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_7():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.LOW)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.LOW)
    GPIO.output(g,GPIO.LOW)
    GPIO.output(dp,GPIO.LOW)
def d_8():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.HIGH)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)
def d_9():
    GPIO.output(a,GPIO.HIGH)
    GPIO.output(b,GPIO.HIGH)
    GPIO.output(c,GPIO.HIGH)
    GPIO.output(d,GPIO.HIGH)
    GPIO.output(e,GPIO.LOW)
    GPIO.output(f,GPIO.HIGH)
    GPIO.output(g,GPIO.HIGH)
    GPIO.output(dp,GPIO.LOW)

def b_show(bit):   #Choose which digital tube to turn on
    #Choose to activate the single-digit digital tube, 
    #which is the right-most digit of the 4-digit digital tube
    if(bit == 0):
        GPIO.output(d1,GPIO.LOW)
        GPIO.output(d2,GPIO.HIGH)
        GPIO.output(d3,GPIO.HIGH)
        GPIO.output(d4,GPIO.HIGH)
    if(bit == 1):   #Select the start digit digital tube
        GPIO.output(d1,GPIO.HIGH)
        GPIO.output(d2,GPIO.LOW)
        GPIO.output(d3,GPIO.HIGH)
        GPIO.output(d4,GPIO.HIGH)
    if(bit == 2):   #Select the digital tube that activates the hundreds digit number
        GPIO.output(d1,GPIO.HIGH)
        GPIO.output(d2,GPIO.HIGH)
        GPIO.output(d3,GPIO.LOW)
        GPIO.output(d4,GPIO.HIGH)
    if(bit == 3):   #Select the digital tube to activate thousands of digits
        GPIO.output(d1,GPIO.HIGH)
        GPIO.output(d2,GPIO.HIGH)
        GPIO.output(d3,GPIO.HIGH)
        GPIO.output(d4,GPIO.LOW)

def recongnition(num):
    if(num == 0):  #num = 0
        d_0()      #Call d_0() to display 0 on the digital tube
    if(num == 1):
        d_1()
    if(num == 2):
        d_2()
    if(num == 3):
        d_3()
    if(num == 4):
        d_4()
    if(num == 5):
        d_5()
    if(num == 6):
        d_6()
    if(num == 7):
        d_7()
    if(num == 8):
        d_8()
    if(num == 9):
        d_9()
        
def display():
    global b_num
    if(b_num == 0):  #The ones place, the one on the far right of the 4-digit digital tube
        ge = d_num%10 # So % is the cooperations, so for example, 1356%10 = 6, so you get the units digit of 1356
        recongnition(ge) #This function, called recongnition(), is the number displayed around the digital tube, at d_num=1356, which is 6
        b_show(0)  #Call the function b_show(), which controls the nibbit, so that the units digit is the rightmost digit that can be lit
    if(b_num == 1):  #ten
        shi = d_num%100 #I'm going to subtract the hundreds place，1356 % 100 = 56
        shi = shi/10  # 56 / 10 = 5 ，You get ten digits
        recongnition(shi)
        b_show(1)  #Enable the ten digit digital tube to be lit
    if(b_num == 2): #A one hundred - bit
        bai = d_num%1000  #Let's leave out the thousands first, for example：1356 % 1000 = 356 ，So we get rid of the 1
        bai = bai/100     #Then,356 / 100 = 3，The integers are equal to 3, so you get the hundreds
        recongnition(bai)
        b_show(2)  #So that the hundreds digit digital tube can be lit
    if(b_num == 3): #A one thousand - bit
        qian = d_num/1000 # 1356 / 1000 = 1 ，We get thousands
        recongnition(qian)
        b_show(3)  #So that the digital tube in the thousands can be lit
    b_num = b_num + 1  #b_num add 1，In order to show you all the numbers
    if(b_num >3): #Since the digital tube is four bits, the limit cannot be greater than three
        b_num = 0 #Greater than 3 is equal to 0
    t = Timer(timer_interval,display) #
    t.start()

timer_interval = 0.005   #Start the timer interrupt every 0.005 seconds
t = Timer(timer_interval,display)  #Timer() is the Timer function, which means display is executed every 0.005s
t.start() #On timer

print("test...")
while True:
    for num in range(0,10000):  #display 0~10000
        d_num = num  #num = d_num
        print(d_num) #Terminal print out : d_num
        sleep(1)  #delay 1s

GPIO.cleanup() #release all GPIO
```



Explanation：

**from threading import Timer**

Import Timer from“threading” start() enables“Timer”, cancel() means stopping“Timer”

**t = Timer(timer_interval,display)**

This is a timer“t”，timer_interval is the time interval of triggering timer function, for instance, timer_interval = 0.005，that means trigger”display”function each 0.005s



Threading module library:

 <https://docs.python.org/3/library/threading.html>



### Project 12：8*8 Dot Matrix

Description：

In this chapter, let’s get down with a 8x8 LED dot matrix

Components：

| ![image-20230421153024822](media/image-20230421153024822.png) | ![image-20230421153028518](media/image-20230421153028518.png) | ![image-20230421153032365](media/image-20230421153032365.png) | ![image-20230421153036255](media/image-20230421153036255.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230421153047551](media/image-20230421153047551.png) | ![image-20230421153051905](media/image-20230421153051905.png) | ![image-20230421153055260](media/image-20230421153055260.png) |                                                              |
| 8\*8 LED Matrix\*1                                           | 220Ω Dot Matrix*8                                            | Jumper Wires                                                 |                                                              |



Component Knowledge

**8\*8 LED Matrix：**

8×8 matrix consists of 64 dots or pixels. There is a LED for each pixel and these LEDs are connected to total of 16 pins.

Generally, there are two types of dot matrix – common cathode and common anode.

![](media/69c719a7898907ab32f089f0cbbaff13.png)

Pic 1

![](media/bcfa2498367eaf9c7733da15af32eae7.png)

Pic 2

Schematic Diagram：

![](media/f4db95b367ac12e35c2f8ccd8ce28070.png)

![](media/4ede649bb46acce5d88013522065aa70.png)

Working Principle：

8\*8 is composed of LEDs. It will turn on if the positive is high level and negative is low level.

For the above figure, the first LED will be on if setting Y0(0) to HIGH and the rest of pins to LOW, X0(A) to LOW and the rest one to HIGH.

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 12_Matrix-LED.py

Test Result：

The dot on 8\*8 dot matrix module gradually turns on until to full screen and then off.

Note: Press Ctrl + C on keyboard to exit code runningExample Code：

Example Code：

```python
-*- coding:utf-8 -*-

import RPi.GPIO as GPIO
from time import sleep

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

#Define the pin of the row
row1 = 27
row2 = 4
row3 = 5
row4 = 17
row5 = 26
row6 = 6
row7 = 19
row8 = 13
#Define the pins of the column
col1 = 24
col2 = 16
col3 = 20
col4 = 18
col5 = 21
col6 = 23
col7 = 25
col8 = 12

#Set to output
GPIO.setup(row1,GPIO.OUT)
GPIO.setup(row2,GPIO.OUT)
GPIO.setup(row3,GPIO.OUT)
GPIO.setup(row4,GPIO.OUT)
GPIO.setup(row5,GPIO.OUT)
GPIO.setup(row6,GPIO.OUT)
GPIO.setup(row7,GPIO.OUT)
GPIO.setup(row8,GPIO.OUT)

GPIO.setup(col1,GPIO.OUT)
GPIO.setup(col2,GPIO.OUT)
GPIO.setup(col3,GPIO.OUT)
GPIO.setup(col4,GPIO.OUT)
GPIO.setup(col5,GPIO.OUT)
GPIO.setup(col6,GPIO.OUT)
GPIO.setup(col7,GPIO.OUT)
GPIO.setup(col8,GPIO.OUT)

#Sets the pin of the column to low level
GPIO.output(col1,GPIO.LOW)
GPIO.output(col2,GPIO.LOW)
GPIO.output(col3,GPIO.LOW)
GPIO.output(col4,GPIO.LOW)
GPIO.output(col5,GPIO.LOW)
GPIO.output(col6,GPIO.LOW)
GPIO.output(col7,GPIO.LOW)
GPIO.output(col8,GPIO.LOW)

#Since the column of the lattice has been set to low level, 
#the corresponding row of the lattice will light up when the pin of the row is at high level
def Row(d):
    if(d ==1):
        GPIO.output(row1,GPIO.HIGH)  #Light the first line
    if(d ==2):
        GPIO.output(row2,GPIO.HIGH)  #Light the second line
    if(d ==3):
        GPIO.output(row3,GPIO.HIGH)
    if(d ==4):
        GPIO.output(row4,GPIO.HIGH)
    if(d ==5):
        GPIO.output(row5,GPIO.HIGH)
    if(d ==6):
        GPIO.output(row6,GPIO.HIGH)
    if(d ==7):
        GPIO.output(row7,GPIO.HIGH)
    if(d ==8):
        GPIO.output(row8,GPIO.HIGH)
    
#Close the lattice
def off(): 
    GPIO.output(row1,GPIO.LOW)
    GPIO.output(row2,GPIO.LOW)
    GPIO.output(row3,GPIO.LOW)
    GPIO.output(row4,GPIO.LOW)
    GPIO.output(row5,GPIO.LOW)
    GPIO.output(row6,GPIO.LOW)
    GPIO.output(row7,GPIO.LOW)
    GPIO.output(row8,GPIO.LOW)

print("test...")
while True:
    for num in range(1,10):  #Light the lattice line by line
        Row(num)
        if(num == 9):  #Because the lattice has only 8 rows, and I'm limiting it here, is equal to 9
            off()      #Close the lattice
        sleep(0.2)

GPIO.cleanup()  #Release all GPIO ports
```



### Project 13：74HC595

Description：

In previous lesson, we control a 1-digit LED display with eight, which is wasteful. We need to figure out a method to save the use of GPIO ports. In fact, we need a 74HC595 CHIP.

Components：

| ![image-20230421153219888](media/image-20230421153219888.png) | ![image-20230421153225565](media/image-20230421153225565.png) | ![image-20230421153228430](media/image-20230421153228430.png) | ![image-20230421153231520](media/image-20230421153231520.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230421153240590](media/image-20230421153240590.png) | ![image-20230421153245133](media/image-20230421153245133.png) | ![image-20230421153248061](media/image-20230421153248061.png) | ![image-20230421153251470](media/image-20230421153251470.png) |
| 1-digit 7- seg LED*1                                         | 220Ω Resistor*8                                              | 74HC595N*1                                                   | Jumper Wires                                                 |



Component Knowledge

**74HC595**：

The 74HC595 consists of an 8−bit shift register and an 8−bit D−type latch with three−state parallel outputs. The shift register accepts serial data and provides a serial output. The shift register also provides parallel data to the 8−bit latch.  

The shift register and latch have independent clock inputs. This device also has an asynchronous reset for the shift register.

![](media/37c66aae4e707278592c6c5d5c5abfab.png)

74HC595 Control Protocol

| PIN         | FUNCTION                                                     |
| ----------- | ------------------------------------------------------------ |
| 13 PIN OE   | Enable pin, not controlled by program when high level<br />make it connect to GND when low level |
| 14 PIN SI   | This is pin receiving data, enter a bit each time and compose a byte if inputting eight times |
| 10 PIN SCLK | Shift register clear pin, used to clear out all data in shift register.<br />When low level, data will be cleared out. |
| 11 PIN SCK  | Clock pin of shift register, <br />the data inside will move backward and receive the data input when it is on rising edge. |
| 12 PIN RCK  | Clock input pin of latch register, data from shift register will saved in latch register when it is on rising edge. <br />The data will be output from QA\~QH |
| 9 Pin SQH   | Cascade pin，connected to multiple 74HC595 chips             |

More details about 74HC595 chip, you could look through chip specification folder.

Schematic Diagram：

![](media/217d295bf815c6bfaba5c8085f308068.png)

![](media/62d25dd7c6a68579dba763b53d97fba8.png)

The output end QA~QH of 74HC595 respond to the pin DP, and g~a.

Why? Since the binary is counted from the right, programming will be convenient. For example, 1-digit display shows 0011 1111 , the first bit is 1 which equals to QA saved in 74HC595, then when the rest numbers are sent to 74HC595, 1 will be pushed to QH, and last bit 0 is placed on QA. 

However, the wiring is so inverse that the first bit of binary corresponds to a and last one to DIP controlling 1-digit display.

| 74HC595 |    |    |    |    |    |    |    |    |         |
|---------|----|----|----|----|----|----|----|----|---------|
|         | QH | QG | QF | QE | QD | QC | QB | QA |         |
|         | a  | b  | c  | d  | e  | f  | g  | dp |         |
| **0**   | 1  | 1  | 1  | 1  | 1  | 1  | 0  | 0  | **252** |
| **1**   | 0  | 1  | 1  | 0  | 0  | 0  | 0  | 0  | **96**  |
| **2**   | 1  | 1  | 0  | 1  | 1  | 0  | 1  | 0  | **218** |
| **3**   | 1  | 1  | 1  | 1  | 0  | 0  | 1  | 0  | **242** |
| **4**   | 0  | 1  | 1  | 0  | 0  | 1  | 1  | 0  | **102** |
| **5**   | 1  | 0  | 1  | 1  | 0  | 1  | 1  | 0  | **182** |
| **6**   | 1  | 0  | 1  | 1  | 1  | 1  | 1  | 0  | **190** |
| **7**   | 1  | 1  | 1  | 0  | 0  | 0  | 0  | 0  | **224** |
| **8**   | 1  | 1  | 1  | 1  | 1  | 1  | 1  | 0  | **254** |
| **9**   | 1  | 1  | 1  | 1  | 0  | 1  | 1  | 0  | **246** |

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 13_74HC595.py

Test Result：

1-digit seven segment display shows 0\~9

Note: Press Ctrl + C on keyboard to exit code runningExample Code：

Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep

#define 74Hc595 pin
data = 17  #Serial digital input pin
rck = 27
sck = 22

#These hexadecimal numbers show data from 0 to 9
#Hexadecimal to binary,0x3F, 0011 1111
num = [0x3F, 0x06, 0x5B, 0x4F, 0x66, 0x6D, \
       0x7D, 0x07, 0x7F, 0x6F]

GPIO.setmode(GPIO.BCM)   #use BCM numbers
#set the 74HC595 Pin OUTPUT mode
GPIO.setup(data,GPIO.OUT)  
GPIO.setup(rck,GPIO.OUT)  
GPIO.setup(sck,GPIO.OUT)
#Set rck and sck to high first
GPIO.output(rck,GPIO.HIGH)
GPIO.output(sck,GPIO.HIGH)

def bitshift(dat):
    if dat == 0:
        da = num[0]
    if dat == 1:
        da = num[1]
    if dat == 2:
        da = num[2]
    if dat == 3:
        da = num[3]
    if dat == 4:
        da = num[4]
    if dat == 5:
        da = num[5]
    if dat == 6:
        da = num[6]
    if dat == 7:
        da = num[7]
    if dat == 8:
        da = num[8]
    if dat == 9:
        da = num[9]
    for a in range(0,8):
        GPIO.output(sck,GPIO.LOW)  #set sckPin LOW 
        if (da & 0x01) == 0x01:    #Judge whether the last bit is 1
            GPIO.output(data,GPIO.HIGH)  #1
        else:
            GPIO.output(data,GPIO.LOW)   #0
            #set sckPin HIGH , Move data to shift register
        GPIO.output(sck,GPIO.HIGH)
        #Move data one bit to the right
        da =da  >> 1

def display(num):
    #Clock pin of storage register is set to low level
    GPIO.output(rck,GPIO.LOW)
    #function, receive data
    bitshift(num)
    #Clock pin of storage register is set to high level
    #At this time, the data will be output from the Q0 ~ Q7 port
    GPIO.output(rck,GPIO.HIGH)

print("test...")
while True:
    for a in range(0,10):  #display 0~9
        display(a)
        sleep(1)
        
GPIO.cleanup()
```



### Project 14：Button-controlled LED

Description：

Usually, a complete open loop control is made of external information input. Controller and actuator.

The external information is input into controller which can analyze the input data and send to control signals to make actuator to react.

![](media/ebb6bb8058377aa3715096f9296c8e07.png)

A button-controlled LED is decided by an open loop control. Next, we will make a desk lamp with a button, an LED and RPi. LED is on when button is pressed, on the contrary, it will be off.

Components：

| ![image-20230421153655910](media/image-20230421153655910.png) | ![image-20230421153658849](media/image-20230421153658849.png) | ![image-20230421153702080](media/image-20230421153702080.png) | ![image-20230421153705041](media/image-20230421153705041.png) | ![image-20230421153708113](media/image-20230421153708113.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 | LED - Red *1                                                 |
| ![image-20230421153719937](media/image-20230421153719937.png) | ![image-20230421153723569](media/image-20230421153723569.png) | ![image-20230421153726753](media/image-20230421153726753.png) | ![image-20230421153729536](media/image-20230421153729536.png) |                                                              |
| 220Ω Resistor*1                                              | Jumper Wires                                                 | 10KΩ Resistor*1                                              | Button Switch *1                                             |                                                              |



Schematic Diagram：

![](media/56df70c171335f4e2432a1e1eb4bb4ab.png)

![](media/eb5b50bc4a31b3d370d9ddff64b452a9.png)

Eliminate Button Shaking

The LED status won’t jump into new state immediately when button is pressed. There will be a short continuous shaking before into new status, which is similar with release status.

![](media/ac2e8dbf544dd0c7a937ad3adaa5be5d.png)

Therefore, there will be many a presses and release actions. The shaking will misleads the high speed movement of MCU, causing wrong judgement. That requires that we need to judge the button’ status frequently.

The button means being pressed when its status is stable.

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 14_button_led.py

Test Result：

Press button, LED turns on, press again, LED is off.

Note: Press Ctrl + C on keyboard to exit code runningExample Code：

Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep

LED = 27  #set ledPin
button = 18 #set buttonPin
val = 0 #Button variables
count = 0 #Record the number of button presses
flag = 0 #Odd even variable
GPIO.setmode(GPIO.BCM)  # use BCM numbers

GPIO.setup(LED,GPIO.OUT)   #set the ledPin OUTPUT mode
GPIO.setup(button,GPIO.IN,GPIO.PUD_UP) #set the buttonPin INPUT mode and buttonPin to PULL UP

while True:
    val = GPIO.input(button)  #Receive button value
    #print("button = %d"%(val))
    if(val == 0):   #if button is pressed
        sleep(0.01) #Eliminate button jitter
        val = GPIO.input(button)  #Receive button value
        if(val == 1):  #Loosen the button
            count = count + 1  #Count the number of clicks on the button
            print("count = %d" %count)
    
    flag = count % 2  #Remainder 2 ,Even is 0, odd is 1
    if(flag == 1):
        GPIO.output(LED,GPIO.HIGH)  #turn on led
    else:
        GPIO.output(LED,GPIO.LOW)  #turn off led
        
GPIO.cleanup() #release all GPIO
```



### Project 15：Responder

Description：

A responder is someone who answers a question or who acts quickly in response to some event. In this lesson, we will show you how to make a responder and introduce its working principle.

Components：

| ![image-20230421153918444](media/image-20230421153918444.png) | ![image-20230421153923890](media/image-20230421153923890.png) | ![image-20230421153929729](media/image-20230421153929729.png) | ![image-20230421153933028](media/image-20230421153933028.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230421153942065](media/image-20230421153942065.png) | ![image-20230421153945985](media/image-20230421153945985.png) | ![image-20230421153949219](media/image-20230421153949219.png) | ![image-20230421153954530](media/image-20230421153954530.png) |
| LED - Red *1                                                 | LED - Green*1                                                | LED - Yellow*1                                               | Button Switch *4                                             |
| ![image-20230421154027714](media/image-20230421154027714.png) | ![image-20230421154032004](media/image-20230421154032004.png) | ![image-20230421154035266](media/image-20230421154035266.png) |                                                              |
| 220Ω Resistor*3                                              | Jumper Wires                                                 | 10KΩ Resistor*4                                              |                                                              |



Schematic Diagram：

![](media/843984784bbd495aa7484c0372339f17.png)

![](media/a392d5e55d4eb2da49e56697610c781e.png)

Design Description：

You could assume a scene that three competitors in knowledge quiz.

Everyone has a responder and an LED. Corresponding LED will turn on if one presses his own responder, however, others’ won’t be on. 

What’s more, a questioner has a button to control their LEDs. After a round of game, LEDs are off, the quiz restarts.

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 15_Responder.py

Test Result：

The corresponding LED will turn on if a competitor press his own responder, but others’ are off. The questioner press a button to turn off their LEDs and restart a new round quiz.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep

led colour

red = 26 
yellow = 19
blue = 13

#set button pin
#Player's button
key1 = 23
key2 = 24
key3 = 25
#Button for the author
reset = 18  
flag = True  #One sign quantity for restriction, only one light can be on

GPIO.setmode(GPIO.BCM) #use BCM numbers
#set the led Pin OUTPUT mode
GPIO.setup(red,GPIO.OUT)  
GPIO.setup(yellow,GPIO.OUT)  
GPIO.setup(blue,GPIO.OUT)
#set the button pin INPUT mode and PUD_UP
GPIO.setup(key1,GPIO.IN,GPIO.PUD_UP)  
GPIO.setup(key2,GPIO.IN,GPIO.PUD_UP)  
GPIO.setup(key3,GPIO.IN,GPIO.PUD_UP)  
GPIO.setup(reset,GPIO.IN,GPIO.PUD_UP)  

while True:  #loop
    if not GPIO.input(key1) and flag == True:  #Judge if player 1's button is pressed
        GPIO.output(red,GPIO.HIGH)
        flag = False
    if not GPIO.input(key2) and flag == True:  #Judge if player 2's button is pressed
        GPIO.output(yellow,GPIO.HIGH)
        flag = False
    if not GPIO.input(key3) and flag == True:  #Judge if player 3's button is pressed
        GPIO.output(blue,GPIO.HIGH)
        flag = False
    if not GPIO.input(reset):  #The writer's button is pressed
        GPIO.output(red,GPIO.LOW)
        GPIO.output(yellow,GPIO.LOW)
        GPIO.output(blue,GPIO.LOW)
        flag = True

GPIO.cleanup()  #release all GPIO
```



### Project 16：PIR Motion Sensor

Description：

In this lesson, we will learn about PIR motion sensor.

Components：

| ![image-20230421154225733](media/image-20230421154225733.png) | ![image-20230421154228292](media/image-20230421154228292.png) | ![image-20230421154231924](media/image-20230421154231924.png) | ![image-20230421154237331](media/image-20230421154237331.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230421154250310](media/image-20230421154250310.png) | ![image-20230421154301079](media/image-20230421154301079.png) | ![image-20230421154304741](media/image-20230421154304741.png) | ![image-20230421154308068](media/image-20230421154308068.png) |
| LED - Red *1                                                 | 220Ω Resistor*1                                              | PIR Motion Sensor*1                                          | Jumper Wires                                                 |



Component Knowledge

**PIR Motion Sensor：**

The principle of human infrared sensor is that when certain crystals, such as lithium tantalite and triglyceride sulfate, are heated, the two ends of the crystal will generate an equal number of charges, with opposite signs, which can be converted into voltage output by an amplifier.

Human body will emit IR ray, although weak but can be detected. Sensor will output high level(1) when human being is detected by sensor, otherwise, it will output low level o.

Note: Nothing but moving person can be detected, with the detection distance is up to 3m.

Schematic Diagram：

![](media/141d346dc2bd7d36c1478faff22908b6.png)

![](media/b0a265ba193a9879fb34c45f24ae9c4f.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 16_PIR-led.py

Test Result：

LED will turn on and terminal will print **somebody** if the PIR motion sensor detects people; if not, LED will be off and terminal will print **nobody.**

Note: Press Ctrl + C on keyboard to exit code running

Example Code

```python
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

ledPin = 5  #set led pin
pirPin = 18  #set PYE-IR pin
GPIO.setup(ledPin,GPIO.OUT)
GPIO.setup(pirPin,GPIO.IN)


while True:                     ##loop 
    if GPIO.input(pirPin):    #When someone is detected
        GPIO.output(ledPin,GPIO.HIGH)  #turn on the led
        print("somebody")
    else:
        GPIO.output(ledPin,GPIO.LOW)  #turn off led
        print("nobody")
    
GPIO.cleanup()
```



### Project 17：Fire Alarm

Description：

A flame detector is a sensor designed to detect and respond to the presence of a flame or fire, allowing flame detection.

Components：

| ![image-20230423080816522](media/image-20230423080816522.png) | ![image-20230423080822887](media/image-20230423080822887.png) | ![image-20230423080829063](media/image-20230423080829063.png) | ![image-20230423080832551](media/image-20230423080832551.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230423080842311](media/image-20230423080842311.png) | ![image-20230423080846615](media/image-20230423080846615.png) | ![image-20230423080850679](media/image-20230423080850679.png) | ![image-20230423080854023](media/image-20230423080854023.png) |
| Active Buzzer *1                                             | Flame Sensor *1                                              | 10KΩ Resistor*1                                              | Jumper Wires                                                 |



Component Knowledge

**Flame Sensor：**

Flame sensor is made based on the principle that infrared ray is highly sensitive to flame. It has an infrared receiving tube specially designed to detect fire, and then convert the flame brightness to fluctuating level signal. The signals are then input into the central processor and be dealt with accordingly.

Flame sensor is used to detect fire source with wavelength in 760nm～1100nm, detection angle is 60°. When its IR waves length is close to 940nm, and its sensitivity is highest.

Notice that keep flame sensor away from fire source to defend its damage for its working temperature is between -25°-85°

Schematic Diagram：

![](media/cf920e1d7db7c5905292baa2e01eb268.png)

![](media/fce67c08fbe3c0aa4a550d2859c7e58a.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 17_flame_buzzer.py

Test Result：

Buzzer will alarm when detecting fire; otherwise, it will stop emitting sound

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep

#define buzzer pin
buzPin = 27
#define flame Pin
flamePin = 18

val = 0  #

GPIO.setmode(GPIO.BCM) #use BCM numbers
GPIO.setup(buzPin,GPIO.OUT)  #set the buzPin OUTPUT
GPIO.setup(flamePin,GPIO.IN,GPIO.PUD_UP) #set the flamePin INPUT

while True:
    val = GPIO.input(flamePin) #Receives the value of the flame sensor
    print("val = %d" %val)
    if (val == 1):  #When flame is detected
        GPIO.output(buzPin,GPIO.HIGH)  #Buzzer turn on
    else:
        GPIO.output(buzPin,GPIO.LOW)   #buzzer turn off
        
GPIO.cleanup() # Release all GPIO
```



### Project 18：Electronic Hourglass

Description：

An hourglass (or sandglass, sand timer, sand clock or egg timer) is a device used to measure the passage of time. It comprises two glass bulbs connected vertically by a narrow neck that allows a regulated flow of a substance (historically sand) from the upper bulb to the lower one. 

Typically the upper and lower bulbs are symmetric so that the hourglass will measure the same duration regardless of orientation. The specific duration of time a given hourglass measures is determined by factors including the quantity and coarseness of the particulate matter, the bulb size, and the neck width.

Components：

| ![image-20230423081147152](media/image-20230423081147152.png) | ![image-20230423081154408](media/image-20230423081154408.png) | ![image-20230423081200825](media/image-20230423081200825.png) | ![image-20230423081207033](media/image-20230423081207033.png) | ![image-20230423081212585](media/image-20230423081212585.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 | LED - Red *2                                                 |
| ![image-20230423081218538](media/image-20230423081218538.png) | ![image-20230423081223785](media/image-20230423081223785.png) | ![image-20230423081227897](media/image-20230423081227897.png) | ![image-20230423081233690](media/image-20230423081233690.png) |                                                              |
| 220Ω Resistor*2                                              | Ball Tilt Sensor*1                                           | 10KΩ Resistor*1                                              | Jumper Wires                                                 |                                                              |



Component Knowledge

**Ball Tilt Sensor**：

Tilt sensors (tilt ball switch) allow you to detect orientation or inclination. They are small, inexpensive, low-power and easy-to-use. If used properly, they will not wear out.

The tilt-switch twig is the equivalent of a button, and is used as a digital input. Inside the tilt switch is a ball that make contact with the pins when the case is upright. Tilt the case over and the balls don't touch, thus not making a connection. When the switch is level it is open, and when tilted, the switch closes.

It can be used for orientation detection, alarm device or others.

Here is the principle of tilt sensor to illustrate how it works:

![](media/a589e5da5f5f91c3d16a4dded9e33cb1.png)

Schematic Diagram：

![](media/a811fe1c36aa601e9a48d3ada938c917.png)

![](media/749562134c34f33283faf8d1e4ba8f13.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 18_ball_Tilt.py

Test Result：

Led1 will brighten gradually and led2 will gradually darken the hourglass is placed; however, as you make it upside down, led1 will get darkens and led2 will get bright.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep

#define led pin
led1Pin = 17
led2Pin = 27
#define Ball Tilt Sensor Pin
tiltPin = 18


GPIO.setmode(GPIO.BCM) #use BCM unmbers
GPIO.setup(led1Pin,GPIO.OUT)  #set the ledPin OUTPUT mode
GPIO.setup(led2Pin,GPIO.OUT)
GPIO.output(led1Pin,GPIO.HIGH)  # make ledPin output HIGH level
GPIO.output(led2Pin,GPIO.LOW)  # make ledPin output LOW level
GPIO.setup(tiltPin,GPIO.IN,GPIO.PUD_UP)
pwm1 = GPIO.PWM(led1Pin,1000)  #create a pwm1 instance
pwm1.start(0)  #start pwm1
pwm2 = GPIO.PWM(led2Pin,1000)  #create a pwm2 instance
pwm2.start(0)  #start pwm2
val1 = 50
val2 = 50

while True:
    if not GPIO.input(tiltPin):
        val1 = val1 + 1
        val2 = val2 - 1
        if (val1 >= 100):  #Limit PWM value to no more than 100
            val1 = 100
        if (val2 < 0):    #Limit PWM value not less than 0
            val2 = 0
        print("led1 = %1.0f" %(val1))
        pwm1.ChangeDutyCycle(val1)  #change the frequency
        pwm2.ChangeDutyCycle(val2)
        sleep(0.1)
    else:
        val1 = val1 - 1
        val2 = val2 + 1
        if (val1 < 0):
            val1 = 0
        if (val2 >= 100):
            val2 = 100
        print("led2 = %1.0f" %(val2))
        pwm1.ChangeDutyCycle(val1)
        pwm2.ChangeDutyCycle(val2)
        sleep(0.1)
        
pwm1.stop()  #stop pwm1

GPIO.cleanup()    #release all GPIO
```



### Project 19：Stepless Dimming

Description：

A stepless dimming control method of a lighting system is applicable to the situations where a light source for a lighting terminal is a fluorescent lamp and/or an LED lamp.

Components：

| ![image-20230423081648180](media/image-20230423081648180.png) | ![image-20230423081652397](media/image-20230423081652397.png) | ![image-20230423081703876](media/image-20230423081703876.png) | ![image-20230423081711086](media/image-20230423081711086.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230423081716157](media/image-20230423081716157.png) | ![image-20230423081720430](media/image-20230423081720430.png) | ![image-20230423081723837](media/image-20230423081723837.png) |                                                              |
| Potentiometer*1                                              | PCF8591 A/D Converter Module*1                               | Jumper Wires                                                 |                                                              |



Component Knowledge

**PCF8591 A/D Converter Module：**

Raspberry Pi doesn’t come with AD/DA function. It has to be connected AD/DA shield if it is connected to analog sensor. We use pcf8591 AD/DA converter which adopts I2C communication. Therefore, the operation steps are shown below:

a. Enter sudo raspi-config and press “Enter” to navigate the configuration page.

![](media/2c8b4e4fce58dce6952d3bf59738cf1d.png)

b. Enable the I2C function according to the following pictures (press（↑）,（↓）,（←）,（→）on the keyboard and “Enter”k）

![](media/e00c383d371eb91380f7ae6eb6fb880e.png)

![](media/5857137609951026428431b4a82ad4d2.png)

![](media/f15f3a54b9f31c7cfc1fd4f8b4387c70.png)

You could check more detailS about I2C communication agreement in the following link:

<https://www.nxp.com/docs/en/user-guide/UM10204.pdf>

**PCF8591 Pins:**

More details about PCF8591 chip, you could look through chip specification folder.

From the below figure, PCF8591 has an analog output pin Aout and four analog input pin A0-A3.

![](media/0a7c25ac32deb42347f5450be7bc23bd.png)

Check the address of iic module（PCF8591）of Raspberry Pi, enter command i2cdetect -y 1 and press Enter.

The iic address of PCF8591 is 0x48.

![](media/6193784f9a6697876ca54844be38e3c0.png)

Used to read the address of pin A0\~A3.

The address of analog output pin AOUT: 0x40, that is, 64 converting from hexadecimal to decimal

A0 = 0x40 \#\#A0 ----\> port address

A1 = 0x41

A2 = 0x42

A3 = 0x43

**Adjustable Potentiometer**

The rotary potentiometer means the change of resistance.

We could convert the resistance’s change into the voltage’s when setting circuit. Then, voltage changes will be output to GPIO port through module signals.

Wiring according to the below figure and rotate clockwise, resistance value reduces.

Schematic Diagram：

![](media/87f632c39b0360057fa161c3ae5e1c8f.png)

![](media/7b2a25854307f0d399f770f5723fe8e1.png)

Note: PCF8591 module comes with an LED connected to Aout pint

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 19_potentiometer-LED.py

Test Result：

Terminal prints the analog value read by adjustable potentiometer. The LED brightness will vary with the the rotary of potentiometer.

Note: Press Ctrl + C on keyboard to exit code runningExample Code：

Example Code：

```python
import smbus
import time
address = 0x48 #default address of PCF8591
bus=smbus.SMBus(1)  #Create an instance of smbus
cmd=0x40 #command

A0 = 0x40      ##A0  ----> port address

A1 = 0x41

A2 = 0x42

A3 = 0x43

def analogRead(chn):   #read ADC value,chn:0,1,2,3
    value = bus.read_byte_data(address,cmd+chn)
    return value

def analogWrite(value):#write DAC value
    bus.write_byte_data(address,cmd,value) 

def loop():
    while True:
        value = analogRead(0) #read the ADC value ofchannel 0
        analogWrite(value) #write the DAC value
        voltage = value / 255.0 * 3.3 #calculate the voltage value
        print ('ADC Value : %d, Voltage : %.2f'%(value,voltage))
        time.sleep(0.01)

def destroy():
    bus.close()

if __name__ == '__main__':
    print ('Program is starting ... ')
    try:
        loop()
    except KeyboardInterrupt:
        destroy()
```



Explanation：

**smbus**

Smbus is based on iic communication. We treat it as iic communication library.

**bus.read_byte_data(address,cmd+chn)**

Read the corresponding modules with iic address，address is the address of pcf8591 module, cmd+chn correspond to the address of analog port pcf8591: A0 = 0x40，A1 = 0x41，A2 = 0x42，A3 = 0x43

**bus.write_byte_data(address,cmd,value)**

D/A analog value outputs, address is address of pcf8591 module, cmd outputs the address of pins, value: output value



**Smbus library file**: https://pypi.org/project/smbus2/0.1.2/



### Project 20：Photoresistor

Description：

Photo resistor (Photovaristor) is a resistor whose resistance varies according to different incident light strength. It's made based on the photoelectric effect of semiconductor. In this lesson, let’s explain how it works.

Components：

| ![image-20230423082128587](media/image-20230423082128587.png) | ![image-20230423082132545](media/image-20230423082132545.png) | ![image-20230423082138273](media/image-20230423082138273.png) | ![image-20230423082141841](media/image-20230423082141841.png) | ![image-20230423082148898](media/image-20230423082148898.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 | LED - Red *1                                                 |
| ![image-20230423082201331](media/image-20230423082201331.png) | ![image-20230423082208882](media/image-20230423082208882.png) | ![image-20230423082213361](media/image-20230423082213361.png) | ![image-20230423082217457](media/image-20230423082217457.png) | ![image-20230423082221201](media/image-20230423082221201.png) |
| 220Ω Resistor*1                                              | Photo Resistor*1                                             | 10KΩ Resistor*1                                              | PCF8591 A/D Converter Module*1                               | Jumper Wires                                                 |



Component Knowledge

**Photoresistor：**

Photo resistor (Photovaristor) is a resistor whose resistance varies according to different incident light strength. It's made based on the photoelectric effect of semiconductor. If the incident light is intense, its resistance reduces; if the incident light is weak, the resistance increases.

If incident light on a photoresistor exceeds a certain frequency, photons absorbed by the semiconductor give bound electrons enough energy to jump into the conduction band. The resulting free electrons (and their hole partners) conduct electricity, thereby lowering resistance.

Schematic Diagram：

![](media/62d7ded39ba13d8789248e93165013ae.png)

![](media/b92c4cb38844f1ee074779eae270d650.png)

Run Example Code：

Note: in the experiment, I2C communication is used. We need to check the iic address first (enter command: i2cdetect -y 1 and press “Enter”. If failed, check the wiring is correct or not. If correct, you need to enable I2C communication function of Raspberry Pi, project 19 is for your reference.

After enabling I2C communication, input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 20_photo-resistor.py

Test Result：

Terminal prints the value tested by photoresistor. LED will turn on if the ambient environment is dim; otherwise, LED will be off.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
import smbus   
import time

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

led = 5
GPIO.setup(led,GPIO.OUT)

address = 0x48 ##address  ---> device address
cmd = 0x40     ##DA converter command
A0 = 0x40      ##A0  ----> port address
A1 = 0x41
A2 = 0x42
A3 = 0x43
bus = smbus.SMBus(1)            ##start the bus

def analogRead(count):   #function,read analog data
    read_val = bus.read_byte_data(address,cmd+count)
    return read_val

while True:                     ##loop 
    #Vout = 10                  ##10*0.0196=0.196V
    #bus.write_byte_data(address,cmd,Vout) ##DA converter
    value = analogRead(0) ##read A0 data
    if(value<80):   #When the ambient brightness is less than 80, the LED light will be on
        GPIO.output(led,GPIO.HIGH)
    else:
        GPIO.output(led,GPIO.LOW)

    print("data:%1.0f" %(value))   ##print data

time.sleep(0.5)                ##delay 0.5 second
GPIO.cleanup()
```



### Project 21：Sound-activated Light

Description：

You might find the lights automatically on when you pass them, nevertheless they will be off if the surrounding is quiet. Do you know why?

Actually, it is sound sensor that controls them on and off.

Components:

| ![image-20230423082502613](media/image-20230423082502613.png) | ![image-20230423082506691](media/image-20230423082506691.png) | ![image-20230423082510277](media/image-20230423082510277.png) | ![image-20230423082514179](media/image-20230423082514179.png) | ![image-20230423082517860](media/image-20230423082517860.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 | LED - Red *1                                                 |
| ![image-20230423082522884](media/image-20230423082522884.png) | ![image-20230423082526563](media/image-20230423082526563.png) | ![image-20230423082534085](media/image-20230423082534085.png) | ![image-20230423082538084](media/image-20230423082538084.png) |                                                              |
| 220Ω Resistor*1                                              | Sound Sensor*1                                               | Jumper Wires                                                 | PCF8591 A/D Converter Module*1                               |                                                              |



Component Knowledge

A sound sensor is defined as a module that detects sound waves through its intensity and converting it to electrical signals.

The sound sensor has a built-in capacitive electret microphone which is highly sensitive to sound. Sound waves cause the thin film of the electret to vibrate and then the capacitance changes, thus producing the corresponding changed voltage. Since the voltage change is extremely weak, it needs to be amplified. So it is converted into a voltage ranging from 0 to 5V, which is received by data acquisition unit after A/D adapter conversion and then sent to an MCU.

The module can be applied to noise monitoring in traffic artery, and detection of noises within the boundary of industrial enterprises, factories, and construction sites, detection of noises in urban regions, and noise detection and assessment of living surroundings. 

Schematic and Connection Diagram：

![](media/5d8a9db8a2ce59f8ffb251ab054a8bbe.png)

![](media/13628b82afe32eb71bc4c2b54cb8d294.png)

Run Example Code：

Note: in the experiment, I2C communication is used. We need to check the iic address first( enter command：i2cdetect -y 1 and press“Enter”.  If failed, check the wiring is correct or not. If correct, you need to enable I2C communication function of Raspberry Pi, project 19 is for your reference.

After enabling the I2C communication，input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 21_sound_led.py

Test Result：

When you clap your hands suddenly, LED lights up and clap again, LED is off.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
import smbus
import time

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

led = 5
GPIO.setup(led,GPIO.OUT)

address = 0x48 ##address  ---> device address
cmd = 0x40     ##DA converter command
A0 = 0x40      ##A0  ----> port address
A1 = 0x41
A2 = 0x42
A3 = 0x43
bus = smbus.SMBus(1)            ##start the bus

flag = 0
mode = 0

def analogRead(count):   #function,read analog data
    read_val = bus.read_byte_data(address,cmd+count)
    return read_val

while True:                     ##loop
    value = analogRead(0) ##read A0 data
    if(value>50):
        flag += 1
        mode = flag % 2
    if(mode == 0):
        GPIO.output(led,GPIO.LOW)
    else:
        GPIO.output(led,GPIO.HIGH)

    print("data:%1.0f" %(value))   ##print data
    time.sleep(0.05)                ##delay 0.05 second

GPIO.cleanup()
```



### Project 22：LCD1602 & MQ-2 Gas Leakage Alarm

Description：

Some households have access to gas, which is composed of CO, CO2, N2, H2 and CH4. CO is one of toxic gases. People will be in danger if absorbing too much CO. However, we could tackle with this problem over a gas leakage alarm.

Gas MQ-2 leakage alarm detects the presence of a combustible or toxic gas and react by displaying a reading, setting off an audible or visual alarm.

Components：

| ![image-20230423083536561](media/image-20230423083536561.png) | ![image-20230423083540203](media/image-20230423083540203.png) | ![image-20230423083546988](media/image-20230423083546988.png) | ![image-20230423083550682](media/image-20230423083550682.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230423083556810](media/image-20230423083556810.png) | ![image-20230423083600043](media/image-20230423083600043.png) | ![image-20230423083606266](media/image-20230423083606266.png) | ![image-20230423083609450](media/image-20230423083609450.png) |
| Potentiometer*1                                              | Active Buzzer *1                                             | Jumper Wires                                                 | M-F Dupont Line                                              |
| ![image-20230423083614491](media/image-20230423083614491.png) | ![image-20230423083617611](media/image-20230423083617611.png) | ![image-20230423083621035](media/image-20230423083621035.png) |                                                              |
| LCD1602 display*1                                            | Analog Gas MQ-2 Sensor * 1                                   | PCF8591 A/D Converter Module*1                               |                                                              |



Component Knowledge

MQ-2 gas sensor adopts the material sensitive to gas------SnO2 with low electricity conductivity. When beset with combustible gas, its electricity conductivity varies with the of the concentration of flammable gas, however, the simple circuit could convert the change of  electricity conductivity into the output signals of the concentration of gas sensor.

MQ-2 gas sensor is a multi-purpose and cost-effective. It can detect the concentration of flammable gas and smoke in the range of 300~10000ppm.Meanwhile, it has high sensitivity to natural gas, liquefied petroleum gas and other smoke, especially to alkanes smoke. 

**LCD1602 LED Display：**

It could show the characters or numbers in 16 rows and 2 columns

![](media/28f90ce528bf6fe3d6f1475ac055c3b5.png)

**1602 LCD Pins:**

| PIN       | FUNCTION                                                     |
| --------- | ------------------------------------------------------------ |
| Pin 1     | GND                                                          |
| Pin 2     | VCC is connected to positive of 5V                           |
| Pin 3     | V0 is the contrast adjustment terminal of LCD. <br />The contrast is the weakest when the positive power is connected, and the contrast is the highest when the power is grounded (for high contrast causing double image a 10K potentiometer can help adjust contrast during use) |
| Pin 4     | RS is register selection, select data register when high level 1 and choose command register when low level 0 |
| Pin 5     | RW is reading and writing signal line. <br />Reading operation actives if high level(1), writing operation actives ig low level(0) |
| Pin 6     | E(EN) is enable end, read information when high level(1), execute the command when low level(0) |
| Pin 7\~14 | D0～D7 are 8-bit two-way data ends                           |
| Pin 15    | Positive of backlight                                        |
| Pin 16    | Negative of backlight                                        |

LCD1602 usually uses eight data cable to provide the data of Data0\~Data7, however, it supports“4Bits”mode which is so called four data cables so as to save GPIO ports

Schematic Diagram：

![](media/f74a594c0359c12f0e7ed93641d6c65b.png)

![](media/9869034bfb6e61fcbd4f07fe2f770590.png)

Run Example Code：

Note: in the experiment, I2C communication is used. We need to check the iic address first( enter command：i2cdetect -y 1 and press“Enter”.  If failed, check the wiring is correct or not. If correct, you need to enable I2C communication function of Raspberry Pi, project 19 is for your reference.

After enabling the I2C communication，input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 22_LCD1602_MQ2.py

Test Result：

Buzzer alarms when detecting the poisonous gas.

Note: Press Ctrl + C on keyboard and exit code running.

Example Code：

```python
#!/usr/bin/python
#import
import RPi.GPIO as GPIO
import time
import smbus

Define GPIO to LCD mapping

LCD_RS = 19
LCD_E  = 13
LCD_D4 = 22
LCD_D5 = 27
LCD_D6 = 17
LCD_D7 = 4

Define some device constants

LCD_WIDTH = 16    # Maximum characters per line
LCD_CHR = True
LCD_CMD = False

LCD_LINE_1 = 0x80 # LCD RAM address for the 1st line
LCD_LINE_2 = 0xC0 # LCD RAM address for the 2nd line

Timing constants

E_PULSE = 0.0005
E_DELAY = 0.0005

#pcf8591
address=0x48
cmd=0x40
A0=0x40##A0---->port address
A1=0x41
A2=0x42
A3=0x43
bus=smbus.SMBus(1)

#buzzer
buzPin = 20  #set buzPin to 20
GPIO.setmode(GPIO.BCM) # use BCM numbers
GPIO.setup(buzPin,GPIO.OUT)  #set buzPin OUTPUT mode


def main():
    # Main program block
    GPIO.setwarnings(False)
    GPIO.setmode(GPIO.BCM)       # Use BCM GPIO numbers
    GPIO.setup(LCD_E, GPIO.OUT)  # E
    GPIO.setup(LCD_RS, GPIO.OUT) # RS
    GPIO.setup(LCD_D4, GPIO.OUT) # DB4
    GPIO.setup(LCD_D5, GPIO.OUT) # DB5
    GPIO.setup(LCD_D6, GPIO.OUT) # DB6
    GPIO.setup(LCD_D7, GPIO.OUT) # DB7
    

    # Initialise display
    lcd_init()
    
    while True:
        temp = analogRead(0)
        print("MQ-2 = %s"%(temp))
        #display
        # Send some test
        lcd_string("MQ-2",LCD_LINE_1)
        lcd_string(temp,LCD_LINE_2)
        time.sleep(0.1)

#LM35, require Temperature
def analogRead(count):
    read_val=bus.read_byte_data(address,cmd+count)
    if(read_val > 60):
        GPIO.output(buzPin,GPIO.HIGH)  #Buzzer ring
    else:
        GPIO.output(buzPin,GPIO.LOW)  #Buzzer stop

    mq2_val = str(read_val)  # int to string
    return mq2_val

 


def lcd_init():
    # Initialise display
    lcd_byte(0x33,LCD_CMD) # 110011 Initialise
    lcd_byte(0x32,LCD_CMD) # 110010 Initialise
    lcd_byte(0x06,LCD_CMD) # 000110 Cursor move direction
    lcd_byte(0x0C,LCD_CMD) # 001100 Display On,Cursor Off, Blink Off
    lcd_byte(0x28,LCD_CMD) # 101000 Data length, number of lines, font size
    lcd_byte(0x01,LCD_CMD) # 000001 Clear display
    time.sleep(E_DELAY)

def lcd_byte(bits, mode):
    # Send byte to data pins
    # bits = data
    # mode = True  for character
    #        False for command
    

    GPIO.output(LCD_RS, mode) # RS
    
    # High bits
    GPIO.output(LCD_D4, False)
    GPIO.output(LCD_D5, False)
    GPIO.output(LCD_D6, False)
    GPIO.output(LCD_D7, False)
    if bits&0x10==0x10:
        GPIO.output(LCD_D4, True)
    if bits&0x20==0x20:
        GPIO.output(LCD_D5, True)
    if bits&0x40==0x40:
        GPIO.output(LCD_D6, True)
    if bits&0x80==0x80:
        GPIO.output(LCD_D7, True)
    
    # Toggle 'Enable' pin
    lcd_toggle_enable()
    
    # Low bits
    GPIO.output(LCD_D4, False)
    GPIO.output(LCD_D5, False)
    GPIO.output(LCD_D6, False)
    GPIO.output(LCD_D7, False)
    if bits&0x01==0x01:
        GPIO.output(LCD_D4, True)
    if bits&0x02==0x02:
        GPIO.output(LCD_D5, True)
    if bits&0x04==0x04:
        GPIO.output(LCD_D6, True)
    if bits&0x08==0x08:
        GPIO.output(LCD_D7, True)
    
    # Toggle 'Enable' pin
    lcd_toggle_enable()

def lcd_toggle_enable():

    # Toggle enable

    time.sleep(E_DELAY)
    GPIO.output(LCD_E, True)
    time.sleep(E_PULSE)
    GPIO.output(LCD_E, False)
    time.sleep(E_DELAY)

def lcd_string(message,line):
    # Send string to display
    

    message = message.ljust(LCD_WIDTH," ")
    
    lcd_byte(line, LCD_CMD)
    
    for i in range(LCD_WIDTH):
        lcd_byte(ord(message[i]),LCD_CHR)

 


if __name__ == '__main__':

try:
    main()
except KeyboardInterrupt:
    pass
finally:
    lcd_byte(0x01, LCD_CMD)
    lcd_string("Goodbye!",LCD_LINE_1)
    GPIO.cleanup()
```



### Project 23：Water Level Monitor

Description：

If you have ever had a water heater explode or ever tried to make submersible electronics, then you know how important it is to detect when water is around. Let’s know more about water level sensor.

Components:

| ![image-20230423084909868](media/image-20230423084909868.png) | ![image-20230423084913349](media/image-20230423084913349.png) | ![image-20230423084916725](media/image-20230423084916725.png) | ![image-20230423084929061](media/image-20230423084929061.png) | ![image-20230423084933924](media/image-20230423084933924.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 | Active Buzzer *1                                             |
| ![image-20230423084945621](media/image-20230423084945621.png) | ![image-20230423084949094](media/image-20230423084949094.png) | ![image-20230423084952677](media/image-20230423084952677.png) | ![image-20230423084957637](media/image-20230423084957637.png) |                                                              |
| Water level sensor * 1                                       | PCF8591 A/D Converter Module*1                               | Jumper Wires                                                 | M-F Dupont Line                                              |                                                              |



Component Knowledge

**Water Level Sensor：**

Our water sensor is easy- to-use, portable and cost-effective, designed to identify and detect water level and water drop.

This sensor measures the volume of water drop and water quantity through an array of traces of exposed parallel wires.

It could convert water content to analog signals, and output analog value could be used by function of application. It has the features of low consumption as well.

Schematic and Connection Diagram：

![](media/d0b751b8110bac27f1aba11c1e8b7abe.png)
![](media/b7c0b634e88a8682a338a261c48eb0ab.png)

Run Example Code：

Note: in the experiment, I2C communication is used. We need to check the iic address first( enter command：i2cdetect -y 1 and press“Enter”. If failed, check the wiring is correct or not. If correct, you need to enable I2C communication function of Raspberry Pi, project 19 is for your reference.

After enabling the I2C communication，input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 23_water_buzzer.py

Test Result：

Buzzer makes a sound when water covering the exposed detection part.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
import smbus
import time

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

buz = 18
GPIO.setup(buz,GPIO.OUT)

address = 0x48 ##address  ---> device address
cmd = 0x40     ##DA converter command
A0 = 0x40      ##A0  ----> port address
A1 = 0x41
A2 = 0x42
A3 = 0x43
bus = smbus.SMBus(1)            ##start the bus


def analogRead(count):   #function,read analog data
    read_val = bus.read_byte_data(address,cmd+count)
    return read_val

while True:                     ##loop
    value = analogRead(0) ##read A0 data
    if(value>30):
        GPIO.output(buz,GPIO.HIGH)
    else:
        GPIO.output(buz,GPIO.LOW)

    print("data:%1.0f" %(value))   ##print data
    time.sleep(0.05)                ##delay 0.05 second

GPIO.cleanup()
```



### Project 24：5V Relay + Water Pump

Description：

From a safety perspective, we specially designed this relay module with NO (normally open) and NC (normally closed) terminals. In this lesson, we will learn a special and easy-to-use switch, which is the relay module. Use the relay to start the motor.

In daily life, the electronic device is driven by 220V AC and controlled by switch. People will be in danger once the electricity leakage happens, connecting switch to 220V AC directly.

Therefore, we design a relay module with NO and NC ends. Let’s get started.

Components：

| ![image-20230423085643467](media/image-20230423085643467.png) | ![image-20230423085647417](media/image-20230423085647417.png) | ![image-20230423085650697](media/image-20230423085650697.png) | ![image-20230423085654189](media/image-20230423085654189.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40pin Colorful Jumper Wires*1                                | Breadboard*1                                                 |
| ![image-20230423085659465](media/image-20230423085659465.png) | ![image-20230423085702985](media/image-20230423085702985.png) | ![image-20230423085707753](media/image-20230423085707753.png) |                                                              |
| Relay Module*1                                               | Water Pipe*1                                                 | Water Pump*1                                                 |                                                              |
| ![image-20230423085716379](media/image-20230423085716379.png) | ![image-20230423085719849](media/image-20230423085719849.png) | ![image-20230423085723066](media/image-20230423085723066.png) | ![image-20230423085726123](media/image-20230423085726123.png) |
| M-F Dupont Line                                              | 220Ω Resistor*1                                              | Screwdriver*1                                                | Jumper Wires                                                 |



Component Knowledge

Relay: It is an "automatic switch" that uses a small current to control the operation of a large current.

Control input voltage: 5V

Rated load: 5A 250VAC (NO/NC) 5A 24VDC (NO/NC)

**Water Pump**

-   Working voltage: DC3-5V,

-   Working current: 100-200mA,

-   Head: 0.3-0.8 meters,

-   Flow rate: 1.2-1.6L/min,

-   Weight: 28 grams

Schematic Diagram：

![](media/6662f0a4c7b034287e392d41ec762477.png)

![](media/6e4bbab19404629a90d8c2c64897b522.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 24_relay.py

Test Result：

Water pump activates when the indication on relay module turns on.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
from time import sleep

relayPin = 18   #define relay pin

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)
GPIO.setup(relayPin,GPIO.OUT)

while True:
	GPIO.output(relayPin,GPIO.HIGH)  #Starting relay
	print("turn on")
	sleep(5)
	GPIO.output(relayPin,GPIO.LOW)  #Close relay
	print("turn off")
	sleep(1)

GPIO.cleanup()
```



### Project 25：Watering Flower Device

Description：

The household plants are popular in many a communities. They will die if you forget to water them, how about making an automatic watering device?

Components：

| ![image-20230423085919841](media/image-20230423085919841.png) | ![image-20230423085923035](media/image-20230423085923035.png) | ![image-20230423085925900](media/image-20230423085925900.png) | ![image-20230423085929661](media/image-20230423085929661.png) | ![image-20230423085933627](media/image-20230423085933627.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 | Relay Module*1                                               |
| ![image-20230423085938140](media/image-20230423085938140.png) | ![image-20230423085941148](media/image-20230423085941148.png) | ![image-20230423085944700](media/image-20230423085944700.png) | ![image-20230423085948044](media/image-20230423085948044.png) | ![image-20230423085951037](media/image-20230423085951037.png) |
| Water Pump*1                                                 | Soil Humidity Sensor*1                                       | PCF8591 A/D Converter Module*1                               | 220Ω Resistor*1                                              | Water Pipe*1                                                 |
| ![image-20230423090012348](media/image-20230423090012348.png) | ![image-20230423090017325](media/image-20230423090017325.png) | ![image-20230423090020624](media/image-20230423090020624.png) |                                                              |                                                              |
| M-F Dupont Line                                              | Jumper Wires                                                 | Screwdriver*1                                                |                                                              |                                                              |



Component Knowledge

**Soil Humidity Sensor：**

This is a simple soil humidity sensor aims to detect the soil humidity. 

If the soil is in lack of water, the analog value output by the sensor will decrease; otherwise, it will increase. If you use this sensor to make an automatic watering device, it can detect whether your botany is thirsty to prevent it from withering when you go out. 

Using the sensor with controller makes your plant more comfortable and your garden smarter. The soil humidity sensor module is not as complicated as you might think, and if you need to detect the soil in your project, it will be your best choice.

Schematic Diagram：

![](media/ea4b4fce32b759da7b0ca14005920567.png)

![](media/6a9cb5f9734c007528532a6aafecfb79.png)

Run Example Code：

Note: in the experiment, I2C communication is used. We need to check the iic address first( enter command：i2cdetect -y 1 and press“Enter”. If failed, check the wiring is correct or not. If correct, you need to enable I2C communication function of Raspberry Pi, project 19 is for your reference.

After enabling the I2C communication，input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 25_soil.py

Test Result：

Water pump starts running when soil humidity sensor detects the drought of soil.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
import smbus   
import time

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

pumpPin = 18
GPIO.setup(pumpPin,GPIO.OUT)

address = 0x48 ##address  ---> device address
cmd = 0x40     ##DA converter command
A0 = 0x40      ##A0  ----> port address
A1 = 0x41
A2 = 0x42
A3 = 0x43
bus = smbus.SMBus(1)            ##start the bus
while True:                     ##loop 
    #Vout = 10                  ##10*0.0196=0.196V
    #bus.write_byte_data(address,cmd,Vout) ##DA converter
    bus.write_byte(address,A0)     ##which port of the device you want to access
    value = bus.read_byte(address) ##access the data
    if(value<30):    #When the soil moisture value is less than 50, turn on the relay to start the water pump
        GPIO.output(pumpPin,GPIO.HIGH)
    else:
        GPIO.output(pumpPin,GPIO.LOW)
    print("data:%1.0f" %(value))   ##print data
    
time.sleep(0.5)                ##delay 0.5 second
GPIO.cleanup()
```

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          

### Project 26：OLED Display

Description：

OLED display is the most commonly used for cellphone screen, thanks to its characteristics of high resolution, small-sized and high brightness.

Components：

| ![image-20230423090833627](media/image-20230423090833627.png) | ![image-20230423090837281](media/image-20230423090837281.png) | ![image-20230423090840034](media/image-20230423090840034.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230423090849362](media/image-20230423090849362.png) | ![KS0271](media/KS0271.png)                                  | ![image-20230423090856338](media/image-20230423090856338.png) |
| Breadboard*1                                                 | OLED Display*1                                               | Jumper Wires                                                 |



Component Knowledge

**OLED Display：**

-   Use SSD1306 chip to drive

-   Communication: IIC communication

-   Size: 0.96inch

-   Resolution: 128\*96

-   Display Color: Blue

Schematic Diagram：

![](media/a24a50c17ca27d35d2287305abdbd3dd.png)

![](media/oledjiexian.png)

Install Luma.oled Library：

**Input in terminal the following commands：**

sudo apt-get update

sudo apt-get install python3-dev python3-pip libfreetype6-dev libjpeg-dev

sudo -H pip3 install --upgrade pip

sudo apt-get purge python3-pip

sudo -H pip3 install --upgrade luma.oled

Run Example Code：

Note: in the experiment, I2C communication is used. We need to check the iic address first( enter command：i2cdetect -y 1 and press“Enter”. If failed, check the wiring is correct or not. If correct, you need to enable I2C communication function of Raspberry Pi, project 19 is for your reference.

After enabling the I2C communication，input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 26_oled.py

Test Result：

OLED displays “Hello world”.

Note: Press Ctrl + C on keyboard to exit code runningExample Code：

Example Code：

```python
from luma.core.interface.serial import i2c, spi
from luma.core.render import canvas
from luma.oled.device import ssd1306

#rev.1 users set port=0
#substitute spi(device=0, port=0) below if using that interface
serial = i2c(port=1, address=0x3C)

#substitute ssd1331(...) or sh1106(...) below if using that device
device = ssd1306(serial)  #change to ssd1306, ssd1325, ssd1331, sh1106

while(1):
	with canvas(device) as draw:
		draw.rectangle(device.bounding_box, outline="white", fill="black")
		draw.text((30, 40), "Hello World", fill="white")
```

More luma.oled Example：

Run the example in luma.examples

Terminal Running：

Install needed environment:

sudo usermod -a -G i2c,spi,gpio pi

sudo apt install python-dev python-pip libfreetype6-dev libjpeg-dev build-essential

sudo apt install libsdl-dev libportmidi-dev libsdl-ttf2.0-dev libsdl-mixer1.2-dev libsdl-image1.2-dev

Download Examples：

git clone https://github.com/rm-hull/luma.examples.git

cd luma.examples

sudo -H pip3 install -e .

Run Examples：

cd examples

Python3 animated_gif.py

Open example file and try to run an example

![](media/4119d59526339386d5eb05492c73b1d8.png)



### Project 27：Servo

Description：

Servo is applied widely, especially for robot like human robots and moving robots. In this lesson, we will learn how it works.

Components：

| ![image-20230423091146956](media/image-20230423091146956.png) | ![image-20230423091150725](media/image-20230423091150725.png) | ![image-20230423091153908](media/image-20230423091153908.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230423091157445](media/image-20230423091157445.png) | ![image-20230423091200677](media/image-20230423091200677.png) | ![image-20230423091203716](media/image-20230423091203716.png) |
| Breadboard*1                                                 | Servo Motor*1                                                | Jumper Wires                                                 |



Component Knowledge

**Servo:**

A location(angle) driver which can rotate a certain angle with high accuracy. It has three external wires which are brown, red and orange,. Brown one is grounded, red one is positive pole of power and orange one is signal wire.

The rotation angle of servo motor is controlled by regulating the duty cycle of PWM (Pulse-Width Modulation) signal. The standard cycle of PWM signal is 20ms (50Hz). 

Theoretically, the width is distributed between 1ms-2ms, but in fact, it's between 0.5ms-2.5ms. The width corresponds the rotation angle from 0° to 180°. But note that for different brand motor, the same signal may have different rotation angle. ![](media/9c287c5ca4f5792f52b8c72d0d2a5448.png)

Schematic Diagram：

![](media/6f0004cfa8bcc392dc5e7d0f62ba8db9.png)

![](media/d4dc5467a491f3f4ebe29840b29fabdc.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 27_servo.py

Test Result：

Enter the angle value and servo rotates the corresponding value, as shown below:

![](media/336ec8c0690f1175b90e87d87c157c60.png)

Note: Press Ctrl + C on keyboard to exit code running.

Example Code：

```python
import RPi.GPIO as GPIO
import time

servo_min_angle = 2.5  #define pulse duty cycle for minimun angle of servo
servo_max_angle = 12.5  #define pulse duty cycle for maximun angle of servo

servopin = 18   #servo Pin
GPIO.setmode(GPIO.BCM)  #BCM numbers

GPIO.setup(servopin,GPIO.OUT)
p = GPIO.PWM(servopin,50)  #set 50Hz , The working frequency of the steering gear is 50Hz
p.start(0)  # start PWM
time.sleep(2)

#define function, map a value from one range to another range
def map(angle, val1, val2, min_angle, max_angle):
    return (max_angle-min_angle)*(angle-val1)/(val2-val1)+min_angle

while(True):  #loop
    p.ChangeDutyCycle(0)   #set 
    time.sleep(0.4)
    b = input("input Angle:")
    b = int(b)
    c = map(b, 0, 180, servo_min_angle, servo_max_angle)  #map angle from 0~180 to 2.5~12.5
    p.ChangeDutyCycle(c) 
    time.sleep(0.4)
    
p.stop()
GPIO.cleanup()
```



### Project 28：L293D Driver Motor

Description：

In generally, we use a DC motor to make smart car. What should we do if we want to control the rotation speed and direction? Here, we need an L293D driver motor.

Components:

| ![image-20230423091723484](media/image-20230423091723484.png) | ![image-20230423091731081](media/image-20230423091731081.png) | ![image-20230423091734681](media/image-20230423091734681.png) | ![image-20230423091738552](media/image-20230423091738552.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230423091742568](media/image-20230423091742568.png) | ![image-20230423091746168](media/image-20230423091746168.png) | ![image-20230423091749257](media/image-20230423091749257.png) |                                                              |
| Jumper Wires                                                 | L293D Chip*1                                                 | Motor*1                                                      |                                                              |



Component Knowledge:

**L293D Chip:**

It is a DC current DC IC which is applied to drive DC motor and stepper motor. In addition, it has 16 pins driving two-way DC motor at same time.

Input voltage range: 4.5 V \~ 36 V

Output current: MAX 600mA, can drive inductive loaded, especially its input end can be connected to MCU directly, controlled by MCU easily.

The two-channel motor can be driven and rotate clockwise and anticlockwise when changing the high and low level on input port.

![](media/2e5e0bd5b4577ac159d0568404dc21b5.png)

| \# | Pin Name | Description                                         |
|----|----------|-----------------------------------------------------|
| 1  | Enable1  | Enable pin input 1(2) and Input 2(7)                |
| 2  | In1      | Control output1 and controlled  by digital circuit  |
| 3  | Out1     | Connect one end of motor1                           |
| 4  | 0V       | Connected to 0V of circuit.                         |
| 5  | 0V       | Connected to 0V of circuit.                         |
| 6  | Out2     | Connect the other end of motor1                     |
| 7  | In2      | Control output2 and controlled  by digital circuit  |
| 8  | +V motor | Connect to 4.5V-36V) of motor                       |
| 9  | Enable2  | Enable pin input 3(10) and 4(15)                    |
| 10 | In3      | Control output pin 3                                |
| 11 | Out3     | Connect one end of motor 2                          |
| 12 | 0V       | Connected to 0V of circuit.                         |
| 13 | 0V       | Connected to 0V of circuit.                         |
| 14 | Out4     | Connect the other end of motor 2                    |
| 15 | In4      | Control output 4 and controlled by  digital circuit |
| 16 | +V       | Connect to + 5V to enable IC function               |

Schematic Diagram：

![](media/88f9ff66e98070062caa1d4695895d44.png)

![](media/980102d2b59a950e13401394f6b8dcc2.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 28_L293D_motor.py

Test Result：

Motor rotates clockwise for 3s, stops for 2s, anticlockwise for 3s and stops for 2 s.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
import time

#define L293D pin
INA1 = 17
INA2 = 27
ENA = 22


GPIO.setmode(GPIO.BCM)

GPIO.setup(INA1,GPIO.OUT)
GPIO.setup(INA2,GPIO.OUT)
GPIO.setup(ENA,GPIO.OUT)

pwmA = GPIO.PWM(ENA,100)  #create a PWM instance
pwmA.start(0)   #start PWM

def forward():
    GPIO.output(INA1,GPIO.HIGH)
    GPIO.output(INA2,GPIO.LOW)
    pwmA.ChangeDutyCycle(100)
    
def back():
    GPIO.output(INA1,GPIO.LOW)
    GPIO.output(INA2,GPIO.HIGH)
    pwmA.ChangeDutyCycle(70)
    
def stop():
    pwmA.ChangeDutyCycle(0)
    
    
while True:     #loop
    forward()
    time.sleep(3)
    stop()
    time.sleep(2)
    back()
    time.sleep(3)
    stop()
    time.sleep(2)
    

pwmA.stop()  #stop PWM
GPIO.cleanup()    #release all GPIO
```



### Project 29：ULN2003 Stepper Motor Driver

Description：

Stepper motor is applied widely in our daily life, such as hard drives, 3D printers, CNC machine tools, robots, etc.

Let’s get started with stepper motor.

Components：

| ![image-20230423091910410](media/image-20230423091910410.png) | ![image-20230423091913531](media/image-20230423091913531.png) | ![image-20230423091928411](media/image-20230423091928411.png) | ![image-20230423091931977](media/image-20230423091931977.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230423091941004](media/image-20230423091941004.png) | ![image-20230423091947403](media/image-20230423091947403.png) | ![image-20230423091950458](media/image-20230423091950458.png) | ![image-20230423091953482](media/image-20230423091953482.png) |
| Driver Board ULN2003*1                                       | 5V 4-Phase Stepper Motor*1                                   | M-F Dupont Line                                              | Jumper Wires                                                 |



Component Knowledge:

**28BYJ-48 Stepper Motor：**

Stepper motor consists of stators and rotors. Stators are fixed, as shown below, which are the part A, B, C and D coils surround. The coil set will produce magnetic field when electrified. 

The rotor is the rotation part( the central part of stators), as shown below:

![](media/32748e0804b1fff434181cb228b23242.png)

Single -Phase four Beat：

The poles of rotor point at A coil when it is electrified, then it is disconnected, B is connected, rotor rotates to C; then C is disconnected and D is connected, rotor rotates to D; however, D is disconnected and A is electrified, rotor rotates to A. Therefore, rotor turns 180° and continuously rotates B-C-D-A, which means it runs a circle (eight phase). 

As shown below, the rotation principle of stepper motor is A - B - C - D - A.

The poles of rotor points at A coil when A is electrified; then it is cut, B coil is connected.

You make order inverse(D - C - B - A - D .....) if you want to make stepper motor rotate anticlockwise.

![](media/b8ae50bbdee2dd5bc683e8c450baee6a.png)

Half-phase and eight beat：

8 beat adopts single and dual beat way，A - AB - B - BC - C - CD - D - DA - A ...... ，rotor will rotate half phase in this order. For example, when A coil is electrified, rotor faces to A coil  then A and B coil are connected, on this condition, the strongest magnetic field produced lies in the central part of AB coil, which means rotating half-phase clockwise.

**Stepper Motor Parameters**：

The rotor rotates one circle when the stepper motor we provide rotates 32 phases and with the output shaft driven by 1:64 reduction geared set.

Therefore the rotation (a circle) of output shaft requires 2048 phases.

The step angle of 4-beat mode of 5V and 4-phase stepper motor.

is 11.25. And the step angle of 8-beat mode is 5.625, the reduction ratio is 1:64.

More details about ULN2003 chip, you could look through chip specification folder.

Schematic Diagram:

![](media/d62ddc971eef5a5d287c4f2b0fef1433.png)

![](media/d3e72e4f7d8a69b49e5ececf957f4487.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 29_ULN2003.py

Test Result：

Rotate anticlockwise for one circle and stop for 3s and one circle in clockwise orientation, stop for 3s

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

for single-phase four beat

```python
import RPi.GPIO as GPIO
import time
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)       # Numbers GPIOs by physical location

IN1 = 22   
IN2 = 27
IN3 = 17
IN4 = 4
GPIO.setup(IN1, GPIO.OUT)      # Set pin's mode is output
GPIO.setup(IN2, GPIO.OUT)
GPIO.setup(IN3, GPIO.OUT)
GPIO.setup(IN4, GPIO.OUT)

#Output the high and low level of each pin to drive the stepping motor
def setStep(w1, w2, w3, w4):  
	GPIO.output(IN1, w1)
	GPIO.output(IN2, w2)
	GPIO.output(IN3, w3)
	GPIO.output(IN4, w4)

def stop():                     # stop
	setStep(0, 0, 0, 0)

def backward(delay, steps):       # Counterclockwise rotation
	for i in range(0, steps):
		setStep(1, 0, 0, 0)
		time.sleep(delay)
		setStep(0, 1, 0, 0)
		time.sleep(delay)
		setStep(0, 0, 1, 0)
		time.sleep(delay)
		setStep(0, 0, 0, 1)
		time.sleep(delay)

def forward(delay, steps):     #lockwise rotation
	for i in range(0, steps):
		setStep(0, 0, 0, 1)
		time.sleep(delay)
		setStep(0, 0, 1, 0)
		time.sleep(delay)
		setStep(0, 1, 0, 0)
		time.sleep(delay)
		setStep(1, 0, 0, 0)
		time.sleep(delay)

def loop():
	while True:
		print "backward..."
		backward(0.003, 512)  # 512 steps --- 360 angle
		

		print "stop..."
		stop()                 # stop
		time.sleep(3)          # sleep 3s
		
		print "forward..."
		forward(0.003, 512)
		
		print "stop..."
		stop()
		time.sleep(3)

if __name__ == '__main__':         # Program start from here
	try:
		loop()
	except KeyboardInterrupt:  # When 'Ctrl+C' is pressed.
	    GPIO.cleanup()     # Release resource


```



### Project 30：Thermometer

Description：

We will teach you how to make a thermometer. Does it sound interesting?

Components：

| ![image-20230423092241981](media/image-20230423092241981.png) | ![image-20230423092245723](media/image-20230423092245723.png) | ![image-20230423092248796](media/image-20230423092248796.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230423092252619](media/image-20230423092252619.png) | ![image-20230423092256092](media/image-20230423092256092.png) | ![image-20230423092300940](media/image-20230423092300940.png) |
| Breadboard*1                                                 | Potentiometer*1                                              | Jumper Wires                                                 |
| ![image-20230423092317596](media/image-20230423092317596.png) | ![image-20230423092320652](media/image-20230423092320652.png) | ![image-20230423092323564](media/image-20230423092323564.png) |
| LCD 1602 display*1                                           | LM35-DZ * 1                                                  | PCF8591 A/D Converter Module*1                               |



Component Knowledge

It is widely used temperature sensor whose output voltage proportional to temperature. It outputs 0°at the beginning since it adopts internal compensation. Its sensitivity is 10mV/℃ and output temperature in the range of 0℃～100℃.

Transfer formula: output 0V when 0°, plus 1° each time, output voltage increases 10mV.

![](media/ec7093fbb4e3578c3edac13c187582d7.jpeg)

Note: VCC is connected to （+）, GND to （-）. LM35-DZ will be burned if connecting inversely

Schematic Diagram：

![](media/a4cfca10725182b6336a5d81163f1ba5.png)

![](media/c17959eb51c46f205f4d2b03dbdd3554.png)

Run Example Code：

Note: in the experiment, I2C communication is used. We need to check the iic address first( enter command：i2cdetect -y 1 and press “Enter”. 

If failed, check the wiring is correct or not. If correct, you need to enable I2C communication function of Raspberry Pi, project 19 is for your reference.

After activating the I2C communication function of Raspberry Pi, input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 30_LM35.py

Test Result：

LCD1602 displays the temperature value.

Note: Press Ctrl + C on keyboard and exit code running.

Example Code：

```python
#!/usr/bin/python
#import
import RPi.GPIO as GPIO
import time
import smbus

Define GPIO to LCD mapping

LCD_RS = 19
LCD_E  = 13
LCD_D4 = 22
LCD_D5 = 27
LCD_D6 = 17
LCD_D7 = 4

Define some device constants

LCD_WIDTH = 16    # Maximum characters per line
LCD_CHR = True
LCD_CMD = False

LCD_LINE_1 = 0x80 # LCD RAM address for the 1st line
LCD_LINE_2 = 0xC0 # LCD RAM address for the 2nd line

Timing constants

E_PULSE = 0.0005
E_DELAY = 0.0005

address=0x48
cmd=0x40
A0=0x40##A0---->port address
A1=0x41
A2=0x42
A3=0x43
bus=smbus.SMBus(1)

def main():
    # Main program block
    GPIO.setwarnings(False)
    GPIO.setmode(GPIO.BCM)       # Use BCM GPIO numbers
    GPIO.setup(LCD_E, GPIO.OUT)  # E
    GPIO.setup(LCD_RS, GPIO.OUT) # RS
    GPIO.setup(LCD_D4, GPIO.OUT) # DB4
    GPIO.setup(LCD_D5, GPIO.OUT) # DB5
    GPIO.setup(LCD_D6, GPIO.OUT) # DB6
    GPIO.setup(LCD_D7, GPIO.OUT) # DB7
    

    # Initialise display
    lcd_init()
    
    while True:
        temp = analogRead(0)
        print("Temp = %s"%(temp))
        #display
        # Send some test
        lcd_string("Rasbperry Pi",LCD_LINE_1)
        lcd_string(temp,LCD_LINE_2)
        time.sleep(0.1);

#LM35, require Temperature
def analogRead(count):
    read_val=bus.read_byte_data(address,cmd+count)
    Temp_val = (read_val*500)/256  #Calculate the degree Celsius
    Temp_val = str(Temp_val)  # int to string
    #Temp_val = str(read_val)
    return Temp_val


def lcd_init():
    # Initialise display
    lcd_byte(0x33,LCD_CMD) # 110011 Initialise
    lcd_byte(0x32,LCD_CMD) # 110010 Initialise
    lcd_byte(0x06,LCD_CMD) # 000110 Cursor move direction
    lcd_byte(0x0C,LCD_CMD) # 001100 Display On,Cursor Off, Blink Off
    lcd_byte(0x28,LCD_CMD) # 101000 Data length, number of lines, font size
    lcd_byte(0x01,LCD_CMD) # 000001 Clear display
    time.sleep(E_DELAY)

def lcd_byte(bits, mode):
    # Send byte to data pins
    # bits = data
    # mode = True  for character
    #        False for command
    

    GPIO.output(LCD_RS, mode) # RS
    
    # High bits
    GPIO.output(LCD_D4, False)
    GPIO.output(LCD_D5, False)
    GPIO.output(LCD_D6, False)
    GPIO.output(LCD_D7, False)
    if bits&0x10==0x10:
        GPIO.output(LCD_D4, True)
    if bits&0x20==0x20:
        GPIO.output(LCD_D5, True)
    if bits&0x40==0x40:
        GPIO.output(LCD_D6, True)
    if bits&0x80==0x80:
        GPIO.output(LCD_D7, True)
    
    # Toggle 'Enable' pin
    lcd_toggle_enable()
    
    # Low bits
    GPIO.output(LCD_D4, False)
    GPIO.output(LCD_D5, False)
    GPIO.output(LCD_D6, False)
    GPIO.output(LCD_D7, False)
    if bits&0x01==0x01:
        GPIO.output(LCD_D4, True)
    if bits&0x02==0x02:
        GPIO.output(LCD_D5, True)
    if bits&0x04==0x04:
        GPIO.output(LCD_D6, True)
    if bits&0x08==0x08:
        GPIO.output(LCD_D7, True)
    
    # Toggle 'Enable' pin
    lcd_toggle_enable()

def lcd_toggle_enable():
    # Toggle enable
    time.sleep(E_DELAY)
    GPIO.output(LCD_E, True)
    time.sleep(E_PULSE)
    GPIO.output(LCD_E, False)
    time.sleep(E_DELAY)

def lcd_string(message,line):
    # Send string to display
    

    message = message.ljust(LCD_WIDTH," ")
    
    lcd_byte(line, LCD_CMD)
    
    for i in range(LCD_WIDTH):
        lcd_byte(ord(message[i]),LCD_CHR)

 


if __name__ == '__main__':  # Program entrance
try:
    main()  #call main()
except KeyboardInterrupt:
    pass
finally:
    lcd_byte(0x01, LCD_CMD)
    GPIO.cleanup()
```

### Project 31：DHT11 Temperature and Humidity Sensor

Description：

In this lesson, we will show you how temperature and humidity sensor works.

Components：

| ![image-20230423092549047](media/image-20230423092549047.png) | ![image-20230423092551935](media/image-20230423092551935.png) | ![image-20230423092555279](media/image-20230423092555279.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230423092603247](media/image-20230423092603247.png) | ![image-20230423092607310](media/image-20230423092607310.png) | ![image-20230423092559125](media/image-20230423092559125.png) |
| DHT11 Temperature and Humidity Sensor*1                      | Jumper Wires                                                 | Breadboard*1                                                 |



Component Knowledge

**DHT11 Temperature Humidity Sensor：**

It is a composite sensor which contains a calibrated digital signal output of the temperature and humidity.

The sensor can measure temperature from 0°C to 50°C and humidity from 20% to 90% with an accuracy of ±1°C and ±1%. So if you are looking to measure in this range then this sensor might be the right choice for you.

DHT11 temperature and humidity sensor uses dedicated digital module acquisition technology and temperature and humidity sensing technology to ensure that the product has extremely high reliability and excellent long-term stability. 

The temperature and humidity sensor includes a resistive humidity sensing element and an NTC temperature measurement element, which is very suitable for temperature and humidity measurement occasions that do not require high accuracy and real-time. The working voltage is in the range of 3.3V-5.5V.

In addition, it comes with a dedicated NTC to measure temperature and an 8-bit microcontroller to output the values of temperature and humidity as serial data.

DHT11 has three pins which are VCC，GND and S.

S is data output pin and uses serial communication.

**DHT11 Temperature and Humidity 1-wire Bus Format Definition**

| **Name**        | **1-wire Bus Format Definition**                                                                                                                                 |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initial Signal  | MCU pulls data bus（SDA）down at least 18ms（no more than 30ms）and inform sensor to prepare data                                                                |
| Response Signal | Sensor pulls data bus（SDA）down for 83µs and up for 87µs to response the initial signal of host                                                                 |
| Humidity        | Humidity high bit is part humidity integer data and humidity low bit is the part decimal data                                                                    |
| Temperature     | Humidity high bit is part humidity integer data and humidity low bit is the part decimal data. Bit8 means negative temperature, otherwise positive temperature   |
| Parity Bit      | ＝Humidity high bit+ Humidity low bit+temperature high bit+temperature low bit                                                                                   |

**Sequence Diagram：**

DHT11 switches low consumption mode to high consumption mode after the user host（MCU）sends a start signal. Then DHT11 will emit a response signal and 40bit data and trigger a information collection, as shown below:

![](media/933ac5e5a5e921d4b16c7c48091ba75a.png)Detailed DHT11 protocol：

<https://www.mouser.com/datasheet/2/758/DHT11-Technical-Data-Sheet-Translated-Version-1143054.pdf>

Schematic Diagram：

![](media/8e3f2bb885d212fa5df7bfc6e8571004.png)

![](media/5974c6541c6b79b4f41429f380cd1fb2.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 31_DHT11.py

Test Result：

Terminal prints the temperature and humidity value.

Note: Press Ctrl + C on keyboard to exit code running7.Example Code：

Example Code：

```python
-*- coding: utf-8 -*-

import RPi.GPIO as GPIO   #import the GPIO module from RPI.GPIO.
import time               #import the time module.
dhtPin = 18                #set 'dhtPin' as digital 18.

GPIO.setmode(GPIO.BCM)    #set gpio as BCM mode.
time.sleep(1)             #delay 1 second.
data=[]                   #init array

def test():
    loopCnt = 0
    #Host signal start
    GPIO.setup(dhtPin, GPIO.OUT) #To send a start signal, set the pin to output
    GPIO.output(dhtPin, GPIO.LOW)#Pin output low level
    time.sleep(0.02)              #delay 0.02 second. >=18ms Host start signal
    GPIO.output(dhtPin, GPIO.HIGH) #Pin output high level
    time.sleep(0.00004)          #delay 40us.
    #End of host signal

    #Read-signal preparation
    GPIO.setup(dhtPin, GPIO.IN)  #set gpio 9 as input mode.
    loopCnt = 0
    while GPIO.input(dhtPin)==GPIO.LOW:  #The normal low level here is 83US
        loopCnt +=1
        time.sleep(0.000001)
        if loopCnt > 100:       #It's wrong if the time is greater than 83US
            print("time out 2!")  #Print out time Out 2! Indicates that the data is wrong here
            break    #Exit the loop
    loopCnt = 0
    while GPIO.input(dhtPin)==GPIO.HIGH: #The normal low level here is 87US
        loopCnt +=1
        time.sleep(0.000001)
        if loopCnt > 100:       #It's an error if the time is greater than 87US
            print("time out 3!")  #Print out time Out 3! Indicates that the data is wrong here
            break   #Exit the loop
    #Read signal ready to end
    #Start reading 40 bits of data
    j = 0
    while j < 40:     #store 40 piecs of data.
        loopCnt = 0
        #The low level of 54MS is read, and each bit of data starts at the low level of 54US
        while GPIO.input(dhtPin) == GPIO.LOW:   #Instead of checking the 54US low level, we just wait for the low level to pass
            loopCnt +=1
            if loopCnt > 50000:  #If the low level is too long, it is not correct and the terminal prints time out 4! And exit the loop
               print("time out 4!")
               break
     
        start_time = time.time()  #Record the moment when the high level reading begins
        loopCnt = 0
        while GPIO.input(dhtPin) == GPIO.HIGH:   #Wait for the high level to pass
            loopCnt +=1
            if loopCnt > 50000:
               print("time out 5!")
               break
    
        stop_time = time.time() #The moment when the high level ends
        t = stop_time - start_time #Figure out the time it takes to read to the high level
        #The high level range of logic 0 is 23~ 27US, and the high level of logic 1 is 70US. 
        #Then we set less than 40US as logic 0, otherwise it is 1
        if t < 0.00004:   #If the high level time read is less than 40US
            data.append(0) #Add a 0 at the end of the array data
        else:
            data.append(1) # Add a 1 to the end of the array data
        j += 1 # Add one to read the next data
    
    #The 40bits were split into 5 bytes, 8 bits for each byte, namely, 
    #8 bits for high humidity, 8 bits for low humidity, 
    #8 bits for high temperature, 8 bits for low temperature, and 8 bits for checking
    humidity_bit = data[0:8]
    humidity_point_bit = data[8:16]
    temperature_bit = data[16:24]
    temperature_point_bit = data[24:32]
    check_bit = data[32:40]
    
    #Defines the value used to store the calculated value
    humidity = 0
    humidity_point = 0
    temperature = 0
    temperature_point = 0
    check = 0
     
    #calculate each data and checksum.
    for i in range(8):  #This is converting every bit of base 2 to base 10 and adding them up
        humidity += humidity_bit[i] * 2 ** (7 - i)   
        humidity_point += humidity_point_bit[i] * 2 ** (7 - i)
        temperature += temperature_bit[i] * 2 ** (7 - i)
        temperature_point += temperature_point_bit[i] * 2 ** (7 - i)
        check += check_bit[i] * 2 ** (7 - i)
    #checksum
    checksum = humidity + humidity_point + temperature + temperature_point


    
    #If the check value == humidity value + temperature value, then the received data is correct
    if check == checksum: 
        print('data is right')
        print("T: "+str(temperature)+", H: "+str(humidity))  #The terminal prints the temperature and humidity values in character form
    else:
        print('data is error')
        print("T: "+str(temperature)+", H: "+str(humidity)+ ", check: "+str(check)+", checksum: "+str(checksum))

if __name__ == '__main__':   #Program entrance
    try:
        while True:
            test() #call function test()
            data = []   #Clears the array data to prepare for the next data reception
            time.sleep(3)  #The read cycle needs to be greater than 2 seconds
        except KeyboardInterrupt:
    GPIO.cleanup()
```



Code Knowledge：

**Binary to decimal**

For instance 1100 1001，the first bit from the left is 1\*27，Python writing of power is \*\*，therefore, 1\*2\*\*7 +, the second bit is 1\*2\*\*6 + .....



### Project 32：DS3231

Description：

Clock module could be taken as timer and time display. In this lesson, we will learn about DS3231 module.

Experiment Components：

| ![image-20230423092905763](media/image-20230423092905763.png) | ![image-20230423092911906](media/image-20230423092911906.png) | ![image-20230423092919329](media/image-20230423092919329.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230423092926833](media/image-20230423092926833.png) | ![image-20230423092930033](media/image-20230423092930033.png) | ![image-20230423092933249](media/image-20230423092933249.png) |
| Breadboard*1                                                 | DS3231 Clock Module*1                                        | Jumper Wires                                                 |



Component Knowledge

**DS3231 Clock Module：**

DS3231 also has dual power supply functions for main power supply and backup power supply.

DS3231 provides a reset output, 2 programmable calendar alarms and 1 programmable square wave output. It monitors the VCC status through a precise, temperature-compensated voltage reference and comparator, detects power failures, and automatically switches to a backup power supply when necessary. 

In addition, the DS3231 clock module has a rechargeable battery to ensure that the clock can still move normally after the system is powered off.

DS3231 is a real-time clock chip, which can provide information such as seconds, minutes, hours, date, month, and year, and can read the calendar before 2100 .

The DS1302 can communicate with the single-chip microcomputer through the synchronous serial way and only three ports needed which are RST reset , I/O data line and SCLK serial clock. 

The real-time clock/calendar circuit provides information about seconds, minutes, hours, days, weeks, months, and years. In addition, the number of days in a month and ones of a leap year can be adjusted automatically. 

Compatible with DS1202, it has a 31×8 RAM register for temporary storage of data.

The clock operation can adopt 24 or 12 hour format through AM/PM indication.

DS3231 clock module has pin GND, VCC, SDA and SCL, and use iic communication agreement，VCC is for positive of main power；GND is grounded；SDA is serial data input, output；SCL is serial clock input.

-   1)Temperature range: -40 to +85; Timing accuracy : ± 5ppm (±0.432 seconds / day)
    
-   2)Provide battery backup for continuous timing

-   3)Low power consumption

-   4)Device package and function compatible with DS3231

-   5)Complete clock calendar function contains seconds and minutes, hour, week, date, month, and year timing and provides leap year compensation until 2100.
    
-   6)Two calendar clock

-   7)Output: 1Hz and 32.768kHz

-   8)Reset output and Input Debounce of Pushbutton

-   9)High speed (400kHz), I2C serial bus

-   10)Supply voltage: +3.3V to +5.5V

-   11)Digital temperature sensor with a precision of±3℃

-   12)Working temperature: -40 \~ C to +85 \~ C

-   13)16 pins Small Outline Package (300mil)

More details about DS3231 chip, you could look through chip specification folder

Schematic Diagram：

![](media/1138bbcfb04a9f6bbea6eebfd5cc1a91.png)

![](media/d2b6b87b3923f0724abf362074be8784.png)

Run Example Code：

Note: in the experiment, I2C communication is used. We need to check the iic address first( enter command：i2cdetect -y 1 and press“Enter”. 

If failed, check the wiring is correct or not. If correct, you need to enable I2C communication function of Raspberry Pi, project 19 is for your reference.

After enabling the I2C communication，input the following commands and press "Enter".

cd /home/pi/pythonCode_A

python 32_ds3231.py

Test Result：

Print time in terminal

Note: Press Ctrl + C on keyboard to exit code runningExample Code：

Example Code：

```python
#-*- coding: UTF-8 -*-
import RPi.GPIO as GPIO
import smbus   
import time

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

addr_ds3231 = 0x68 ##address  ---> device address
addr_second = 0x00
addr_minute = 0x01
addr_hour = 0x02
addr_week = 0x03
addr_data = 0x04
addr_month = 0x05
addr_year = 0x06

dat = []  # Defines a list that stores the time it was read

def set_time():
    bus.write_byte_data(addr_ds3231,addr_year,0x20)  ##20
    bus.write_byte_data(addr_ds3231,addr_month,0x03) ##March
    bus.write_byte_data(addr_ds3231,addr_data,0x26)  ##date 26 
    bus.write_byte_data(addr_ds3231,addr_week,0x04)  ##Thursday
    bus.write_byte_data(addr_ds3231,addr_hour,0x12)  ##24 hour mode,12 o'clock
    bus.write_byte_data(addr_ds3231,addr_minute,0x30)
    bus.write_byte_data(addr_ds3231,addr_second,0x00)

def read_time():
    second = bus.read_byte_data(addr_ds3231,addr_second)  #The seconds read are assigned to the variable second
    minute = bus.read_byte_data(addr_ds3231,addr_minute)
    hour = bus.read_byte_data(addr_ds3231,addr_hour)
    week = bus.read_byte_data(addr_ds3231,addr_week) 
    data = bus.read_byte_data(addr_ds3231,addr_data) 
    month = bus.read_byte_data(addr_ds3231,addr_month)
    year = bus.read_byte_data(addr_ds3231,addr_year) 

    # .append , Add an element to the end of the list

    dat.append(year/16*10 + year%16 + 2000)   #To calculate the years, 0x20 to 20
    dat.append(month/16*10 + month%16)
    dat.append(data/16*10 + data%16)
    dat.append(week)
    dat.append(hour/16*10 + hour%16) 
    dat.append(minute/16*10 + minute%16)
    dat.append(second/16*10 + second%16)
    
bus = smbus.SMBus(1)             #Create an instance of smbus
set_time()
while True:                      ##loop 
    read_time()
    print "date: year  month  date  week  hour  minute  second"
    print "date:",dat            ##print data
    dat = []  #Clear the array DAT to 0
    time.sleep(1)                ##delay 1 second
```



Code Explanation：

| dat.append(year/16\*10 + year%16 + 2000)                                                    |
|---------------------------------------------------------------------------------------------|
| Transfer hexadecimal 0x20 into decimal 20 and plus 2000=2020 0x20 / 16 = 20 , 0x20 % 16 = 0 |



### Project 33：Joystick Module

Description：

Many a people play games with gamepad. But do you know who it work?

Let’s learn about it.

Components：

| ![image-20230423093640732](media/image-20230423093640732.png) | ![image-20230423093644038](media/image-20230423093644038.png) | ![image-20230423093647110](media/image-20230423093647110.png) | ![image-20230423093650758](media/image-20230423093650758.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin ColorfulJumper Wires*1                                | Breadboard*1                                                 |
| ![image-20230423093654454](media/image-20230423093654454.png) | ![image-20230423093657702](media/image-20230423093657702.png) | ![image-20230423093700598](media/image-20230423093700598.png) | ![image-20230423093703590](media/image-20230423093703590.png) |
| Joystick Module*1                                            | PCF8591 A/D Converter Module*1                               | Jumper Wires                                                 | M-F Dupont Line                                              |



Component Knowledge

This is a joystick very similar to the ‘analog’ joysticks on PS2 (PlayStation 2) controllers. It is a self-centering spring loaded joystick, meaning when you release the joystick it will center itself. It also contains a comfortable cup-type knob/cap which gives the feel of a thumb-stick.

It has three signal pins which are connected GND, VCC and signal end（B, X, Y). The X pin is **X-axis** (left to right), the Y pin is **Y-axis** (front and back) and signal B end is Z-axis(usually used as digital port and pushbutton)

VCC is connected to V/VCC（3.3/5V）of MCU, GND to G/GND of MCU and the voltage is around 1.65V/2.5V in initial status

X axis gives readout of the joystick in the horizontal direction (X-coordinate) i.e. how far left and right the joystick is pushed.

Y axis gives readout of the joystick in the vertical direction (Y-coordinate) i.e. how far up and down the joystick is pushed.

Z axis is the output from the pushbutton. It’s normally open, meaning the digital readout from the SW pin will be HIGH. When the button is pushed, it will connect to GND, giving output LOW.

Schematic Diagram：

![](media/02e9dd7858abaf7327d45f48d584982d.png)

![](media/9374b718f5ed44b145926b1672019340.png)

Run Example Code：

Note: in the experiment, I2C communication is used. We need to check the iic address first( enter command：i2cdetect -y 1 and press“Enter”. 

If failed, check the wiring is correct or not. If correct, you need to enable I2C communication function of Raspberry Pi, project 19 is for your reference.

After enabling the I2C communication，input the following commands and press "Enter".

cd /home/pi/pythonCode_A

python 33_joystick.py

Test Result：

Move joystick , the terminal will show the responding data change. If you press it,“The key is pressed”is displayed in the terminal.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
import smbus   
import time

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

key = 26  # joystic button pin
GPIO.setup(key,GPIO.IN)

address = 0x48 ##address  ---> device address
cmd = 0x40     ##DA converter command
A0 = 0x40      ##A0  ----> port address
A1 = 0x41
A2 = 0x42
A3 = 0x43
bus = smbus.SMBus(1)            ##start the bus

def analogRead(count):   #function,read analog data
    read_val = bus.read_byte_data(address,cmd+count)
    return read_val

while True:                     ##loop 
    #Vout = 10                  ##10*0.0196=0.196V
    #bus.write_byte_data(address,cmd,Vout) ##DA converter
    x_val = analogRead(0) ##read A0 data
    y_val = analogRead(1) #read A1 data
    print("x:%1.0f  y:%1.0f" %(x_val,y_val))          ##print data
    if GPIO.input(key):   
        print("The key is presed")   


GPIO.cleanup()
```





### Project 34：Ultrasonic

Description：

An ultrasonic sensor is an electronic device that measures the distance of a target object by emitting ultrasonic sound waves, and converts the reflected sound into an electrical signal.

Components：

| ![image-20230423094330178](media/image-20230423094330178.png) | ![image-20230423094333579](media/image-20230423094333579.png) | ![image-20230423094336444](media/image-20230423094336444.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230423094340845](media/image-20230423094340845.png) | ![image-20230423094343884](media/image-20230423094343884.png) | ![image-20230423094346972](media/image-20230423094346972.png) |
| Breadboard*1                                                 | HC-SR04 Ultrasonic Sensor*1                                  | Jumper Wires                                                 |



Component Knowledge

The ultrasonic module will emit the ultrasonic waves after trigger signal. When the ultrasonic waves encounter the object and are reflected back, the module outputs an echo signal, so it can determine the distance of object from the time difference between trigger signal and echo signal. 

The t is the time that emitting signal meets obstacle and returns.

and the propagation speed of sound in the air is about 343m/s, therefore,  distance = speed * time, because the ultrasonic wave emits and comes back, which is 2 times of distance, so it needs to be divided by 2, the distance measured by **ultrasonic wave = (speed \* time)/2**

**Use method and timing chart of ultrasonic module:  **

1.  Setting the delay time of Trig pin of SR04 to 10μs at least, which can trigger it to detect distance.  
1.  After triggering, the module will automatically send eight 40KHz ultrasonic pulses and detect whether there is a signal return. This step will be completed automatically by the module.  
1.  If the signal returns, the Echo pin will output a high level, and the duration of the high level is the time from the transmission of the ultrasonic wave to the return.

![image-20231114185045781](media/image-20231114185045781.png)

Schematic Diagram：

![](media/71b8b763852ae90066f9972f4bdf40ae.png)

![](media/d17997fbbab5e470fcac62fe8440e7d1.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 34_ultrasonic.py

Test Result：

Terminal prints the detected distance, unit is cm.

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)

#define GPIO pin
GPIO_TRIGGER = 23
GPIO_ECHO = 24

#set GPIO mode (IN / OUT)
GPIO.setup(GPIO_TRIGGER, GPIO.OUT)
GPIO.setup(GPIO_ECHO, GPIO.IN)

def distance():
    # 10us is the trigger signal
    GPIO.output(GPIO_TRIGGER, True)
    time.sleep(0.00001)  #10us
    GPIO.output(GPIO_TRIGGER, False)
    

    start_time = time.time()
    stop_time = time.time()
    
    while GPIO.input(GPIO_ECHO) == 0:   #Indicates that the ultrasonic wave has been emitted
        start_time = time.time()  #Record launch time
      
    while GPIO.input(GPIO_ECHO) == 1:   #Indicates that the returned ultrasound has been received
        stop_time = time.time()   #Record receiving time
      
    time_elapsed = stop_time - start_time  #Time difference from transmit to receive
    distance = (time_elapsed * 34300) / 2  #Calculate the distance
    return distance   #Return to calculated distance

if __name__ == '__main__':   #Program entry
    try:
        while True:  
            dist = distance()  #
            print("Measured Distance = {:.2f} cm".format(dist)) #{:.2f},Keep two decimal places
            time.sleep(0.1)
    # Reset by pressing CTRL + C
except KeyboardInterrupt:
    print("Measurement stopped by User")
    GPIO.cleanup()
```



### Project 35：Accelerometer and Gyroscope Module

Description：

When creating balance robot car, we need to take account of the balanced angles. 

This requires a sensor detecting posture------MPU6050

Components：

| ![image-20230423094542656](media/image-20230423094542656.png) | ![image-20230423094546492](media/image-20230423094546492.png) | ![image-20230423094549597](media/image-20230423094549597.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230423094552750](media/image-20230423094552750.png) | ![image-20230423094556333](media/image-20230423094556333.png) | ![image-20230423094559596](media/image-20230423094559596.png) |
| Breadboard*1                                                 | MPU6050*1                                                    | Jumper Wires                                                 |



Component Knowledge

**MPU6050：**

The MPU6050 is a Micro Electro-Mechanical Systems (MEMS) which integrates a 3-axis MEMS accelerometer, 3-axis Gyroscope inside it and digital motion processor, using IIC communication.

This helps us to measure acceleration, velocity, orientation, displacement and many other motion related parameter of a system or object.

It can interface the external 3-axis compass and provide complete 9-axis output thanks to I2C. It is also designed to be interfaced with non-inertial digital sensor interface.

The MPU-6050 has 3 16-bit analog-to-digital converters (ADCs) for digital gyroscope output and 3 16-bit ADCs for digital accelerometer output. For accurate tracking of fast and slow motion, the measurable range of the gyroscope is ±250, ±500, ±1000, ±2000°/s (dps); the measurable range of the accelerometer is ±2, ±4, ±8, ±16g.

**Technical Parameter：**

1\. Chip: MPU-6050

2\. Working voltage: 3-5V (internal low bias voltage)

3\. Communication method: standard IIC protocol

4\. Built-in 16-bit analog-to-digital converter, 16-bit data output

5\. The measurable range of the gyroscope is ±250, ±500, ±1000, ±2000°/s (dps); the measurable range of the accelerometer is ±2, ±4, ±8, ±16g.

6\. Needle pitch: 2.54mm

More details about mpu6050 chip, you could look through chip specification folder

Schematic Diagram：

![](media/6508f4ebc11f78fd85bdd01c00b2f42d.png)

![](media/6a83940edfde515b2ad0528cae4598b3.png)

Run Example Code：

Note: in the experiment, I2C communication is used. We need to check the iic address first( enter command：i2cdetect -y 1 and press“Enter”. If failed, check the wiring is correct or not. If correct, you need to enable I2C communication function of Raspberry Pi, project 19 is for your reference.

After enabling the I2C communication，input the following commands and press "Enter".

cd /home/pi/pythonCode_A/35_MPU6050

python 35_MPU6050.py

Test Result：

Note: wait a moment until data appears

Terminal shows the data detected by MPU6050 accelerator and gyroscope and switches to the data about Gravitational acceleration and angular velocity, as shown below:

![](media/1c5fd7be4e52b581dda4f7b590025ea9.png)

Note: Press Ctrl + C on keyboard to exit code running

Example Code：

```python
import MPU6050 
import time

mpu = MPU6050.MPU6050() #instantiate a MPU6050 class object
accel = [0]*3 #store accelerometer data
gyro = [0]*3 #store gyroscope data

def setup():
	mpu.dmp_initialize() #initialize MPU6050

def loop():
	while(True):
		accel = mpu.get_acceleration() #get accelerometer data
		gyro = mpu.get_rotation() #get gyroscope data
		print("a/g:%d\t%d\t%d\t%d\t%d\t%d"%(accel[0],accel[1],accel[2],gyro[0],gyro[1],gyro[2]))
		print("a/g:%.2f g\t%.2f g\t%.2f g\t%.2f d/s\t%.2f d/s\t%.2f d/s"%(accel[0]/16384.0,accel[1]/16384.0,accel[2]/16384.0,gyro[0]/131.0,gyro[1]/131.0,gyro[2]/131.0))
		time.sleep(0.1)

if __name__ == '__main__':
	print("Program is starting ... ")
	setup()
	try:
		loop()
	except KeyboardInterrupt:
		pass


```



### Project 36：4*4 Membrane Switch Keypad

Description：

Matrix keypads are the kind of keypads you see on cell phones, calculators, microwaves ovens, door locks, etc. They’re practically everywhere.

However, in DIY electronics, they let users interact with your project and are often needed to navigate menus, punch in passwords and control robots.

Membrane keypads are made of a thin, flexible membrane material. They do come in may sizes 4×3, 4×4, 4×1 etc. Regardless of their size, they all work in the same way.

Components:

| ![image-20230423095009733](media/image-20230423095009733.png) | ![image-20230423095013328](media/image-20230423095013328.png) | ![image-20230423095016192](media/image-20230423095016192.png) | ![image-20230423095019567](media/image-20230423095019567.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230423095024401](media/image-20230423095024401.png) | ![image-20230423095027263](media/image-20230423095027263.png) | ![image-20230423095030223](media/image-20230423095030223.png) | ![image-20230423095033200](media/image-20230423095033200.png) |
| 4\*4 Membrane Switch Keypad\*1                               | 10KΩ Resistor*4                                              | Servo Motor*1                                                | Jumper Wires                                                 |



Component Knowledge

**Membrane Switch Keypad：**

This keypad integrates many a keys, as shown below, it has 16 keys

![](media/fcd187eb009098d691927511606c991b.jpeg)

If you had used 16 individual push buttons, you would have required 17 input pins (one for each key and a ground pin) in order to make them work. However, with matrix arrangement, you only need 8 microcontroller pins (4-columns and 4-rows) to scan through the pad.

The working principle is very simple. Pressing a button shorts one of the row lines to one of the column lines, allowing current to flow between them. For example, when key‘4’is pressed, column 1 and row 2 are shorted.

![](media/5ebdacba906622079e0ef41dc1ea3fdf.png)

Schematic Diagram：

![](media/a9871809d5070ff65c7d043c47b0c81d.png)

![](media/3149709bc015b5c9056a15f9b2b1647c.png)

Run Example Code1：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 36_1_keyboard.py

Test Result1：

Terminal prints the key values of 4\*4 membrane switch keypad

![](media/cfdd65a706ab8ca108d7dd00c6b72511.png)

Note: Press Ctrl + C on keyboard to exit code runningExample Code1：

Example Code1：

```python
import time
import RPi.GPIO as GPIO

class keypad(object):
  KEYPAD=[
    ['1','2','3','A'],
    ['4','5','6','B'],
    ['7','8','9','C'],
    ['*','0','#','D']]

  ROW =[12,16,20,21]#row
  COLUMN =[6,13,19,26]#col

#init function
def __init__():
  GPIO.cleanup()
  GPIO.setmode(GPIO.BCM)

#Get the number of keys
def getkey():
  GPIO.setmode(GPIO.BCM)
  #Set the column output low
  for i in range(len(keypad.COLUMN)):
    GPIO.setup(keypad.COLUMN[i],GPIO.OUT)
    GPIO.output(keypad.COLUMN[i],GPIO.LOW)
  #Set the row input and pull up
  for j in range(len(keypad.ROW)):
    GPIO.setup(keypad.ROW[j],GPIO.IN,pull_up_down=GPIO.PUD_UP)

  #Detects if a row has a key pressed down and reads the row value if so
  RowVal=-1
  for i in range(len(keypad.ROW)):
    RowStatus=GPIO.input(keypad.ROW[i])
    if RowStatus==GPIO.LOW:
       RowVal=i
       #print('RowVal=%s' % RowVal)
  #If no key is pressed, exit to prepare for the next scan
  if RowVal<0 or RowVal>3:
    exit()
    return

  #If row RowVal has a key pressed down
  #Outputs a high level row RowVal
  GPIO.setup(keypad.ROW[RowVal],GPIO.OUT)
  GPIO.output(keypad.ROW[RowVal],GPIO.HIGH)
  #Column drop-down input
  for j in range(len(keypad.COLUMN)):
    GPIO.setup(keypad.COLUMN[j],GPIO.IN,pull_up_down=GPIO.PUD_DOWN)

  #Read the value of the column in which the key resides
  ColumnVal=-1
  for i in range(len(keypad.COLUMN)):
    ColumnStatus=GPIO.input(keypad.COLUMN[i])
    if ColumnStatus==GPIO.HIGH:
      ColumnVal=i
      #Wait for the button to release
      while GPIO.input(keypad.COLUMN[i])==GPIO.HIGH:
        time.sleep(0.05)
        #print ('ColumnVal=%s' % ColumnVal)
  #If no key is pressed, return
  if ColumnVal<0 or ColumnVal>3:
    exit()
    return

  exit()
  return keypad.KEYPAD[RowVal][ColumnVal] #return keypad value


def exit():
  import RPi.GPIO as GPIO
  for i in range(len(keypad.ROW)):
    GPIO.setup( keypad.ROW[i],GPIO.IN,pull_up_down=GPIO.PUD_UP)
  for j in range(len( keypad.COLUMN)):
    GPIO.setup( keypad.COLUMN[j],GPIO.IN,pull_up_down=GPIO.PUD_UP)

#key=None
while True:
    key=getkey()  #Assigns the detected keyboard value to key
    if not key==None:  #If the key value is not null
        print ('You enter the  key:',key)  #print key
```



Run Example Code2：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 36_2_keyboard.py

Test Result2：

（Password：123D）

Terminal will print open the door and servo will rotate 180 ° if the password is correct； if not, error will be shown and servo will rotate 0°.

![](media/ec809f6f04e864b10da204f3f86b98e8.png)

Note: Press Ctrl + C on keyboard to exit code running

Example Code2：

```python
import time
import RPi.GPIO as GPIO

servo_min_angle = 2.5  #define pulse duty cycle for minimun angle of servo
servo_max_angle = 12.5  #define pulse duty cycle for maximun angle of servo
servopin = 18   #servo Pin
GPIO.setmode(GPIO.BCM)  #BCM numbers
GPIO.setup(servopin,GPIO.OUT)
p = GPIO.PWM(servopin,50)  #set 50Hz , The working frequency of the steering gear is 50Hz
p.start(0)  # start PWM
time.sleep(1)

#define function, map a value from one range to another range
def map(angle, val1, val2, min_angle, max_angle):
    return (max_angle-min_angle)*(angle-val1)/(val2-val1)+min_angle
    
p.ChangeDutyCycle(0)   #set 
time.sleep(0.5)


class keypad(object):
  KEYPAD=[
    ['1','2','3','A'],
    ['4','5','6','B'],
    ['7','8','9','C'],
    ['*','0','#','D']]

  ROW    =[12,16,20,21]#row
  COLUMN =[6,13,19,26]#col

#init function
def __init__():
  GPIO.cleanup()
  GPIO.setmode(GPIO.BCM)

#Get the number of keys
def getkey():
  GPIO.setmode(GPIO.BCM)
  #Set the column output low
  for i in range(len(keypad.COLUMN)):
    GPIO.setup(keypad.COLUMN[i],GPIO.OUT)
    GPIO.output(keypad.COLUMN[i],GPIO.LOW)
  #Set the row input and pull up
  for j in range(len(keypad.ROW)):
    GPIO.setup(keypad.ROW[j],GPIO.IN,pull_up_down=GPIO.PUD_UP)

  #Detects if a row has a key pressed down and reads the row value if so
  RowVal=-1
  for i in range(len(keypad.ROW)):
    RowStatus=GPIO.input(keypad.ROW[i])
    if RowStatus==GPIO.LOW:
       RowVal=i
       #print('RowVal=%s' % RowVal)
  #If no key is pressed, exit to prepare for the next scan
  if RowVal<0 or RowVal>3:
    exit()
    return

  #If row RowVal has a key pressed down
  #Outputs a high level row RowVal
  GPIO.setup(keypad.ROW[RowVal],GPIO.OUT)
  GPIO.output(keypad.ROW[RowVal],GPIO.HIGH)
  #Column drop-down input
  for j in range(len(keypad.COLUMN)):
    GPIO.setup(keypad.COLUMN[j],GPIO.IN,pull_up_down=GPIO.PUD_DOWN)

  #Read the value of the column in which the key resides
  ColumnVal=-1
  for i in range(len(keypad.COLUMN)):
    ColumnStatus=GPIO.input(keypad.COLUMN[i])
    if ColumnStatus==GPIO.HIGH:
      ColumnVal=i
      #Wait for the button to release
      while GPIO.input(keypad.COLUMN[i])==GPIO.HIGH:
        time.sleep(0.05)
        #print ('ColumnVal=%s' % ColumnVal)
  #If no key is pressed, return
  if ColumnVal<0 or ColumnVal>3:
    exit()
    return

  exit()
  return keypad.KEYPAD[RowVal][ColumnVal] #return keypad value


def exit():
  import RPi.GPIO as GPIO
  for i in range(len(keypad.ROW)):
    GPIO.setup( keypad.ROW[i],GPIO.IN,pull_up_down=GPIO.PUD_UP)
  for j in range(len( keypad.COLUMN)):
    GPIO.setup( keypad.COLUMN[j],GPIO.IN,pull_up_down=GPIO.PUD_UP)

print('Please enter your password : ')
#key=None
passward = ''
while True:
    key=getkey()  #Assigns the detected keyboard value to key
    if not key==None:  #If the key value is not null
        print (key)  #Displays the password entered
        passward = passward + key
        if(key == 'D'):
          print (passward)  #passward
          if(passward == "123D"): #set the password here
            print("open the door")
            p.ChangeDutyCycle(12.5)
            time.sleep(0.5)
            password = ''
          else:
            print("error")
            p.ChangeDutyCycle(2.5)
            time.sleep(0.5)
            passward = ''
        
p.stop()
GPIO.cleanup()
```



### Project 37：Intelligent Access Control System

Description：

The intelligent access control system is applied to many communities in China, the door can be open automatically when touching it with access key carrying RFID-RC522 module.

Components：

| ![image-20230423095718603](media/image-20230423095718603.png) | ![image-20230423095721909](media/image-20230423095721909.png) | ![image-20230423095724854](media/image-20230423095724854.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230423095729940](media/image-20230423095729940.png) | ![image-20230423095733860](media/image-20230423095733860.png) | ![image-20230423095736980](media/image-20230423095736980.png) |
| Breadboard*1                                                 | RFID-RC522 Module*1                                          | Access Key*1                                                 |
| ![image-20230423095740037](media/image-20230423095740037.png) | ![image-20230423095743140](media/image-20230423095743140.png) | ![image-20230423095749318](media/image-20230423095749318.png) |
| RFID Card*1                                                  | Servo Motor*1                                                | Jumper Wires                                                 |



**RFID-RC522 Module：**

Radio-frequency identification (RFID) uses electromagnetic fields to automatically identify and track tags attached to objects.

More details about c522 chip, you could look through chip specification folder.

a. Input sudo raspi-config in terminal，and press Enter to open the configuration page of Raspberry Pi.

![](media/4db419660d332deac1346539912b4072.png)

b. Activate the spi communication function according to the picture below.(Press（↑）, （↓）, （←）,（→) and“Enter”keys on keyboard).

![](media/dc81023253e5e95fc0f9052651d4d642.png)

![](media/3d258a0292c33db26900a472603c6a14.png)

![](media/a200c15da5c227cd2141b835996af7bc.png)

![](media/bdb501a9cd7fe98839b6c0d3231bcbc9.png)

![](media/31cdef3308f9d61b91c231a5104a86d1.png)

You could look through the SPI communication agreement in the following link.

<https://en.wikipedia.org/wiki/Serial_Peripheral_Interface>

**Install supporting library of Raspberry Pi（input in terminal）：**

sudo apt-get install python-spidev python3-spidev

Install **SPI-Py** library **(input command sentence by sentence in terminal):** git clone <https://github.com/lthiery/SPI-Py.git>

cd SPI-Py

git checkout 8cce26b9ee6e69eb041e9d5665944b88688fca68

sudo python setup.py install

sudo python3 setup.py install

Schematic Diagram：

![](media/934ac85ab85bb3765e275088105f6086.png)

![](media/e89b3cf1e50f9436a3c3bbd6c6dc9394.png)

Run Example Code1：

Input the following commands and press "Enter".

cd /home/pi/pythonCode_A/37_MFRC522-python

python Read.py

Test Result1：

Terminal prints card number, as shown below

![](media/cffc2777491a220c1ec2242541211d50.png)

Note: Press Ctrl + C on keyboard to exit code running

Example Code1：

```python
import RPi.GPIO as GPIO
import MFRC522
import signal

continue_reading = True

#Capture SIGINT for cleanup when the script is aborted
def end_read(signal,frame):
    global continue_reading
    print ("Ctrl+C captured, ending read.")
    continue_reading = False
    GPIO.cleanup()

#Hook the SIGINT
signal.signal(signal.SIGINT, end_read)

#Create an object of the class MFRC522
MIFAREReader = MFRC522.MFRC522()

#Welcome message
print ("Welcome to the MFRC522 data read example")
print ("Press Ctrl-C to stop.")

#This loop keeps checking for chips. If one is near it will get the UID and authenticate while continue_reading:
    

    # Scan for cards    
    (status,TagType) = MIFAREReader.MFRC522_Request(MIFAREReader.PICC_REQIDL)
    
    # If a card is found
    if status == MIFAREReader.MI_OK:
        print ("Card detected")
    
    # Get the UID of the card
    (status,uid) = MIFAREReader.MFRC522_Anticoll()
    
    # If we have the UID, continue
    if status == MIFAREReader.MI_OK:
    
        # Print UID
        print ("Card read UID: %s,%s,%s,%s" % (uid[0], uid[1], uid[2], uid[3]))
    
        # This is the default key for authentication
        key = [0xFF,0xFF,0xFF,0xFF,0xFF,0xFF]
        
        # Select the scanned tag
        MIFAREReader.MFRC522_SelectTag(uid)
    
        # Authenticate
        status = MIFAREReader.MFRC522_Auth(MIFAREReader.PICC_AUTHENT1A, 8, key, uid)
    
        # Check if authenticated
        if status == MIFAREReader.MI_OK:
            MIFAREReader.MFRC522_Read(8)
            MIFAREReader.MFRC522_StopCrypto1()
        else:
            print ("Authentication error")
  
```

Run Example Code2

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A/37_MFRC522-python

python 37_open_door.py

Test Result2：

Terminal will print“open the door”if the password of card is correct, otherwise, it will show error.

![](media/8ab5fd2cdec98dbb07871de5ec6672b9.png)

Note: Press Ctrl + C on keyboard to exit code running

Example Code2：

```python
import RPi.GPIO as GPIO
import MFRC522
import signal
import time

servo_min_angle = 2.5  #define pulse duty cycle for minimun angle of servo
servo_max_angle = 12.5  #define pulse duty cycle for maximun angle of servo
servopin = 18   #servo Pin
GPIO.setmode(GPIO.BCM)  #BCM numbers
GPIO.setup(servopin,GPIO.OUT)
p = GPIO.PWM(servopin,50)  #set 50Hz , The working frequency of the steering gear is 50Hz
p.start(0)  # start PWM
time.sleep(2)

continue_reading = True
read_card = ''
passward = "8301333"   #Change to your card number

#Capture SIGINT for cleanup when the script is aborted
def end_read(signal,frame):
    global continue_reading
    print ("Ctrl+C captured, ending read.")
    continue_reading = False
    GPIO.cleanup()

#Hook the SIGINT
signal.signal(signal.SIGINT, end_read)

#Create an object of the class MFRC522
MIFAREReader = MFRC522.MFRC522()

#Welcome message
print ("Welcome to the MFRC522 data read example")
print ("Press Ctrl-C to stop.")

#This loop keeps checking for chips. If one is near it will get the UID and authenticate
while continue_reading:
    p.ChangeDutyCycle(0)   #set 
    # Scan for cards    
    (status,TagType) = MIFAREReader.MFRC522_Request(MIFAREReader.PICC_REQIDL)

    # If a card is found
    if status == MIFAREReader.MI_OK:
        print ("Card detected")
    
    # Get the UID of the card
    (status,uid) = MIFAREReader.MFRC522_Anticoll()
    
    # If we have the UID, continue
    if status == MIFAREReader.MI_OK:
        # Print UID
        #print ("Card read UID: %s,%s,%s,%s" % (uid[0], uid[1], uid[2], uid[3]))
        read_card = str(uid[0]) + str(uid[1]) + str(uid[2]) + str(uid[3])  #Concatenates the card number into a string
        print ("Read card : ",read_card)
        if(read_card == passward):   #Here you need to change the password of the card you hold
            print("open the door")
            p.ChangeDutyCycle(12.5)
            time.sleep(0.5)
        else:
            print("error")
            p.ChangeDutyCycle(2.5)
            time.sleep(0.5)
        
        # This is the default key for authentication
        key = [0xFF,0xFF,0xFF,0xFF,0xFF,0xFF]
        
        # Select the scanned tag
        MIFAREReader.MFRC522_SelectTag(uid)
    
        # Authenticate
        status = MIFAREReader.MFRC522_Auth(MIFAREReader.PICC_AUTHENT1A, 8, key, uid)
    
        # Check if authenticated
        if status == MIFAREReader.MI_OK:
            MIFAREReader.MFRC522_Read(8)
            MIFAREReader.MFRC522_StopCrypto1()
        else:
            print ("Authentication error")

```



### Project 38：IR Remote Control

Description：

IR remote control is everywhere, for instance, remote control to TV. Next, let’s learn about its principle.

Components：

| ![image-20230423095841831](media/image-20230423095841831.png) | ![image-20230423095845206](media/image-20230423095845206.png) | ![image-20230423095847989](media/image-20230423095847989.png) | ![image-20230423095850758](media/image-20230423095850758.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 |
| ![image-20230423095854358](media/image-20230423095854358.png) | ![image-20230423095857318](media/image-20230423095857318.png) | ![image-20230423095900277](media/image-20230423095900277.png) | ![image-20230423095903990](media/image-20230423095903990.png) |
| IR Receiver *1                                               | 10KΩ Resistor*1                                              | Jumper Wires                                                 | IR Remote Control*1                                          |



Component Knowledge

**IR Remote Control：**

It transmits data via [near infrared](http://www.baidu.com/link?url=aNkRTZYAmLHj1hFJUhEcLH8YOilXkNj3vUYCfaPNohUbevu59PrKsi1OMt6x6uVYonOcAF0OnuEQ2Xm3M0UQXEGTYYmrlNBq4CLMXfW1W7adWDonnmbT_63l1sQ7taul) light. The wave length of [near infrared](http://www.baidu.com/link?url=aNkRTZYAmLHj1hFJUhEcLH8YOilXkNj3vUYCfaPNohUbevu59PrKsi1OMt6x6uVYonOcAF0OnuEQ2Xm3M0UQXEGTYYmrlNBq4CLMXfW1W7adWDonnmbT_63l1sQ7taul) light is 0.76um\~1.5um. However, IR remote control’s is 0.8um\~0.94um. It has the feature of high transmission efficiency and anti-interference.

IR Transmission Protocol: NEC Protocol

The emitting element is IR transmission tube, IR remote emits data in modulation way and adjust data to fixed carrier wave. The modulation emission has high anti-interference and long-distance transmission.

**IR Receiver：**

The integrated infrared receiver is used to integrate infrared receiving, amplification, filtering, comparator output and other functions to convert the received signal into a TTL signal that can be recognized by the MCU.

NEC Protocol：

-   8 bit address and 8 bit command length.

-   Extended mode available, doubling the address size.

-   Address and command are transmitted twice for reliability.

-   Pulse distance modulation.

-   Carrier frequency of 38kHz.

-   Bit time of 1.125ms or 2.25ms.

![](media/a2461ccc332a5a94425c5981863ccec3.png)

Notice from Figure 1 that it takes:

Send 9ms+4.5ms leading code firstly, then address, inverse, command and inverse.

The inverse code is used to verify and improve the accuracy of keys value.

The four bytes of data bits are each sent least significant bit first. Figure 1 illustrates the format of an NEC IR transmission frame, for an address of 00h (00000000b) and a command of ADh (10101101b).

![](media/2a8899cf0db571f7e2d1e55746237405.png)

The NEC protocol uses pulse distance encoding of the bits. Each pulse is a 562.5µs long 38kHz carrier burst (about 21 cycles). A logical "1" takes 2.25ms to transmit, while a logical "0" is only half of that, being 1.125ms. The recommended carrier duty-cycle is 1/4 or 1/3.

Logical‘0’– a 562.5µs pulse burst followed by a 562.5µs space, with a total transmit time of 1.125ms.   

Logical‘1’– a 562.5µs pulse burst followed by a 1.6875ms space, with a total transmit time of 2.25ms.

Note: a 562.5µs pulse and a 1.6875ms space combine 2.23ms, 562.5µs pulse is high level, therefore, the rest is low level.

Schematic Diagram：

![](media/98e6113f4f8c9a37aed94dbaaf0dfe2d.png)

![](media/9ad5a233ca111ffca8a10d12df1ca353.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 38_IR-remote.py

Test Result：

Terminal will display the corresponding key value when you point at IR reception and press keys of remote control.

Note: Press Ctrl + Z to exit the code running

Example Code：

```python
import RPi.GPIO as GPIO
import time

PIN = 24;

GPIO.setmode(GPIO.BCM)
GPIO.setup(PIN,GPIO.IN,GPIO.PUD_UP)
print("irm test start...")

def exec_cmd(key_val):
    if(key_val==0x46):
        print("Button up")
    elif(key_val==0x44):
        print("Button left")
    elif(key_val==0x40):
        print("Button ok")
    elif(key_val==0x43):
        print("Button right")
    elif(key_val==0x15):
        print("Button down")
    elif(key_val==0x16):
        print("Button 1")
    elif(key_val==0x19):
        print("Button 2")
    elif(key_val==0x0d):
        print("Button 3")
    elif(key_val==0x0c):
        print("Button 4")
    elif(key_val==0x18):
        print("Button 5")
    elif(key_val==0x5e):
        print("Button 6")
    elif(key_val==0x08):
        print("Button 7")
    elif(key_val==0x1c):
        print("Button 8")
    elif(key_val==0x5a):
        print("Button 9")
    elif(key_val==0x42):
        print("Button *")
    elif(key_val==0x52):
        print("Button 0")
    elif(key_val==0x4a):
        print("Button #")

try:
    while True:
        if GPIO.input(PIN) == 0:
            count = 0
            while GPIO.input(PIN) == 0 and count < 200:  # Wait for 9ms LOW level boot code and exit the loop if it exceeds 1.2ms
                count += 1
                time.sleep(0.00006)

            count = 0
            while GPIO.input(PIN) == 1 and count < 80:   # Wait for a 4.5ms HIGH level boot code and exit the loop if it exceeds 0.48ms
                count += 1
                time.sleep(0.00006)
    
            idx = 0  # byte count variable
            cnt = 0  #Variable per byte bit
            #There are 4 bytes in total. The first byte is the address code, the second is the address inverse code, 
            #the third is the control command data of the corresponding button, and the fourth is the control command inverse code
            data = [0,0,0,0]
            for i in range(0,32):  # Start receiving 32BITE data
                count = 0
                while GPIO.input(PIN) == 0 and count < 15:  # Wait for the LOW LOW level of 562.5US to pass and exit the loop if it exceeds 900US
                    count += 1
                    time.sleep(0.00006)
    
                count = 0
                while GPIO.input(PIN) == 1 and count < 40:  # waits for logical HIGH level to pass and exits the loop if it exceeds 2.4ms
                    count += 1
                    time.sleep(0.00006)
                
                # if count>8, that is, the logical time is greater than 0.54+0.562=1.12ms, that is, 
                #the period is greater than the logical 0 period, that is equivalent to receiving logical 1
                if count > 8:   
                    data[idx] |= 1<<cnt    #When idx=0 is the first data  data[idx] = data[idx] | 1<<cnt   00000001 <<1 == 0000 0010
                if cnt == 7:    #With 8 byte
                    cnt = 0     #Displacement qing 0
                    idx += 1    #Store the next data
                else:
                    cnt += 1   #The shift adds 1
            #Determine whether address code + address inverse code =0xff, control code + control inverse code = 0xFF
            if data[0]+data[1] == 0xFF and data[2]+data[3] == 0xFF:  
                 print("Get the key: 0x%02x" %data[2])  #Data [2] is the control code we need
                 exec_cmd(data[2])

except KeyboardInterrupt:
    GPIO.cleanup()
```



### Project 39：IR Remote Controlled LED

Components：

| ![image-20230423100108654](media/image-20230423100108654.png) | ![image-20230423100111863](media/image-20230423100111863.png) | ![image-20230423100114680](media/image-20230423100114680.png) | ![image-20230423100117607](media/image-20230423100117607.png) | ![image-20230423100120679](media/image-20230423100120679.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               | Breadboard*1                                                 | IR Receiver *1                                               |
| ![image-20230423100125160](media/image-20230423100125160.png) | ![image-20230423100128056](media/image-20230423100128056.png) | ![image-20230423100131719](media/image-20230423100131719.png) | ![image-20230423100134536](media/image-20230423100134536.png) | ![image-20230423100138007](media/image-20230423100138007.png) |
| 10KΩ Resistor*1                                              | 220Ω Resistor * 1                                            | Jumper Wires                                                 | IR Remote Control*1                                          | LED - Red *1                                                 |



Schematic Diagram：

![](media/4be329bc8120c44a87db539272266f99.png)

![](media/c7f5a14685ecfed1826647284fe127b8.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 39_IR-remote-LED.py

Test Result：

LED will turn on when pressing“forward”button and it will be off when pressing“OK”key.

![](media/a7c50c5e0093e77b193918f864a92ec6.png)

Note: Press Ctrl + Z to exit the code running

Example Code：

```python
import RPi.GPIO as GPIO
import time

PIN = 24;  #Infrared receiving pin

GPIO.setmode(GPIO.BCM)
GPIO.setup(PIN,GPIO.IN,GPIO.PUD_UP)

ledPin = 25  #define led pin
GPIO.setup(ledPin,GPIO.OUT)   #set the ledPin OUTPUT mode
GPIO.output(ledPin,GPIO.LOW)  # make ledPin output LOW level
print("irm test start...")

def exec_cmd(key_val):
    if(key_val==0x46):
        print("Button up")
    elif(key_val==0x44):
        print("Button left")
    elif(key_val==0x40):
        print("Button ok")
    elif(key_val==0x43):
        print("Button right")
    elif(key_val==0x15):
        print("Button down")
    elif(key_val==0x16):
        print("Button 1")
    elif(key_val==0x19):
        print("Button 2")
    elif(key_val==0x0d):
        print("Button 3")
    elif(key_val==0x0c):
        print("Button 4")
    elif(key_val==0x18):
        print("Button 5")
    elif(key_val==0x5e):
        print("Button 6")
    elif(key_val==0x08):
        print("Button 7")
    elif(key_val==0x1c):
        print("Button 8")
    elif(key_val==0x5a):
        print("Button 9")
    elif(key_val==0x42):
        print("Button *")
    elif(key_val==0x52):
        print("Button 0")
    elif(key_val==0x4a):
        print("Button #")

try:
    while True:
        if GPIO.input(PIN) == 0:
            count = 0
            while GPIO.input(PIN) == 0 and count < 200:  # Wait for 9ms LOW level boot code and exit the loop if it exceeds 1.2ms
                count += 1
                time.sleep(0.00006)

            count = 0
            while GPIO.input(PIN) == 1 and count < 80:   # Wait for a 4.5ms HIGH level boot code and exit the loop if it exceeds 0.48ms
                count += 1
                time.sleep(0.00006)
    
            idx = 0  # byte count variable
            cnt = 0  #Variable per byte bit
            #There are 4 bytes in total. The first byte is the address code, the second is the address inverse code, 
            #the third is the control command data of the corresponding button, and the fourth is the control command inverse code
            data = [0,0,0,0]
            for i in range(0,32):  # Start receiving 32BITE data
                count = 0
                while GPIO.input(PIN) == 0 and count < 15:  # Wait for the LOW LOW level of 562.5US to pass and exit the loop if it exceeds 900US
                    count += 1
                    time.sleep(0.00006)
    
                count = 0
                while GPIO.input(PIN) == 1 and count < 40:  # waits for logical HIGH level to pass and exits the loop if it exceeds 2.4ms
                    count += 1
                    time.sleep(0.00006)
                
                # if count>8, that is, the logical time is greater than 0.54+0.562=1.12ms, that is, 
                #the period is greater than the logical 0 period, that is equivalent to receiving logical 1
                if count > 8:   
                    data[idx] |= 1<<cnt    #When idx=0 is the first data  data[idx] = data[idx] | 1<<cnt   00000001 <<1 == 0000 0010
                if cnt == 7:    #With 8 byte
                    cnt = 0     #Displacement qing 0
                    idx += 1    #Store the next data
                else:
                    cnt += 1   #The shift adds 1
            #Determine whether address code + address inverse code =0xff, control code + control inverse code = 0xFF
            if data[0]+data[1] == 0xFF and data[2]+data[3] == 0xFF:  
                 print("Get the key: 0x%02x" %data[2])  #Data [2] is the control code we need
                 exec_cmd(data[2])
                 if(data[2] == 0x46):
                     GPIO.output(ledPin,GPIO.HIGH)  #turn on led
                     print("turn on led")
                 if(data[2] == 0x40):
                     GPIO.output(ledPin,GPIO.LOW)  #turn off led
                     print("turn on led")

except KeyboardInterrupt:
    GPIO.cleanup()
```



### Project 40：Smart Home Kit

Description：

![](media/3df5c42c7b5e3983fb07a4a43a2633d9.jpeg)

This Smart Home Learning Kit based on the Arduino platform is newly-issued by Keyestudio DIY Robot Co. Ltd. It's meant for those who dream of making people's lives more comfortable using technology.

Envision and build a remotely-operated smart home, and control its systems with your phone or computer, even when you're out.

Turn on the air conditioning, boot up the water heater, secure your home with an electronic lock, and set your LED lights and smart curtains to turn on automatically when you get home, conserving electricity for only when its use will be appreciated.

The intelligent lighting system allows you to choose from a variety of preset lighting scenes to create a comfortable, tranquil atmosphere. And you can create these presets easily via the controller app.

Components：

| ![image-20230423100248656](media/image-20230423100248656.png) | ![image-20230423100252233](media/image-20230423100252233.png) | ![image-20230423100255177](media/image-20230423100255177.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Raspberry Pi*1                                               | GPIO Extension Board*1                                       | 40 pin Colorful Jumper Wires*1                               |
| ![image-20230423100304810](media/image-20230423100304810.png) | ![image-20230423100308250](media/image-20230423100308250.png) | ![image-20230423100315209](media/image-20230423100315209.png) |
| Breadboard*1                                                 | IR Receiver *1                                               | Jumper Wires                                                 |
| ![image-20230423100341674](media/image-20230423100341674.png) | ![image-20230423100344730](media/image-20230423100344730.png) | ![image-20230423100347594](media/image-20230423100347594.png) |
| 10KΩResistor*1                                               | 100Ω Resistor * 3                                            | IR Remote Control*1                                          |
| ![image-20230423100355466](media/image-20230423100355466.png) | ![image-20230423100404905](media/image-20230423100404905.png) | ![image-20230423100408185](media/image-20230423100408185.png) |
| RGB Light*1                                                  | L293D Chip *1                                                | Servo Motor*1                                                |
| ![image-20230423100416986](media/image-20230423100416986.png) | ![image-20230423100419802](media/image-20230423100419802.png) |                                                              |
| Relay Module*1                                               | Motor*1                                                      |                                                              |



Schematic Diagram：

![](media/d5c2cc28feff01f61a516bcf34af7dc3.png)

![](media/c93914cd0d11cbde1eb6ade3e8249cd2.png)

Run Example Code：

Input the following commands and press "Enter"

cd /home/pi/pythonCode_A

python 40_IR-remote-All.py

Test Result：

![](media/05fe27d8ca12c08541f02b6c218e88ea.png)：DC motor rotate clockwise

![](media/5117519b77db00e38801bb3887faadcb.png)：DC motor rotate anticlockwise

ok： DC motor stops

![](media/488c54f39589a60a8825173b86ad07b3.png)：DC motor speeds up （need to press left or right button again)

![](media/829b5b4e2ef4ca7720fc3de78d34b757.png)：DC motor speeds down （need to press left or right button again)

1\~6：Control RGB light

8：Turn off RGB light

7：Open relay module

9：Turn off relay module

\*：Servo rotates clockwise 10 degree

\#：Servo rotates anticlockwise 10 degree

Note: Press Ctrl + Z to exit the code running

Example Code：

```python
import RPi.GPIO as GPIO
import time

PIN = 24;  #Infrared receiving pin

GPIO.setmode(GPIO.BCM)

GPIO.setup(PIN,GPIO.IN,GPIO.PUD_UP)

ledPin = 25  #define led pin
GPIO.setup(ledPin,GPIO.OUT)   #set the ledPin OUTPUT mode
GPIO.output(ledPin,GPIO.LOW)  # make ledPin output LOW level
#define RGB pin
pin_R = 21
pin_G = 20
pin_B = 16

relayPin = 12   #define relay pin

#define L293D pin
INA1 = 17
INA2 = 27
ENA = 22
global speed
speed = 60

#set the RGB Pin OUTPUT mode
GPIO.setup(pin_R,GPIO.OUT)
GPIO.setup(pin_G,GPIO.OUT)
GPIO.setup(pin_B,GPIO.OUT)
#set pwm frequence to 1000hz
pwm_R = GPIO.PWM(pin_R,100)
pwm_G = GPIO.PWM(pin_G,100)
pwm_B = GPIO.PWM(pin_B,100)
#set inital duty cycle to 0
pwm_R.start(0)
pwm_G.start(0)
pwm_B.start(0)

GPIO.setup(relayPin,GPIO.OUT)
GPIO.output(relayPin,GPIO.LOW)

servo_min_angle = 2.5  #define pulse duty cycle for minimun angle of servo
servo_max_angle = 12.5  #define pulse duty cycle for maximun angle of servo
servopin = 26   #servo Pin
GPIO.setup(servopin,GPIO.OUT)
p = GPIO.PWM(servopin,50)  #set 50Hz , The working frequency of the steering gear is 50Hz
p.start(0)  # start PWM
global angle
angle = 0
time.sleep(0.5)

GPIO.setup(INA1,GPIO.OUT)
GPIO.setup(INA2,GPIO.OUT)
GPIO.setup(ENA,GPIO.OUT)
pwmA = GPIO.PWM(ENA,100)  #create a PWM instance
pwmA.start(0)   #start PWM

print("irm test start...")

#motor forward
def forward():
    GPIO.output(INA1,GPIO.HIGH)
    GPIO.output(INA2,GPIO.LOW)
    pwmA.ChangeDutyCycle(speed)
    
def back():
    GPIO.output(INA1,GPIO.LOW)
    GPIO.output(INA2,GPIO.HIGH)
    pwmA.ChangeDutyCycle(speed)
    
def stop():
    pwmA.ChangeDutyCycle(0)
    
#function. receive the value to display different colors
def setColor(val_R,val_G,val_B):
    pwm_R.ChangeDutyCycle(val_R)
    pwm_G.ChangeDutyCycle(val_G)
    pwm_B.ChangeDutyCycle(val_B)
    
#define function, map a value from one range to another range
def map(angle, val1, val2, min_angle, max_angle):
    return (max_angle-min_angle)*(angle-val1)/(val2-val1)+min_angle

def exec_cmd(key_val):
    if(key_val==0x46):
        print("Button up")
    elif(key_val==0x44):
        print("Button left")
    elif(key_val==0x40):
        print("Button ok")
    elif(key_val==0x43):
        print("Button right")
    elif(key_val==0x15):
        print("Button down")
    elif(key_val==0x16):
        print("Button 1")
    elif(key_val==0x19):
        print("Button 2")
    elif(key_val==0x0d):
        print("Button 3")
    elif(key_val==0x0c):
        print("Button 4")
    elif(key_val==0x18):
        print("Button 5")
    elif(key_val==0x5e):
        print("Button 6")
    elif(key_val==0x08):
        print("Button 7")
    elif(key_val==0x1c):
        print("Button 8")
    elif(key_val==0x5a):
        print("Button 9")
    elif(key_val==0x42):
        print("Button *")
    elif(key_val==0x52):
        print("Button 0")
    elif(key_val==0x4a):
        print("Button #")

try:
    while True:
        if GPIO.input(PIN) == 0:
            count = 0
            while GPIO.input(PIN) == 0 and count < 200:  # Wait for 9ms LOW level boot code and exit the loop if it exceeds 1.2ms
                count += 1
                time.sleep(0.00006)

            count = 0
            while GPIO.input(PIN) == 1 and count < 80:   # Wait for a 4.5ms HIGH level boot code and exit the loop if it exceeds 0.48ms
                count += 1
                time.sleep(0.00006)
    
            idx = 0  # byte count variable
            cnt = 0  #Variable per byte bit
            #There are 4 bytes in total. The first byte is the address code, the second is the address inverse code, 
            #the third is the control command data of the corresponding button, and the fourth is the control command inverse code
            data = [0,0,0,0]
            for i in range(0,32):  # Start receiving 32BITE data
                count = 0
                while GPIO.input(PIN) == 0 and count < 15:  # Wait for the LOW LOW level of 562.5US to pass and exit the loop if it exceeds 900US
                    count += 1
                    time.sleep(0.00006)
    
                count = 0
                while GPIO.input(PIN) == 1 and count < 40:  # waits for logical HIGH level to pass and exits the loop if it exceeds 2.4ms
                    count += 1
                    time.sleep(0.00006)
                
                # if count>8, that is, the logical time is greater than 0.54+0.562=1.12ms, that is, 
                #the period is greater than the logical 0 period, that is equivalent to receiving logical 1
                if count > 8:   
                    data[idx] |= 1<<cnt    #When idx=0 is the first data  data[idx] = data[idx] | 1<<cnt   00000001 <<1 == 0000 0010
                if cnt == 7:    #With 8 byte
                    cnt = 0     #Displacement qing 0
                    idx += 1    #Store the next data
                else:
                    cnt += 1   #The shift adds 1
            #Determine whether address code + address inverse code =0xff, control code + control inverse code = 0xFF
            if data[0]+data[1] == 0xFF and data[2]+data[3] == 0xFF:  
                print("Get the key: 0x%02x" %data[2])  #Data [2] is the control code we need
                exec_cmd(data[2])
                 
                if(data[2] == 0x44):
                    forward()
                    print("motor run")
                if(data[2] == 0x43):
                    back()
                    print("motor back")
                if(data[2] == 0x40):
                    stop()
                    print("motor stop")
                if(data[2] == 0x46):
                    speed = speed + 10
                    if(speed >= 100):
                        speed = 99
                    print("speed add 10")
                if(data[2] == 0x15):
                    speed = speed - 10
                    if(speed <= 50):
                        speed = 50
                    print("speed subtract 10")
    
                if(data[2] == 0x16):
                    setColor(100,0,0)
                if(data[2] == 0x19):
                    setColor(0,100,0)
                if(data[2] == 0x0d):
                    setColor(0,0,100)
                if(data[2] == 0x0c):
                    setColor(100,100,0)
                if(data[2] == 0x18):
                    setColor(0,100,100)
                if(data[2] == 0x5e):
                    setColor(100,100,100)
                if(data[2] == 0x1c):
                    setColor(0,0,0)
    
                if(data[2] == 0x08):
                    GPIO.output(relayPin,GPIO.HIGH)  #Starting relay
                if(data[2] == 0x5a):
                    GPIO.output(relayPin,GPIO.LOW)
                if(data[2] == 0x42):
                    p.ChangeDutyCycle(0)
                    angle = angle + 10
                    if(angle >= 180):
                        angle = 180
                    c = map(angle, 0, 180, servo_min_angle, servo_max_angle)  #map angle from 0~180 to 2.5~12.5
                    p.ChangeDutyCycle(c) 
                    time.sleep(0.01)
                if(data[2] == 0x4a):
                    p.ChangeDutyCycle(0)
                    angle = angle - 10
                    if(angle <= 0):
                        angle = 0
                    c = map(angle, 0, 180, servo_min_angle, servo_max_angle)  #map angle from 0~180 to 2.5~12.5
                    p.ChangeDutyCycle(c) 
                    time.sleep(0.01)

except KeyboardInterrupt:
    GPIO.cleanup()
```

