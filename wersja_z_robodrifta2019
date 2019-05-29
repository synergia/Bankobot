#include<Servo.h>

//DEKLARACJE ZMIENNYCH
#define DEBBUG 1

//Sterownik 1 - PRZEDNI
#define IN1_M1  23 //P-P
#define IN2_M1  25 //P-P
#define IN3_M1  27 //P-L
#define IN4_M1  29 //P-L

//Sterownik 2 - tylny
#define IN1_M2  2 //T-L
#define IN2_M2  3 //T-L
#define IN3_M2  22 //T-P
#define IN4_M2  24 //T-P

//Serwomechanizm
#define serwo_pis_pin 11 //pin serwomechanizmu
//Bąbelki (tranzystor) 
#define pistolet 52  //pin tranzystora z pistoletem
#define wiatrak A8 //pin wiatraka 

//Kanały RC
#define CH1_pin A2  //lewo prawo jedz
#define CH2_pin A1  //przod tyl jedz
#define CH4_pin A0  //lewo preawo skrec
#define CH5_pin A3  //obsluga serwa
#define CH6_pin A4 //obsluga pistoletu 
#define CH7_pin A5 //obsluga pistoletu 

int speed_pwm=127; //predkosc kol 
int CH1, CH2, CH4, CH5, CH5_1,CH5_2,CH5_3, CH6, CH7, CH7_1, CH7_2, CH7_3; //zczytane dane z odbiornika

unsigned long aktualnyCzas = 0;
unsigned long zapamientanyCzasRC = 0;
int tmp, tmp2, tmp3 = 0;

Servo serwo_pis;
///////////////////////////////////////////////////
void setup() {
//  Serial.begin(9600);
  //USTAWIENIE WYJŚĆ
  pinMode(IN1_M1, OUTPUT); pinMode(IN2_M1, OUTPUT); pinMode(IN3_M1, OUTPUT); pinMode(IN4_M1, OUTPUT);
  pinMode(IN1_M2, OUTPUT); pinMode(IN2_M2, OUTPUT); pinMode(IN3_M2, OUTPUT); pinMode(IN4_M2, OUTPUT);
  pinMode(pistolet, OUTPUT); pinMode(wiatrak, OUTPUT);
  pinMode(CH1_pin, INPUT); pinMode(CH2_pin, INPUT); pinMode(CH4_pin, INPUT); pinMode(CH5_pin, INPUT); pinMode(CH6_pin, INPUT); pinMode(CH7_pin, INPUT);

  serwo_pis.attach(serwo_pis_pin);
}
///////////////////////////////////////////////////


void loop() {

aktualnyCzas = millis();

////  !!!BLUETOOTH!!!!
//  char  bt_data = 0;
//  if (Serial.available() > 0) {
//
//    bt_data = Serial.read();
//    if (bt_data >= '0' && bt_data <= 'z') {
//      Serial.println(bt_data);
//
//      switch (bt_data) {
//        case '1': jedz_przod(speed_pwm); break;
//        case '2': jedz_tyl(speed_pwm); break;
//        case '3': jedz_lewo(speed_pwm); break;
//        case '4': jedz_prawo(speed_pwm); break;
//        case '5': skrec_lewo(speed_pwm); break;
//        case '6': skrec_prawo(speed_pwm); break;
//        case '7': speed_pwm = MAX_SPEED; break;
//        case '8': speed_pwm = MAX_SPEED/2; break;
//        case '0': STOP(); break;
//        default: STOP();
//
//      }
//    }
//  }

//jedz_tyl(MAX_SPEED);


//!!!!RC RC RC RC RC !!!!!
CH1 = pulseIn(CH1_pin, HIGH); //jedz lewo prawo
CH2 = pulseIn(CH2_pin, HIGH); //jedz przod tyl
CH4 = pulseIn(CH4_pin, HIGH); //skresc lewo prawo
CH5 = pulseIn(CH5_pin, HIGH); //serwo
CH6 = pulseIn(CH6_pin, HIGH); //pistolet
CH7 = pulseIn(CH7_pin, HIGH); //serwo kamery


//if(DEBBUG == 1){
//  if(aktualnyCzas - zapamientanyCzasRC >=1000UL) {
//    zapamientanyCzasRC = aktualnyCzas;  
  Serial.print("CH1: "); Serial.println(CH1);
  Serial.print("CH2: "); Serial.println(CH2);
  Serial.print("CH4: "); Serial.println(CH4);
  Serial.print("CH5: "); Serial.println(CH5);
  Serial.print("CH6: "); Serial.println(CH6);
  Serial.print("CH7: "); Serial.println(CH7);
  Serial.println("======");
//}
//}

//wszystkie gałki w pozycji 0
if( (CH1 >= 1400) && (CH1 <= 1550) && (CH2 >= 1400) && (CH2 <= 1550) && (CH4 >= 1400) && (CH4 <= 1550) )
{
   STOP();
}
//inne, błędne pomiary. Szumy itp.
else if((CH1 >= 2000) || (CH1 <= 950) || (CH2 >= 2000) || (CH2 <= 950) || (CH4 >= 2000) || (CH4 <= 950) || (CH5 <=950) || (CH5>=2000) || (CH6 <=900) || (CH6>=2000) || (CH7 <=900) || (CH7>=2000) )
{
   STOP(); 
}
//jedziemy prosto
else if((CH1 >= 1450) && (CH1 <= 1550) && (CH2 > 1550) && (CH4 >= 1450) && (CH4 <= 1550))
{
jedz_przod();

}

//jedziemy do tyłu
else if((CH1 >= 1450) && (CH1 <= 1550) && (CH2 < 1400) && (CH4 >= 1450) && (CH4 <= 1550) )
{
 jedz_tyl();

}


//jade w prawo
else if((CH1 > 1500) && (CH2 >= 1450) && (CH2 <= 1550) && (CH4 >= 1450) && (CH4 <= 1550) )
{
  jedz_prawo();
}

//jade w lewo
else if( (CH1 < 1400) && (CH2 >= 1450) && (CH2 <= 1550) && (CH4 >= 1450) && (CH4 <= 1550) )
{
jedz_lewo();
}

//skrec w prawo
else if( (CH1 >= 1450) && (CH1 <= 1550) && (CH2 >= 1450) && (CH2 <= 1550) && (CH4 > 1550) )
{
skrec_prawo();
}
//skrec w lewo
else if( (CH1 >= 1450) && (CH1 <= 1550) && (CH2 >= 1450) && (CH2 <= 1550) &&  (CH4 < 1400)  )
{
skrec_lewo();
}

//REGULACJA PISTOLETU 
//serwo w pozycji domyslnej
if((CH5 < 1100) || (CH5>=2000)) {
  serwo_pis.write(90);
}

//sterowanie reczne serwem
else if( (CH5 >= 1100) && (CH5 <= 2000)){

 // CH5 = (CH5+CH5_1+CH5_2+CH5_3)/4;
  tmp2 =int( map(CH5, 1100, 2000, 10, 170));
  serwo_pis.write(tmp2);
}

//sterowanie wiatrakiem 
if(CH7 <= 1100) //pistolet off
{
  digitalWrite(wiatrak, LOW);
}
else if(CH7 >= 1100) //pistolet on
{
  digitalWrite(wiatrak, HIGH);
}

if(CH6 <= 1100) //pistolet off
{
  digitalWrite(pistolet, LOW);
}
else if(CH6 >= 1100) //pistolet on
{
  digitalWrite(pistolet, HIGH);
}

} //end loop

////////////////////////////////////////////////////
void jedz_przod() {
  Serial.println("jedz przod");   //P-P Przod
  digitalWrite(IN1_M1, LOW);
  digitalWrite(IN2_M1, HIGH);
   //P-L Przod
  digitalWrite(IN3_M1, LOW);
  digitalWrite(IN4_M1, HIGH);

  //T-P Przod
  digitalWrite(IN3_M2, HIGH);
  digitalWrite(IN4_M2, LOW);

   //T-L Przod
  digitalWrite(IN1_M2, HIGH);
  digitalWrite(IN2_M2, LOW);
}

void jedz_tyl() {
  Serial.println("jedz tyl");
   //P-P Tył
  digitalWrite(IN1_M1, HIGH);
  digitalWrite(IN2_M1, LOW);

  //P-L Tył
  digitalWrite(IN3_M1, HIGH);
  digitalWrite(IN4_M1, LOW);

   //T-P Tył
  digitalWrite(IN3_M2, LOW);
  digitalWrite(IN4_M2, HIGH);

  //T-L Tył
  digitalWrite(IN1_M2, LOW);
  digitalWrite(IN2_M2, HIGH);
}


void skrec_lewo() {
  Serial.println("skrec lewo");
   //P-P Przod
  digitalWrite(IN1_M1, LOW);
  digitalWrite(IN2_M1, HIGH);
   //T-P Przod
  digitalWrite(IN3_M2, HIGH);
  digitalWrite(IN4_M2, LOW);

  //P-L Tył
  digitalWrite(IN3_M1, HIGH);
  digitalWrite(IN4_M1, LOW);
   //T-L Tył
  digitalWrite(IN1_M2, LOW);
  digitalWrite(IN2_M2, HIGH);
}

void skrec_prawo() {
  Serial.println("skrec prawo");
  //P-P Tył
  digitalWrite(IN1_M1, HIGH);
  digitalWrite(IN2_M1, LOW);

   //T-P Tył
  digitalWrite(IN3_M2, LOW);
  digitalWrite(IN4_M2, HIGH);
   //P-L Przod
  digitalWrite(IN3_M1, LOW);
  digitalWrite(IN4_M1, HIGH);
  //T-L Przod
  digitalWrite(IN1_M2, HIGH);
  digitalWrite(IN2_M2, LOW);
}

void jedz_lewo() {
  Serial.println("jedz lewo");
   //P-P Przod
  digitalWrite(IN1_M1, LOW);
  digitalWrite(IN2_M1, HIGH);

   //P-L Tył
  digitalWrite(IN3_M1, HIGH);
  digitalWrite(IN4_M1, LOW);

  //T-P Tył
  digitalWrite(IN3_M2, LOW);
  digitalWrite(IN4_M2, HIGH);

  //T-L Przod
  digitalWrite(IN1_M2, HIGH);
  digitalWrite(IN2_M2, LOW);
}


void jedz_prawo() {
  Serial.println("jedz prawo");
   //P-P Tył
  digitalWrite(IN1_M1, HIGH);
  digitalWrite(IN2_M1, LOW);

   //P-L Przod
  digitalWrite(IN3_M1, LOW);
  digitalWrite(IN4_M1, HIGH);

 //T-P Przod
  digitalWrite(IN3_M2, HIGH);
  digitalWrite(IN4_M2, LOW);

   //T-L Tył
  digitalWrite(IN1_M2, LOW);
  digitalWrite(IN2_M2, HIGH);
}

void STOP() {
  Serial.println("STOP");
   //P-P Tył
  digitalWrite(IN1_M1, LOW);
  digitalWrite(IN2_M1, LOW);

   //P-L Przod
  digitalWrite(IN3_M1, LOW);
  digitalWrite(IN4_M1, LOW);

  //T-P Przod
  digitalWrite(IN3_M2, LOW);
  digitalWrite(IN4_M2, LOW);

   //T-L Tył
  digitalWrite(IN1_M2, LOW);
  digitalWrite(IN2_M2, LOW);

}
