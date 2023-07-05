# Gesture Controlled Rover
My project is the Gesture Controlled Rover. This remote controlled rover . It uses bluetooth to allow the phone to communicate with Arduino through an app.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Devan G | Marin Academy | Electrical Engineering | Rising Freshman 

![Headstone Image](https://raw.githubusercontent.com/BlueStampEng/BSE_Template_Portfolio/de8633f62b5da2234992a0178a6a72fd6df7e7e1/branding/BlueStamp-Logo.svg)

<img src="IMG_0426.jpg" width="400" height="400" />

# Project Picture
<img src="IMG_0635.jpg" width="300" height="400" />

# Project Video 
<iframe width="690" height="388.125" src="https://www.youtube.com/embed/geb_Qh8xRIo" title="Devan Demo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Final Milestone
My final milestone was my modification. I choose to make my app better so that the controls wouldn't be as jerky. I tried to approach this in many ways such as using a clock. This however did not work because it would just get stuck in a loop. My second way of making my app better was sliders. Originally, I was going to send the slider location and the character for the motor to rotate but it ended up not working because the arduino couldn't interpret it. I fixed this by rounding the thumb position and sending it in a 1 byte number along with rewiring the HC-06 bluetooth module and changing my arduino code.

<iframe width="690" height="388.125" src="https://www.youtube.com/embed/HeM0xD3lTdw" title="Devan G Milestone 3" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Second Milestone
My second milestone was controlling my arm with my app. One of the challenges I faced while completing this milestone was that the phone that I received has andriod 11 but the app that came with the kit was ment for Android 10. I ended up making my own app using MIT App Inventor which solved the errors that I encountered. It would send characters to the arduino which would then interpret them and initate the motor correspondingly. However this app was still in the testing mode so all of the controls are quite jerky. My next step is my modifications.

<iframe width="690" height="388.125" src="https://www.youtube.com/embed/o-gyQRcRt54" title="Devan G Milestone 2" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# First Milestone
My first milestone was assembling my arm and connecting it to my Arduino. I recieved my pieces in the Lafvin 4DOF Smart Robot Mechanical Arm Kit and then built them using the guide that came with the kit. I had some trouble with screwing in screws into the servo flaps and screwing in lock nuts but I solved it by using a different screwdriver than what was in the box and also using a wrench to keep the lock nut in place while I screwed it in. Eventually I finished assembling my arm except that when I was getting the parts out of the kit, one of the parts broke so currently my claw is disconected from the rest of my arm. My next step is to connect my arm to bluetooth and then connect it to my phone.

<iframe width="690" height="388.125" src="https://www.youtube.com/embed/DGngI1tAAQ4" title="Devan G Milestone 1" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Bill of Materials

| **Item** | **Quanity** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Lavfin Robot Arm Kit | 1 | 35 USD | <a href="https://www.amazon.com/LAFVIN-Acrylic-Mechanical-Compatible-Tutorial/dp/B07ZYZVNY4"> Amazon </a> 
| Moto G Pure| 1 | 60 USD | <a href="https://www.amazon.com/Tracfone-Motorola-moto-Pure-32GB/dp/B09NWDJQ78/ref=sr_1_5?keywords=moto+g+pure&qid=1660325878&sr=8-5"> Amazon </a>

# Useful Links and Tips

<a href="https://drive.google.com/drive/folders/1t8ZgGRvJrYYbfawNBiJ6xqhWS9MYxiCA?usp=sharing"> Go to Drive File </a>

Tips:
Use a different screwdriver than the one that came in the kit.
Be careful when taking out the acrylic parts from the sheet.
Don't be discouraged.
Look up tutorials if you are stuck.

# Schematics

<img src="heh.jpg" width="600" height="400" />

# App

<a href="https://drive.google.com/file/d/1ETSv9KrbHGWk9k7-pq5Kp8rx9XUdQWC4/view?usp=sharing"> Go to Drive File </a>

# Code

```Arduino
#include <SoftwareSerial.h>
#include <Servo.h>  
Servo myservo1;  
Servo myservo2;
Servo myservo3;
Servo myservo4;
SoftwareSerial hc06(2,1);
int pos1=90, pos2=90, pos3=90, pos4=80, pos5=0, pos6=80;  
char val;
int incomingByte = 0;          
String inputString = "";     
int angle = 0;  
boolean newLineReceived = false;
boolean startBit  = false; 
int num_reveice=0;
void setup()
{
  myservo1.write(pos1);  
  delay(1000);
  myservo2.write(pos2);
  myservo3.write(pos3);
  myservo4.write(pos4);
  delay(1500);
  Serial.begin(9600); 
  hc06.begin(9600);
}

void loop() 
{
  myservo1.attach(3);  // set the control pin of servo 1 to D3
  myservo2.attach(5);  // set the control pin of servo 2 to D5
  myservo3.attach(6);   // set the control pin of servo 3 to D6
  myservo4.attach(9);   // set the control pin of servo 4 to D9

  if (hc06.available()) {
    inputString = hc06.readStringUntil('#');
    delay(10);
    angle = hc06.read();
    switch(inputString[1]) {
      case 'A':  Serial.println(angle); myservo2.write(angle); delay(100); break;// the lower arm will draw back 
      case '7':  Serial.println(angle); myservo3.write(angle); delay(100); break;
      case 'C':  Serial.println(angle); myservo1.write(angle); delay(100); break;
      case '5':  ZK();  break;//open the claw
      case '6':  ZB();  break;//close the claw
      default:break;
    }
  }
  }

  void ZK()
{
  
      Serial.println(pos6);
      myservo4.write(pos6);
      delay(5);

}

void ZB()
{
      Serial.println(pos5);
      myservo4.write(pos5);
      delay(5);
}
```
