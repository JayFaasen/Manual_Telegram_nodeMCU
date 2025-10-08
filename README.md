# Manual_Telegram_nodeMCU
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

## step 2.1 ##
After completing the setup, the time has finally arrived to do some cool technical stuff! 
We are starting of with preparing our board before we plug it in. Lets put the wires in the right place (dont remove or move the wires while its plugged in)

Plug the yellow wire onto D1, The red wire onto 3V and the black one on G. It should look like something like this:



![WhatsApp Image 2025-10-08 at 14 40 21](https://github.com/user-attachments/assets/367fa2af-5dcb-43e8-9937-b8156a798b5d)



