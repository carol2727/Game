/* Sends the analog input on A0 and A1 as comma separated keyboard values, which can be read
 * in by a program running on the computer (including p5js). For example, if A0 is 283
 * and A1 is 768, this sketch will "press" the following keys in sequence:
 *   2
 *   8
 *   3
 *   ,
 *   7
 *   6
 *   8
 *   \n 
 * Which can then be parsed by a computer program running on your laptop/computer.
 * 
 * Note: the keyboard starts in OFF mode so as not to write random text all over the place.
 * You can enable it by pressing a toggle button hooked up to pin 2 (with a pull-up configuration).
 * 
 * As an example, run this sketch on your Arduino, then check out the 'Analog Keyboard' 
 * p5js sketch: 
 *  - https://editor.p5js.org/jonfroehlich/sketches/f060jgy7
 * 
 * This sketch will work with any 32u4- or SAMD-based boards like the Arduino
 * Leondardo, Esplora, Zero, Due, which can appear as a native mouse and/or keyboard
 * when connected to the computer via USB.
 * 
 * By Jon Froehlich
 * @jonfroehlich
 * http://makeabilitylab.io
 */
 
#include <Keyboard.h>

/*
Read the analog input of a microphone
*/

int micIN= A0;
int audioVal = 0;
const int MAX_ANALOG_VAL = 1023;

// digital I/O pin
const int BUTTON_TOGGLE_KEYBOARD_PIN = 2;

//make keyboard inactive in the beginning
boolean isKeyboardActive = false;
int prevKeyboardToggleVal = HIGH;

void setup() {
  pinMode(BUTTON_TOGGLE_KEYBOARD_PIN, INPUT_PULLUP);

  //turn on serial for debugging
  Serial.begin(9600);

  // Importantly, we need to start with the keyboard off
  // So that it doesn't immediately start to inadvertently
  // type text everywhere :)
  activateKeyboard(false); 

}

void activateKeyboard(boolean turnKeyboardOn){
  if(turnKeyboardOn){
    Serial.println("*** Activating keyboard! ***"); 
    Keyboard.begin();
  }else{
    Serial.println("*** Deactivating keyboard! ***");
    Keyboard.end();
  }

  isKeyboardActive = turnKeyboardOn;
}

void loop() {
  
int keyboardToggleVal = digitalRead(BUTTON_TOGGLE_KEYBOARD_PIN);
  
  if(keyboardToggleVal != prevKeyboardToggleVal){
    if(keyboardToggleVal == LOW){ // button pressed
      activateKeyboard(!isKeyboardActive);
    }
  }

  if(isKeyboardActive){
     audioVal = analogRead(micIN); //reading input from A0
     Keyboard.print(audioVal);
     Keyboard.print(",");

     //for debugging
     Serial.println(audioVal);
     Serial.println(",");
     delay(600);
  }
  
  delay(100); //why delay?
  prevKeyboardToggleVal = keyboardToggleVal;
}
