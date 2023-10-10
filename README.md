#include <SoftwareSerial.h>
#include <DFRobotDFPlayerMini.h>


SoftwareSerial mySerial(10, 11); // RX, TX

DFRobotDFPlayerMini myDFPlayer;



//Declaração dos botões como Constante Inteiras
const int bot_occipital = 6; 
const int bot_pariental = 5;
const int bot_frontal = 4;
const int bot_temporal = 3;
const int bot_cerebelo = 2;

//Declaração nome dos leds
#define led_occipital 44 //
#define led_pariental 40 //
#define led_frontal 38   //
#define led_temporal 36 //
#define led_cerebelo 42 //

void setup() {
  mySerial.begin(9600); //Declara comunicação serial
  Serial.begin(115200); //Comunicação serial

// Define o pino do botão como entrada com pull-up interno
  pinMode(bot_occipital, INPUT_PULLUP); 
  pinMode(bot_pariental, INPUT_PULLUP);
  pinMode(bot_frontal, INPUT_PULLUP);
  pinMode(bot_temporal, INPUT_PULLUP);
  pinMode(bot_cerebelo, INPUT_PULLUP);

  //Define os leds como saida
  pinMode(led_occipital,OUTPUT);
  pinMode(led_pariental,OUTPUT);
  pinMode(led_frontal,OUTPUT);
  pinMode(led_temporal,OUTPUT);
  pinMode(led_cerebelo,OUTPUT);
  
  //Inicia o módulo DFplayer
  if (!myDFPlayer.begin(mySerial)) {
    Serial.println(F("Falha ao inicializar o DFPlayer Mini."));
    while (true);
  }

  Serial.println(F("DFPlayer Mini inicializado com sucesso."));
  myDFPlayer.volume(50);

 
 INICIANDO(); //testa o funcionamento dos leds

}

void INICIANDO(){


  delay(2000);
digitalWrite(led_occipital, HIGH);
digitalWrite(led_pariental, LOW);
digitalWrite(led_frontal, LOW);
digitalWrite(led_temporal, LOW);
digitalWrite(led_cerebelo, LOW);

delay(2000);
digitalWrite(led_occipital, HIGH);
digitalWrite(led_pariental, HIGH);
digitalWrite(led_frontal, LOW);
digitalWrite(led_temporal, LOW);
digitalWrite(led_cerebelo, LOW);

delay(2000);
digitalWrite(led_occipital, HIGH);
digitalWrite(led_pariental, HIGH);
digitalWrite(led_frontal, HIGH);
digitalWrite(led_temporal, LOW);
digitalWrite(led_cerebelo, LOW);

delay(2000);
digitalWrite(led_occipital, HIGH);
digitalWrite(led_pariental, HIGH);
digitalWrite(led_frontal, HIGH);
digitalWrite(led_temporal, HIGH);
digitalWrite(led_cerebelo, LOW);

delay(2000);
digitalWrite(led_occipital, HIGH);
digitalWrite(led_pariental, HIGH);
digitalWrite(led_frontal, HIGH);
digitalWrite(led_temporal, HIGH);
digitalWrite(led_cerebelo, HIGH);

delay(1500);
digitalWrite(led_occipital, LOW);
digitalWrite(led_pariental, LOW);
digitalWrite(led_frontal, LOW);
digitalWrite(led_temporal, LOW);
digitalWrite(led_cerebelo, LOW);

delay(900);
digitalWrite(led_occipital, HIGH);
digitalWrite(led_pariental, HIGH);
digitalWrite(led_frontal, HIGH);
digitalWrite(led_temporal, HIGH);
digitalWrite(led_cerebelo, HIGH);

delay(900);
digitalWrite(led_occipital, LOW);
digitalWrite(led_pariental, LOW);
digitalWrite(led_frontal, LOW);
digitalWrite(led_temporal, LOW);
digitalWrite(led_cerebelo, LOW);

}



void LED(){
  //Configuração do led occipital
if(digitalRead(bot_occipital) == LOW){
  delay(500);
  myDFPlayer.play(2); // Reproduz o arquivo número 2
  digitalWrite(led_occipital,HIGH);//LED ligado
  delay(17000);
  digitalWrite(led_occipital, LOW);//LED desligado
  }

  //Configuração do led parietal
  if(digitalRead(bot_pariental) == LOW){
  delay(500);
  myDFPlayer.play(5); // Reproduz o arquivo número 5
  digitalWrite(led_pariental,HIGH);//LED ligado
  delay(22000);
  digitalWrite(led_pariental,LOW);//LED desligado
  }

  //Configuração do led frontal
  if(digitalRead(bot_frontal) == LOW){
  delay(500);
  myDFPlayer.play(4); // Reproduz o arquivo número 4
  digitalWrite(led_frontal,HIGH);//LED ligado
  delay(15000);
  digitalWrite(led_frontal, LOW);//LED desligado
  }

  //Configuração do led temporal
  if(digitalRead(bot_temporal) == LOW){
  delay(500);
  myDFPlayer.play(1); // Reproduz o arquivo número 1
  digitalWrite(led_temporal,HIGH);//LED ligado
  delay(20000);
  digitalWrite(led_temporal, LOW);//LED desligado
  }

  //Configuração do led cerebelo
  if(digitalRead(bot_cerebelo) == LOW){
  delay(500); //Reproduz o arquivo número 3
  myDFPlayer.play(3);
  digitalWrite(led_cerebelo,HIGH);//LED ligado
  delay(17000);
  digitalWrite(led_cerebelo, LOW);//LED desligado
  }

}


void audio(){

   if (digitalRead(bot_occipital) == LOW) { // Verifica se o botão occipital foi pressionado
    Serial.println(F("Botão occipital pressionado!"));
    Serial.println("-Tocando faixa 2."); 
    myDFPlayer.play(2); // Reproduz o arquivo número 1
 
 }


   if (digitalRead(bot_pariental) == LOW) { // Verifica se o botão parietal foi pressionado
    Serial.println(F("Botão pariental pressionado!"));
    Serial.println("-Tocando faixa 2.");
    myDFPlayer.play(5); // Reproduz o arquivo número 1
 
  }

   if (digitalRead(bot_frontal) == LOW) { // Verifica se o botão frontal foi pressionado
    Serial.println(F("Botão frontal pressionado!"));
    Serial.println("-Tocando faixa 3.");
    myDFPlayer.play(4); // Reproduz o arquivo número 1
  }

     if (digitalRead(bot_temporal) == LOW) { // Verifica se o botão temporal foi pressionado
    Serial.println(F("Botão temporal pressionado!"));
    Serial.println("-Tocando faixa 1.");
    myDFPlayer.play(1); // Reproduz o arquivo número 1
  
  }

     if (digitalRead(bot_cerebelo) == LOW) { // Verifica se o botão cerebelo foi pressionado
    Serial.println(F("Botão cerebelo pressionado!"));
    Serial.println("-Tocando faixa 5.");
    myDFPlayer.play(3); // Reproduz o arquivo número 3
  }


}



void loop() {

  LED();
  audio();

}
