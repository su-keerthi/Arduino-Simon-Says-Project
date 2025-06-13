// Simon game

#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

int maxCount = 20;  //max number in random sequence
int rndSeq[50] ;
int debounceDelay = 100;
int startButton=3;
int dualplayer=12;
const int buzzerPin = 2;

const int ledPin1 = 8;
const int ledPin2 = 9;
const int ledPin3 = 10;
const int ledPin4 = 11;

const int button1 = 4;
const int button2 = 5;
const int button3 = 6;
const int button4 = 7;
  
const int note_G3 = 196;  //these are piano note frequencies
const int note_A3 = 220;
const int note_B3 = 247;
const int note_C4 = 262;

int iCount;
int iiCount;
int highScore = 0;
int score = 0;
int level=1;

int freq[4] = {196, 220, 247, 262};
int seqDuration = 500; // tone length
int seqDelay = 350;   //delay while LED seq played
int replayDelay = 1500; //delay before playing next sequence
int button;

void setup() 
{
  lcd.init();
pinMode(startButton,INPUT_PULLUP);
pinMode(dualplayer,INPUT_PULLUP);
pinMode(ledPin1, OUTPUT);  
pinMode(ledPin2, OUTPUT);  
pinMode(ledPin3, OUTPUT); 
pinMode(ledPin4, OUTPUT); 
  
pinMode(button1, INPUT_PULLUP);
pinMode(button2, INPUT_PULLUP);
pinMode(button3, INPUT_PULLUP);
pinMode(button4, INPUT_PULLUP);
  
Serial.begin(9600);
}

void loop()
{
  if(digitalRead(startButton)==LOW){
    delay(1000);
     lcd.backlight(); 
     lcd.setCursor(0, 0);
  lcd.print("Simon Says Game");
   melody1();
     lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Get Ready!!");
  beepStart();  // play beeps and flash all leds at start
  delay(1000);
  lcd.clear();
 
//generate random sequence
int randomStart = analogRead(A3);
  randomSeed(randomStart);
  Serial.print("Random seed = ");
  Serial.println(randomStart);
  for (int count =0 ; count < maxCount ; count++)
  {rndSeq[count] = random(1,5);
  }
//print the sequence
  Serial.println("Sequence = ");
  for (int count =0 ; count <maxCount ; count++)
  {Serial.print(rndSeq[count]);
  }  
  Serial.println();
  Serial.println();
    
// play the game until correctResponse is false, or maxCount reached  
  boolean correctResponse = true;
//start with 1 note, then build sequence
  int loopCount = 0,iCount = 0;          
  while (loopCount < maxCount) 
  {
  
    score = loopCount+1;
    while (iCount <= loopCount)  //play sequence up to loopCount    
    {
     button = rndSeq[iCount];
     Serial.print(button);  //print the correct sequence for debugging
     digitalWrite(ledPin1, LOW);  
     digitalWrite(ledPin2, LOW);
     digitalWrite(ledPin3, LOW);  
     digitalWrite(ledPin4, LOW);
     
       lcd.setCursor(4, 0);
     lcd.print("Level:");
    lcd.setCursor(10, 0);
     lcd.print(level);
    lcd.setCursor(4, 1);
     lcd.print("MEMORISE");
      
  if (button == 1) 
     {digitalWrite(ledPin1, HIGH);
     tone(buzzerPin, freq[button-1], seqDuration);
     delay(seqDelay);
     digitalWrite(ledPin1, LOW);
     delay(50);
      noTone(buzzerPin);}
  if (button == 2) 
     {digitalWrite(ledPin2, HIGH);
     tone(buzzerPin, freq[button-1], seqDuration);
     delay(seqDelay);
     digitalWrite(ledPin2, LOW);
     delay(50);
      noTone(buzzerPin);}
  if (button == 3) 
     {digitalWrite(ledPin3, HIGH);
     tone(buzzerPin, freq[button-1], seqDuration); 
     delay(seqDelay);
     digitalWrite(ledPin3, LOW);
     delay(50);
      noTone(buzzerPin);}
  if (button == 4) 
     {digitalWrite(ledPin4, HIGH);
     tone(buzzerPin, freq[button-1], seqDuration);
     delay(seqDelay);
     digitalWrite(ledPin4, LOW);
     delay(50);
      noTone(buzzerPin);} 
     iCount = iCount+1; 
    }  // End of played sequence
   
     level++;  // End of played sequence
    lcd.clear();
// Listen for user replay sequence  
    Serial.println( ); 
    Serial.println("Enter your response: "); 
    iiCount = 0;
    
  while (iiCount <= loopCount) {
    digitalWrite(ledPin1, LOW);  
    digitalWrite(ledPin2, LOW);
    digitalWrite(ledPin3, LOW);  
    digitalWrite(ledPin4, LOW);
 
     lcd.setCursor(4, 0);
    lcd.print("Your Turn");
//Test for button 1 being pressed
  if (digitalRead(button1) == LOW ) 
    {button = 1;
     while (digitalRead(button1) == LOW ) // wait until button release
      {digitalWrite(ledPin1,HIGH);} 
    if (button==rndSeq[iiCount]) 
      {correctResponse = true;
      digitalWrite(ledPin1, HIGH); 
      tone(buzzerPin, freq[0],seqDuration);
      delay(debounceDelay); 
       noTone(buzzerPin);
      iiCount=iiCount+1; 
       digitalWrite(ledPin1, LOW);   } 
    else 
      {correctResponse=false;
      digitalWrite(ledPin1, HIGH);
      digitalWrite(ledPin2, HIGH);
      digitalWrite(ledPin3, HIGH);
      digitalWrite(ledPin4, HIGH);
       tone(buzzerPin, 140, 500);
      delay(seqDuration);
      iiCount=999;
      }    
    
    
    }
   
//Test for button 2 being pressed   
  if (digitalRead(button2) == LOW )
    {button = 2;
     while (digitalRead(button2) == LOW ) // wait until button release
      {digitalWrite(ledPin2,HIGH);}  
    if (button==rndSeq[iiCount]) 
      {correctResponse = true;    
      digitalWrite(ledPin2, HIGH); 
      tone(buzzerPin, freq[1],seqDuration);
      delay(debounceDelay);
        noTone(buzzerPin);
      iiCount=iiCount+1;
      digitalWrite(ledPin2, LOW);
      } 
    else 
      {correctResponse=false;
      digitalWrite(ledPin1, HIGH);
      digitalWrite(ledPin2, HIGH);
      digitalWrite(ledPin3, HIGH);
      digitalWrite(ledPin4, HIGH);
      tone(buzzerPin, 140, 500);
      delay(seqDuration);
      iiCount=999;
      }    
   
        
    }
  
//Test for button 3 being pressed    
  if (digitalRead(button3) == LOW )
    {button = 3;
     while (digitalRead(button3) == LOW ) // wait until button release
      {digitalWrite(ledPin3,HIGH);}
    if (button==rndSeq[iiCount]) 
      {correctResponse = true;
       digitalWrite(ledPin3, HIGH); 
       tone(buzzerPin, freq[2],seqDuration);
       delay(debounceDelay);
        noTone(buzzerPin);
       iiCount=iiCount+1;
        digitalWrite(ledPin3, LOW);
       }          
    else 
      {correctResponse=false;
      digitalWrite(ledPin1, HIGH);
      digitalWrite(ledPin2, HIGH);
      digitalWrite(ledPin3, HIGH);
      digitalWrite(ledPin4, HIGH);
      tone(buzzerPin, 140, 500);
      delay(seqDuration);
      iiCount=999;
      }  
    
   
    } 
    
//Test for button 4 being pressed   
  if (digitalRead(button4) == LOW )
    {button = 4;
     while (digitalRead(button4) == LOW ) // wait until button release
      {digitalWrite(ledPin4,HIGH);} 
    if (button==rndSeq[iiCount]) 
      {correctResponse = true;
      digitalWrite(ledPin4, HIGH); 
      tone(buzzerPin, freq[3],seqDuration);
      delay(debounceDelay);
        noTone(buzzerPin);
      iiCount=iiCount+1;
       digitalWrite(ledPin4, LOW);     
      } 
    else 
      {correctResponse=false;
      digitalWrite(ledPin1, HIGH);
      digitalWrite(ledPin2, HIGH);
      digitalWrite(ledPin3, HIGH);
      digitalWrite(ledPin4, HIGH);
      tone(buzzerPin, 140, 500);
      delay(seqDuration);
      iiCount=999;
      }  
   
   
    }
    
//If correctResponse is false, set the counts high to exit the loop
    if (correctResponse==false) 
    {iiCount= 999; iCount=999; 
    loopCount = 111;
    Serial.println("Wrong one.");
    }                        
  }   //end of user response loop 
    lcd.clear();
      digitalWrite(ledPin1, LOW);
      digitalWrite(ledPin2, LOW);
      digitalWrite(ledPin3, LOW);
      digitalWrite(ledPin4, LOW);
         
   delay(replayDelay); 
   loopCount = loopCount+1;  //add one note to sequence
  }  //end of main loopCount loop -------------------

// game end, the user either finished the sequence, or made a wrong resonse

if(correctResponse==true)
{
  Serial.println("Winner!");
  lcd.setCursor(4,0);
  lcd.print("Winner!");
  melody1();
} 
else 
{
  Serial.println("Sorry");  melody2();
  lcd.setCursor(4,0);
  lcd.print("You lose");
  score = score-1;
}
  // Game over.------------------

   Serial.print("Score = ");Serial.println(score);
     lcd.setCursor(2,1);
  lcd.print("Score = ");
  lcd.setCursor(10,1);
  lcd.print(score);
  delay(1500);
  lcd.clear();
   Serial.println("game over - restarting");
    lcd.setCursor(4,0);
  lcd.print("Game Over");
  delay(1000);
  lcd.clear();
   delay(1000);
    level=1;

  }
  else if(digitalRead(dualplayer)==LOW){
      int arr[2];
      int number=1;
      for(int i=0;i<2;i++){
     delay(1000);
     lcd.backlight(); 
     lcd.setCursor(3,0);
           lcd.print("Player");
           lcd.setCursor(9,0);
           lcd.print(number);
           delay(1000);
           lcd.clear();
     lcd.setCursor(0, 0);
  lcd.print("Simon Says Game");
   melody1();
     lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Get Ready!!");
  beepStart();  // play beeps and flash all leds at start
  delay(1000);
  lcd.clear();
 
//generate random sequence
int randomStart = analogRead(A3);
  randomSeed(randomStart);
  Serial.print("Random seed = ");
  Serial.println(randomStart);
  for (int count =0 ; count < maxCount ; count++)
  {rndSeq[count] = random(1,5);
  }
//print the sequence
  Serial.println("Sequence = ");
  for (int count =0 ; count <maxCount ; count++)
  {Serial.print(rndSeq[count]);
  }  
  Serial.println();
  Serial.println();
    
// play the game until correctResponse is false, or maxCount reached  
  boolean correctResponse = true;
//start with 1 note, then build sequence
  int loopCount = 0,iCount = 0;          
  while (loopCount < maxCount) 
  {
  
    score = loopCount+1;
    while (iCount <= loopCount)  //play sequence up to loopCount    
    {
     button = rndSeq[iCount];
     Serial.print(button);  //print the correct sequence for debugging
     digitalWrite(ledPin1, LOW);  
     digitalWrite(ledPin2, LOW);
     digitalWrite(ledPin3, LOW);  
     digitalWrite(ledPin4, LOW);
     
       lcd.setCursor(4, 0);
     lcd.print("Level:");
    lcd.setCursor(10, 0);
     lcd.print(level);
    lcd.setCursor(4, 1);
     lcd.print("MEMORISE");
      
  if (button == 1) 
     {digitalWrite(ledPin1, HIGH);
     tone(buzzerPin, freq[button-1], seqDuration);
     delay(seqDelay);
     digitalWrite(ledPin1, LOW);
     delay(50);
      noTone(buzzerPin);}
  if (button == 2) 
     {digitalWrite(ledPin2, HIGH);
     tone(buzzerPin, freq[button-1], seqDuration);
     delay(seqDelay);
     digitalWrite(ledPin2, LOW);
     delay(50);
      noTone(buzzerPin);}
  if (button == 3) 
     {digitalWrite(ledPin3, HIGH);
     tone(buzzerPin, freq[button-1], seqDuration); 
     delay(seqDelay);
     digitalWrite(ledPin3, LOW);
     delay(50);
      noTone(buzzerPin);}
  if (button == 4) 
     {digitalWrite(ledPin4, HIGH);
     tone(buzzerPin, freq[button-1], seqDuration);
     delay(seqDelay);
     digitalWrite(ledPin4, LOW);
     delay(50);
      noTone(buzzerPin);} 
     iCount = iCount+1; 
    }  // End of played sequence
   
     level++;  // End of played sequence
    lcd.clear();
// Listen for user replay sequence  
    Serial.println( ); 
    Serial.println("Enter your response: "); 
    iiCount = 0;
    
  while (iiCount <= loopCount) {
    digitalWrite(ledPin1, LOW);  
    digitalWrite(ledPin2, LOW);
    digitalWrite(ledPin3, LOW);  
    digitalWrite(ledPin4, LOW);
 
     lcd.setCursor(4, 0);
    lcd.print("Your Turn");
//Test for button 1 being pressed
  if (digitalRead(button1) == LOW ) 
    {button = 1;
     while (digitalRead(button1) == LOW ) // wait until button release
      {digitalWrite(ledPin1,HIGH);} 
    if (button==rndSeq[iiCount]) 
      {correctResponse = true;
      digitalWrite(ledPin1, HIGH); 
      tone(buzzerPin, freq[0],seqDuration);
      delay(debounceDelay); 
       noTone(buzzerPin);
      iiCount=iiCount+1; 
       digitalWrite(ledPin1, LOW);   } 
    else 
      {correctResponse=false;
      digitalWrite(ledPin1, HIGH);
      digitalWrite(ledPin2, HIGH);
      digitalWrite(ledPin3, HIGH);
      digitalWrite(ledPin4, HIGH);
       tone(buzzerPin, 140, 500);
      delay(seqDuration);
      iiCount=999;
      }    
    
    
    }
   
//Test for button 2 being pressed   
  if (digitalRead(button2) == LOW )
    {button = 2;
     while (digitalRead(button2) == LOW ) // wait until button release
      {digitalWrite(ledPin2,HIGH);}  
    if (button==rndSeq[iiCount]) 
      {correctResponse = true;    
      digitalWrite(ledPin2, HIGH); 
      tone(buzzerPin, freq[1],seqDuration);
      delay(debounceDelay);
        noTone(buzzerPin);
      iiCount=iiCount+1;
      digitalWrite(ledPin2, LOW);
      } 
    else 
      {correctResponse=false;
      digitalWrite(ledPin1, HIGH);
      digitalWrite(ledPin2, HIGH);
      digitalWrite(ledPin3, HIGH);
      digitalWrite(ledPin4, HIGH);
      tone(buzzerPin, 140, 500);
      delay(seqDuration);
      iiCount=999;
      }    
   
        
    }
  
//Test for button 3 being pressed    
  if (digitalRead(button3) == LOW )
    {button = 3;
     while (digitalRead(button3) == LOW ) // wait until button release
      {digitalWrite(ledPin3,HIGH);}
    if (button==rndSeq[iiCount]) 
      {correctResponse = true;
       digitalWrite(ledPin3, HIGH); 
       tone(buzzerPin, freq[2],seqDuration);
       delay(debounceDelay);
        noTone(buzzerPin);
       iiCount=iiCount+1;
        digitalWrite(ledPin3, LOW);
       }          
    else 
      {correctResponse=false;
      digitalWrite(ledPin1, HIGH);
      digitalWrite(ledPin2, HIGH);
      digitalWrite(ledPin3, HIGH);
      digitalWrite(ledPin4, HIGH);
      tone(buzzerPin, 140, 500);
      delay(seqDuration);
      iiCount=999;
      }  
    
   
    } 
    
//Test for button 4 being pressed   
  if (digitalRead(button4) == LOW )
    {button = 4;
     while (digitalRead(button4) == LOW ) // wait until button release
      {digitalWrite(ledPin4,HIGH);} 
    if (button==rndSeq[iiCount]) 
      {correctResponse = true;
      digitalWrite(ledPin4, HIGH); 
      tone(buzzerPin, freq[3],seqDuration);
      delay(debounceDelay);
        noTone(buzzerPin);
      iiCount=iiCount+1;
       digitalWrite(ledPin4, LOW);     
      } 
    else 
      {correctResponse=false;
      digitalWrite(ledPin1, HIGH);
      digitalWrite(ledPin2, HIGH);
      digitalWrite(ledPin3, HIGH);
      digitalWrite(ledPin4, HIGH);
      tone(buzzerPin, 140, 500);
      delay(seqDuration);
      iiCount=999;
      }  
   
   
    }
    
//If correctResponse is false, set the counts high to exit the loop
    if (correctResponse==false) 
    {iiCount= 999; iCount=999; 
    loopCount = 111;
    Serial.println("Wrong one.");
    }                        
  }   //end of user response loop 
    lcd.clear();
      digitalWrite(ledPin1, LOW);
      digitalWrite(ledPin2, LOW);
      digitalWrite(ledPin3, LOW);
      digitalWrite(ledPin4, LOW);
         
   delay(replayDelay); 
   loopCount = loopCount+1;  //add one note to sequence
  }  //end of main loopCount loop -------------------

// game end, the user either finished the sequence, or made a wrong resonse

if(correctResponse==true)
{
  Serial.println("Winner!");
 // lcd.setCursor(4,0);
  //lcd.print("Winner!");
  melody1();
} 
else 
{
  Serial.println("Sorry");  melody2();
  //lcd.setCursor(4,0);
  //lcd.print("You lose");
  score = score-1;
}
  // Game over.------------------
    arr[number-1]=score;
   Serial.print("Score = ");Serial.println(score);
     lcd.setCursor(2,1);
  lcd.print("Score = ");
  lcd.setCursor(10,1);
  lcd.print(score);
  delay(1500);
  lcd.clear();
   Serial.println("game over - restarting");
    lcd.setCursor(4,0);
  lcd.print("Game Over");
  delay(1000);
  lcd.clear();
   delay(1000);
    level=1;
    number++;      
      } 
     if(arr[0]>arr[1]){
         lcd.setCursor(3,0);
         lcd.print("Player1 Wins!");
         delay(1000);
         }
         else if(arr[0]<arr[1]){
         lcd.setCursor(3,0);
         lcd.print("Player2 Wins!");
          delay(1000);
         }
         else{
             lcd.setCursor(3,0);
             lcd.print("It's a Tie!");
              delay(1000);
         }
         lcd.clear();
  }
   lcd.noBacklight();
}

void melody1()  // function to play opening melody
{
// notes in the melody1:
int thisNote;
int pauseDuration;
int playDuration;
int notes1 = 7;
int melody1[] = {note_G3, note_A3, note_B3, note_C4, 0, note_G3, note_C4};

// note durations: 4 = quarter note, 8 = eighth note, etc.
int noteDurations1[] = { 8, 8, 8, 4, 4, 4, 2};
int wholeNoteDuration = 2000;

  for (thisNote = 0; thisNote < notes1; thisNote++) 
  { 
  // to calculate the note duration, take whole note duration
  // divided by the note type.
  //e.g. quarter note = 1000 / 4, eighth note = 1000/8, etc.
  noteDurations1[thisNote] = wholeNoteDuration / noteDurations1[thisNote]; 
  }
  // play the notes of the melody1:------------------
  for (thisNote = 0; thisNote < notes1; thisNote++) 
  {
  playDuration = noteDurations1[thisNote] * .7 ; 
  pauseDuration = noteDurations1[thisNote] *.3 ;
    
  if (melody1[thisNote] == note_G3) {digitalWrite(ledPin1, HIGH);}
  if (melody1[thisNote] == note_A3) {digitalWrite(ledPin2, HIGH);}
  if (melody1[thisNote] == note_B3) {digitalWrite(ledPin3, HIGH);}
  if (melody1[thisNote] == note_C4) {digitalWrite(ledPin4, HIGH);}
   
  tone(buzzerPin, melody1[thisNote], playDuration);
    
    delay(playDuration);
    digitalWrite(ledPin1, LOW);   
    digitalWrite(ledPin2, LOW);
    digitalWrite(ledPin3, LOW);  
    digitalWrite(ledPin4, LOW);  
    noTone(buzzerPin);   // stop the tone playing:          
  } 
}

void melody2()
{
// notes in the melody2:
int thisNote;
int pauseDuration;
int playDuration;
int wholeNoteDuration = 2000;
int notes2 = 7;
int melody2[] = {note_C4, note_G3, note_G3, note_A3, note_G3, note_B3, note_C4};
// note durations: 4 = quarter note, 8 = eighth note, etc.
int noteDurations2[] = {  4, 8, 8, 4, 2, 4, 4};

  
//convert durations to milliseconds melody2
for (thisNote = 0; thisNote < notes2; thisNote++) 
{ 
  // to calculate the note duration, take whole note duration
  // divided by the note type.
  //e.g. quarter note = 1000 / 4, eighth note = 1000/8, etc.
  noteDurations2[thisNote] = wholeNoteDuration / noteDurations2[thisNote]; 
}  
  for (thisNote = 0; thisNote < notes2; thisNote++) 
  {
  playDuration = noteDurations2[thisNote] * .7 ; 
  pauseDuration = noteDurations2[thisNote] *.3 ;
    
  if (melody2[thisNote] == note_G3) {digitalWrite(ledPin1, HIGH);}
  if (melody2[thisNote] == note_A3) {digitalWrite(ledPin2, HIGH);}
  if (melody2[thisNote] == note_B3) {digitalWrite(ledPin3, HIGH);}
  if (melody2[thisNote] == note_C4) {digitalWrite(ledPin4, HIGH);}
   
  tone(buzzerPin, melody2[thisNote], playDuration);
    
    delay(playDuration);
    digitalWrite(ledPin1, LOW);   
    digitalWrite(ledPin2, LOW);
    digitalWrite(ledPin3, LOW);  
    digitalWrite(ledPin4, LOW);  
    noTone(buzzerPin);   // stop the tone playing:          
  } 
}
void beepStart()
{
int toneFreq = 100;
  for(int i=1; i<13; i++)
{  
     tone(buzzerPin, toneFreq, 200);
    digitalWrite(ledPin1, HIGH);  
    digitalWrite(ledPin2, HIGH);
    digitalWrite(ledPin3, HIGH);  
    digitalWrite(ledPin4, HIGH);
   delay(100);
    digitalWrite(ledPin1, LOW);  
    digitalWrite(ledPin2, LOW);
    digitalWrite(ledPin3, LOW);  
    digitalWrite(ledPin4, LOW);
   delay(100);
    toneFreq= float(toneFreq)*1.12;
}
}
