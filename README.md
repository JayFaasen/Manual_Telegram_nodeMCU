Made by Jaydey Faasen. 

## Introduction ##
This manual contains a step by step guide that will help you learn to controll your NodeMCU (ESP8266) via telegram. You will learn how you can controll a ledstrip through telegram. Its always possible that there will be errors and mistakes and thats ok! This manual contains a section that will help you fix that. 

## what do you need? ##
For this specific manual you will need the following parts:
* an ESP8266 board.
* A LEDstrip
* Arduino IDE

Lets get started!


## Step 1 ##
### Step 1.1 setting up Telegram ###
The first step is easy! Go to your playstore/google store on your mobile phone, and search for telegram in the searchbar. After that make an account and make sure you log in to the mobile app. 

<img width="250" alt="image" src="https://github.com/user-attachments/assets/34f7b075-c6b8-4145-87d7-5cf8513a3b62" />

After you logged in, Search for BotFather in the searchbar, click on botfather and begin the chat. 

<img width="250"  alt="Schermafbeelding 2025-10-08 140521" src="https://github.com/user-attachments/assets/d09f9a77-497c-40e9-8d1c-35ad5caee885" />

After starting the chat witch BotFather, you get a big text that contains a lot of things the bot can do for you, for this manual you will only need to type or click on /newbot. After that name your bot, you can name it anything you'd like. The chat should look something like this:

<img width="300" alt="image" src="https://github.com/user-attachments/assets/ff4a485f-4d67-46de-a0fa-d3845ef9acdc" />

Make sure you copy the ID-token that got sended to you in the conformation message after you named your bot, you will need it later to controll your ledstrip remotely (so write it down or put it in a safe document). Dont share it with anyone that you dont want to have in controll of your bot, because the token gives controll so make sure you keep it save. 



### Step 1.2 ###
After completing the Last step, we are going to focus on gathering your telegram chat-id. After you close the bot, go back to the search bar and type "myidbot" or "IDBot". click on 
the bot and start the chat.

<img width="250" alt="Schermafbeelding 2025-10-08 142823" src="https://github.com/user-attachments/assets/8484187a-f70e-4ea4-9c4d-c7721d6fc7c5" />

After starting the chat, click on /getid and write down or copy the ID (the ID should only contain numbers)
ANd thats it for the first step! Continue if you completed both step 1.1 and 1.2. 

### step 2.1 setting up the board ###
We are starting of with preparing our board before we plug it in. Lets put the wires in the right place (dont remove or move the wires while its plugged in)

Plug the yellow wire onto D1, The red wire onto 3V and the black one on G. It should look like something like this:

<img width="250" alt="Schermafbeelding 2025-10-08 144612" src="https://github.com/user-attachments/assets/aae43817-cb13-4058-af09-fa389a33b398" />
Are the wires in the correct places? Continue to the next step. 


## Step 2 ##
### step 2.2 downloading liberaries ###

After putting the wires on to the right plugs, were going to donwload some arduino liberaries. Open arduino and go to liberaries. 

<img width="250" alt="Schermafbeelding 2025-10-08 145029" src="https://github.com/user-attachments/assets/a113b888-924e-4455-8126-71c9702b19ee" />

First we are going to download Adafruit Neopixel, type this in your searchbard and make sure you download this one and not the DMA one. This might cause errors and problems later. 

<img width="250" alt="Schermafbeelding 2025-10-08 145548" src="https://github.com/user-attachments/assets/a78eadbc-e989-49ce-b217-37e1de61a1e0" />

After downloading this one, we are going to download a liberary for our telegram bot. in the same searchbar type in universal telegram bot and select the one from Brian Lough. Click on download

<img width="350" height="1141" alt="image" src="https://github.com/user-attachments/assets/8dd76461-9da5-4e51-a0b5-9111e5d25e81" />

after you clicked on download, its probably gonna give an notification asking about dependencies. Since we will need them, click on install all.

<img width="250" alt="image" src="https://github.com/user-attachments/assets/807eb9fb-49d2-4256-8291-adb6d48cb509" />
 
After installing the liberaries, you are ready to connect your board. 


### step 2.3 connecting our board ###
For this step its gonna be a little bit more technical, since we are going to connect you NodeMCU board. 
First click on tools in the left topside on your screen, after many options have folded click on boards esp8266. after you clicked on sep8266, a bunch of board will appear and make sure you scroll down and pick NodeMCU 1.0 (ESP-12E Module). Make sure your board is connected, check at the right bottom corner. If its not connected try these steps again, otherwise go to troubleshooting. 

steps: tools > board > esp8266 > NodeMCU 1.0 (ESP-12E Module)

<img width="450" alt="Schermafbeelding 2025-10-08 150910" src="https://github.com/user-attachments/assets/7e46de64-2c09-45c5-a310-404ec5ed9089" />

it should say this at the right bottom corner

<img width="570" height="31" alt="Schermafbeelding 2025-10-08 152007" src="https://github.com/user-attachments/assets/e29f7f59-3384-4b4f-9e2c-38951f3f3c07" />

Thats it for connecting!

## Step ##
### step 3.1 starting with coding ###
Lets finally get started with coding! make a new sketch (if youre not already in a new one), we are going to paste this code, you can just copy paste this. 

code:

#ifdef ESP32
  #include <WiFi.h>
#else
  #include <ESP8266WiFi.h>
#endif
#include <WiFiClientSecure.h>
#include <UniversalTelegramBot.h>
#include <ArduinoJson.h>
#include <Adafruit_NeoPixel.h>
#ifdef __AVR__
 #include <avr/power.h>
#endif

// Replace with your network credentials
const char* ssid = "your wifi username";
const char* password = "your wifi password";

// Initialize Telegram BOT
#define BOTtoken "your bot token that you received from the botfather"
#define CHAT_ID "your chattoken that you received from my id bot"

#define PIN D1
#define NUMPIXELS 12

Adafruit_NeoPixel pixels(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);
#define DELAYVAL 500

#ifdef ESP8266
  X509List cert(TELEGRAM_CERTIFICATE_ROOT);
#endif

WiFiClientSecure client;
UniversalTelegramBot bot(BOTtoken, client);

int botRequestDelay = 1000;
unsigned long lastTimeBotRan;

const int ledPin = 2;
bool ledState = HIGH;

// Handle what happens when you receive new messages
void handleNewMessages(int numNewMessages) {
  for (int i=0; i<numNewMessages; i++) {
    String chat_id = String(bot.messages[i].chat_id);
    if (chat_id != CHAT_ID){
      bot.sendMessage(chat_id, "Unauthorized user", "");
      continue;
    }
    String text = bot.messages[i].text;
    String from_name = bot.messages[i].from_name;

    if (text == "/start") {
      String welcome = "Welcome, " + from_name + ".\n";
      welcome += "/led_on to turn GPIO ON \n";
      welcome += "/led_off to turn GPIO OFF \n";
      welcome += "/state to request current GPIO state \n";
      bot.sendMessage(chat_id, welcome, "");
    }

    if (text == "/led_on") {
      bot.sendMessage(chat_id, "LED state set to ON", "");
      pixels.clear(); 
      for(int i=0; i<NUMPIXELS; i++) {
        pixels.setPixelColor(i, pixels.Color(0, 150, 0));
        pixels.show();
        delay(DELAYVAL);
        ledState = LOW;
      }
    }
    
    if (text == "/led_off") {
      bot.sendMessage(chat_id, "LED state set to OFF", "");
      pixels.clear(); 
      pixels.show(); 
      ledState = HIGH;
    }
    
    if (text == "/state") {
      if (digitalRead(ledPin)){
        bot.sendMessage(chat_id, "LED is ON", "");
      }
      else{
        bot.sendMessage(chat_id, "LED is OFF", "");
      }
    }
  }
}

void setup() {
  Serial.begin(115200);

  #if defined(__AVR_ATtiny85__) && (F_CPU == 16000000)
  clock_prescale_set(clock_div_1);
  #endif

  pixels.begin();

  #ifdef ESP8266
    configTime(0, 0, "pool.ntp.org");
    client.setTrustAnchors(&cert);
  #endif

  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, ledState);
  
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  #ifdef ESP32
    client.setCACert(TELEGRAM_CERTIFICATE_ROOT);
  #endif
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi..");
  }
  Serial.println(WiFi.localIP());
}

void loop() {
  if (millis() > lastTimeBotRan + botRequestDelay)  {
    int numNewMessages = bot.getUpdates(bot.last_message_received + 1);

    while(numNewMessages) {
      handleNewMessages(numNewMessages);
      numNewMessages = bot.getUpdates(bot.last_message_received + 1);
    }
    lastTimeBotRan = millis();
  }
}
 

### Step 3.2 changing the code ###
So after you pasted the code in your arduino file, we have to do some changes. Change your wifi name and password to an internet connection near you that has good connection. The board only supports 2.4GHz Wi-Fi, so if you are using a hotspot make sure its in compatibility mode. And also add your keys that you got from the telegram bots. 


edit the code you see here in the photo below: 

<img width="400" alt="Schermafbeelding 2025-10-08 153629" src="https://github.com/user-attachments/assets/887894fe-de1e-451a-b357-706cf4bd75f2" />

If you edited the code your are ready to upload it! click on the arrow button in the left top corner.

<img width="250"  alt="Schermafbeelding 2025-10-08 154150" src="https://github.com/user-attachments/assets/c5efc1de-a7e8-42ed-9f6b-4c6690891a65" />

## Step 4 ##
We are almost done! This is the last and hopefully a succesfull step. 
Click on the link from the Botfather chat, see below

<img width="350" alt="image" src="https://github.com/user-attachments/assets/d453b5f1-53b5-46e5-be10-b2ebd88b728d" />

after that click on /start of type /start. 

You can then give the commands '/led_on' or '/led_off' to turn the LED light strip on or off.

<img width="300" alt="image" src="https://github.com/user-attachments/assets/2b4a45a0-0472-4e3b-83e2-a3cede9acb7e" />

