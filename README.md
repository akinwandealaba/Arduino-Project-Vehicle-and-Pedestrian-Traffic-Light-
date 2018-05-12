# // Arduino-Project-Vehicle-and-Pedestrian-Traffic-Light-
# // I am new in the block and this is my first project to be uploaded here

# #define BUTTON_PIN 2 // Pin of Traffic Button for Pedestrain
# #define G_LED 10     // Pin of Green traffic light for vehicle
# #define Y_LED 11     // Pin of Yellow traffic light for vehicle
# #define R_LED 12     // Pin of Red traffic light for vehicle
# #define G_PEDST_LED 8   //Pin of Green Traffic light for Pedestrain
# #define R_PEDST_LED 9    //Pin of Red Traffic light for Pedestrain


# //flag for interrupt (state: signal from traffic button for pedestrain initially set as LOW = 0) 
# volatile int state = 0;    


# void setup() {
#   // put your setup code here, to run once:
# Serial.begin(9600);    //initiates serial communication between my Computer and Arduino

# // set input and output modes for pins used
# pinMode(BUTTON_PIN,INPUT); 
# pinMode(G_LED,OUTPUT);
# pinMode(Y_LED,OUTPUT);
# pinMode(R_LED,OUTPUT);
# pinMode(G_PEDST_LED,OUTPUT);
# pinMode(R_PEDST_LED,OUTPUT);

# // attach an interrupt to detect signal change in Traffic Push button
# //i.e. Rising signal - change of state from 0 t 1
# attachInterrupt(digitalPinToInterrupt(2),IntrSub,RISING);
# }

# void loop() {
#  // put your main code here, to run repeatedly:

# digitalWrite(R_PEDST_LED,HIGH); //
# digitalWrite(R_LED,HIGH);
# delay(1000);
# // performs this routine when interrupt signal is detected
# //(i.e button is pressed by pedestrian)
# if(state == 1) {
#  delay(1000);
# digitalWrite(R_PEDST_LED,LOW);
# digitalWrite(G_PEDST_LED,HIGH);
#  delay(12000); //Note longer time here for pedestrain to cross the road
#  digitalWrite(G_PEDST_LED,LOW);
#  digitalWrite(R_PEDST_LED,HIGH);
# state = 0;
# }
# // or performs this routine when traffic light for
# //vehicle turns red without pressing the pedestrain button
# else if(digitalRead(R_LED) == HIGH) {
#  delay(1000);
#  digitalWrite(R_PEDST_LED,LOW);
# digitalWrite(G_PEDST_LED,HIGH);
#  delay(6000); //Note shorter time here cos this happens without pressing the pedestrain button
#  digitalWrite(G_PEDST_LED,LOW);
#  digitalWrite(R_PEDST_LED,HIGH);
# }

# digitalWrite(Y_LED,HIGH);
# delay(3000);
# digitalWrite(R_LED,LOW);
# digitalWrite(Y_LED,LOW);
# digitalWrite(G_LED,HIGH);
# delay(4000);
# digitalWrite(G_LED,LOW);
# digitalWrite(Y_LED,HIGH);
# delay(1000);
# digitalWrite(Y_LED,LOW);
# //digitalWrite(R_PEDST_LED,HIGH);
# }


# //This is the interrupt subroutine function that detects 
# //the change of signal ("State" variable declared earlier)
# void IntrSub(){
#  state = 1;
#  Serial.println("Pushed"); //Just a message printed on the Serial Monitor whenever the pedestrain button is pressed
# }
