# ON-OFF-System
![on off](https://user-images.githubusercontent.com/108452991/181660954-155bc56d-972b-45ad-a125-9f11d3190ec8.png)
here is the design of on off system by tinkercad try it https://www.tinkercad.com/things/fs6cmP3stY1
which made of these components.
1.push button 
2.led, 
3.resistor
4.arduino uno 
5.breadboard
----------------------------------------------------------------------------------------------------------------------
To make the project work as expected use this code which solve the bounce problem follow the comments to understand it.
int ledpin = 4;// a pin for the LED
int  pushbuttonpin = 2; //a pin for the pushbutton
int ledstate = LOW;// saving LED state (LOW or HIGH)means on or off
int debouncedelay = 50;//Delay time for bouncing period
int lastbuttonstate = LOW;//Saving the last button state
int buttonstate = LOW;//Saving the current button state
unsigned long lastdebouncetime = 0;//Saving the last time for state change

void setup(){ 
 Serial.begin(9600);//This starts serial communication, so that the Arduino can send out commands through the USB connection. 
 pinMode(ledpin,OUTPUT);//define ledpin as an output 
 pinMode(pushbuttonpin,INPUT);//define pushbuttonpin as an input
}
void loop() {
  ButtonDebounce();//calling  ButtonDebounce function this function to solve bounce problem to learn more
  //about it visit the site 
  //https://circuitdigest.com/electronic-circuits/what-is-switch-bouncing-and-how-to-prevent-it-using-debounce-circuit
 
}

void ButtonDebounce(){
  int readbutton = digitalRead(pushbuttonpin);// Read the button state
  //If the state has changed from the last state, start the timer
  if(lastbuttonstate != readbutton)
  {
    lastdebouncetime = millis();
  }
  //Wait for debouncedelay=50ms to have a stable state
  if(millis() - lastdebouncetime > debouncedelay)
  {
   //Save the actual reading and when
   // the state is HIGH means Button has been pressed change the led state
   if(buttonstate!=readbutton) 
   {
     buttonstate = readbutton;
     if(buttonstate == HIGH)
     {
       ledstate = !ledstate;
       Serial.println(ledstate);//print the led state if 0=low and if 1=high
       
     }
   }
  }
  //Write the ledstate and save the last button read
  digitalWrite(ledpin,ledstate);
  lastbuttonstate = readbutton;
  }
  
  
  
  to see the output click on the Serial monitor if the led (on) you will see 1 otherwise it will be 0 which mean the led is (off).
