const int BUTTON = 5;
const int LED = 3;
const int THRESHOLD = 60;   // variable used to check high temperature
const int BUZZER = 8;

boolean currentState = LOW;       
boolean previousState = LOW;             

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  pinMode(BUTTON, INPUT);
  pinMode(LED, OUTPUT);
  Serial.println("t for temperature, l for lightness");
}

// Create a function to do debouncing of the button
boolean debounce(boolean last){
  boolean current = digitalRead(BUTTON);
  if (last != current){
    delay(5);
    current = digitalRead(BUTTON);
    return current;
  }
}
// Create a functio to activate alarm if threshold is reached
int AlarmOn(boolean state, int thermoVar) {   
    while (thermoVar >= THRESHOLD && state == true){
        digitalWrite(LED, HIGH);
        delay(500);
        digitalWrite(LED, LOW);
        delay(500);
        tone(BUZZER, 4000, 500);
  }
}

void loop() {
  // put your main code here, to run repeatedly:
    
    int photoVar = analogRead(A2);  // Read photoresistor value
    int thermoVar = analogRead(A0);  // Read thermoresistor value

    if (Serial.available() > 0){
      char mode = Serial.read();
      if (mode == 't' || mode == 'T'){
        Serial.print("Thermoresistor value: " );
        Serial.println(thermoVar);
      }else if (mode == 'l' || mode == 'L'){
        Serial.print("Photoresistor value: "); 
        Serial.println(photoVar);
      }else{
        Serial.println("Please enter valid input!");
      }
    }
    
    currentState = debounce(BUTTON);
    if (previousState == false && currentState == true){    // if it was pressed
      Serial.println("Button is pressed, Alarm activated!");
      AlarmOn(currentState, thermoVar);
    }
    previousState = currentState;
}
