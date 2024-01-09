# Arduino-car-parking
As the world becomes increasingly urbanized, parking has become a major challenge for city residents and visitors. The ever-increasing number of vehicles on the road has resulted in limited parking spaces and increased traffic congestion. As a result, there is a growing need for advanced parking systems that can efficiently manage parking spaces.

The Arduino platform has gained popularity in recent years due to its versatility and affordability. With its open-source hardware and software, it has become a go-to platform for developers to create innovative solutions for a wide range of applications. In the context of parking systems, Arduino can be used to develop advanced parking solutions that are efficient, reliable, and cost-effective.

In this report, we will discuss the development of an advanced parking system using Arduino. The system will use a combination of sensors, microcontrollers, and communication devices to provide real-time information about the availability of parking spaces. The system will be designed to be user-friendly, easily scalable, and customizable to suit the needs of different parking facilities.

We will begin by discussing the various components of the system and how they work together to provide real-time parking information. We will also discuss the design considerations, such as power consumption, communication protocols, and data storage, that were taken into account during the development of the system.

Finally, we will discuss the potential benefits of the advanced parking system, such as reduced traffic congestion, improved user experience, and increased revenue for parking facilities. We hope that this report will provide insights into the potential of Arduino in developing advanced parking systems and inspire further research and development in this field


# HARDWARE REQUIRED 
Types of components required-   
a)	Arduino uno 
b)	LCD display
c)	IR Sensor
d)	Connecting wires 
e)	Servo Motor (SG 90)


#  SOFTWARE REQUIRED
a) Arduino ide 

# ALGORITHM
 #include <Servo.h> //includes the servo library
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27, 16, 2);

Servo myservo;

#define ir_enter 2
#define ir_back  4

#define ir_car1 5
#define ir_car2 6
#define ir_car3 7
#define ir_car4 8
#define ir_car5 9
#define ir_car6 10

int S1=0, S2=0, S3=0, S4=0, S5=0, S6=0;
int flag1=0, flag2=0; 
int slot = 6;  

void setup(){
Serial.begin(9600);

pinMode(ir_car1, INPUT);
pinMode(ir_car2, INPUT);
pinMode(ir_car3, INPUT);
pinMode(ir_car4, INPUT);
pinMode(ir_car5, INPUT);
pinMode(ir_car6, INPUT);

pinMode(ir_enter, INPUT);
pinMode(ir_back, INPUT);
  
myservo.attach(3);
myservo.write(90);

lcd.begin(20, 4);  
lcd.setCursor (0,1);
lcd.print("    Car  parking  ");
lcd.setCursor (0,2);
lcd.print("       System     ");
delay (2000);
lcd.clear();   
Read_Sensor();

int total = S1+S2+S3+S4+S5+S6;
slot = slot-total; 
}

void loop(){

Read_Sensor();

lcd.setCursor (0,0);
lcd.print("   Have Slot: "); 
lcd.print(slot);
lcd.print("    ");  

lcd.setCursor (0,1);
if(S1==1){lcd.print("S1:Fill ");}
     else{lcd.print("S1:Empty");}
lcd.setCursor (10,1);
if(S2==1){lcd.print("S2:Fill ");}
     else{lcd.print("S2:Empty");}

lcd.setCursor (0,2);
if(S3==1){lcd.print("S3:Fill ");}
     else{lcd.print("S3:Empty");}

lcd.setCursor (10,2);
if(S4==1){lcd.print("S4:Fill ");}
     else{lcd.print("S4:Empty");}

 lcd.setCursor (0,3);
if(S5==1){lcd.print("S5:Fill ");}
     else{lcd.print("S5:Empty");}

lcd.setCursor (10,3);
if(S6==1){lcd.print("S6:Fill ");}
     else{lcd.print("S6:Empty");}    

if(digitalRead (ir_enter) == 0 && flag1==0){
if(slot>0){flag1=1;
if(flag2==0){myservo.write(180); slot = slot-1;}
}else{
lcd.setCursor (0,0);
lcd.print(" Sorry Parking Full ");  
delay(1500);
}   
}

if(digitalRead (ir_back) == 0 && flag2==0){flag2=1;
if(flag1==0){myservo.write(180); slot = slot+1;}
}

if(flag1==1 && flag2==1){
delay (1000);
myservo.write(90);
flag1=0, flag2=0;
}

delay(1);
}

void Read_Sensor(){
S1=0, S2=0, S3=0, S4=0, S5=0, S6=0;

if(digitalRead(ir_car1) == 0){S1=1;}
if(digitalRead(ir_car2) == 0){S2=1;}
if(digitalRead(ir_car3) == 0){S3=1;}
if(digitalRead(ir_car4) == 0){S4=1;}
if(digitalRead(ir_car5) == 0){S5=1;}
if(digitalRead(ir_car6) == 0){S6=1;}  
}


# FUTURE SCOPE

a
a) Renewable energy sources: Explore the use of renewable energy sources, such as solar or wind power, to power the parking system. This can help reduce the carbon footprint of the parking lot and make it more sustainable.

b) Integration with public transportation: Integrate the parking system with public transportation systems, such as bus or train stations, to create a more seamless transportation experience. This can help reduce traffic congestion and improve the overall transportation infrastructure.

