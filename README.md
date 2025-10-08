<img width="415" height="1141" alt="image" src="https://github.com/user-attachments/assets/39ce6c1d-f57d-41e7-b226-e3db8bb3f4c9" /># Manual_Telegram_nodeMCU
Made by Jaydey Faasen. 

## Introduction ##
This manual contains a step by step guide that will help you learn to controll your NodeMCU (ESP8266) via telegram. You will learn how you can controll a ledstrip through telegram. Its always possible that there will be errors and mistakes and thats ok! This manual contains a section that will help you fix that. 

## what do you need? ##
For this specific manual you will need the following parts:
* an ESP8266 board.
* A LEDstrip
* Arduino IDE

Lets get started!

## Step 1.1 setting up Telegram ##
The first step is easy! Go to your playstore/google store on your mobile phone, and search for telegram in the searchbar. After that make an account and make sure you log in to the mobile app. 

<img width="300" alt="image" src="https://github.com/user-attachments/assets/34f7b075-c6b8-4145-87d7-5cf8513a3b62" />

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

## step 2.1 setting up the board ##
We are starting of with preparing our board before we plug it in. Lets put the wires in the right place (dont remove or move the wires while its plugged in)

Plug the yellow wire onto D1, The red wire onto 3V and the black one on G. It should look like something like this:

<img width="250" alt="Schermafbeelding 2025-10-08 144612" src="https://github.com/user-attachments/assets/aae43817-cb13-4058-af09-fa389a33b398" />
Are the wires in the correct places? Continue to the next step. 



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
First click on tools in the left topside on your screen, after many options have folded click on boards esp8266. after you clicked on sep8266, a bunch of board will appear and make sure you scroll down and pick NodeMCU 1.0 (ESP-12E Module)

steps: tools > board > esp8266 > NodeMCU 1.0 (ESP-12E Module)

<img width="350" alt="Schermafbeelding 2025-10-08 150910" src="https://github.com/user-attachments/assets/7e46de64-2c09-45c5-a310-404ec5ed9089" />





After completing the setup, the time has finally arrived to do some cool technical stuff! 
