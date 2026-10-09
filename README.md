# OpenWeather API manual
In this manual you will learn how to connect a NodeMCU to a weather API and a ledstrip. 
Weather will be visible through color! 

## What you need 
- NodeMCU ESP8266
- NeoPixel led strip
- USB kabel
- Arduino IDE
- WIFI connection
- Weather API key

### 1. Setting up the ESP8266 board
When you install Arduino IDE, it doesn't have the board we need included by default, so we need to add it manually. 
In the top menu, click on Arduino IDE if you have a Mac and File if you have windows. Select preferences. 

<img width="289" alt="Scherm­afbeelding 2026-10-08 om 23 08 53" src="https://github.com/user-attachments/assets/7f5f30a7-0eac-4fa3-92c2-e3208bdf2914" />

A new window will appear. Find the field that's called 'additional boards manager URL's' and make sure to add this URL:
http://arduino.esp8266.com/stable/package_esp8266com_index.json
Is there already an URL in the field? Don't delete it. Click on the button besides it and add the URL on a new line. 

<img width="400"  alt="Scherm­afbeelding 2026-10-08 om 23 11 58" src="https://github.com/user-attachments/assets/74388091-0e19-4ae8-b865-024fad8e0781" />


### 2. Installing libraries
For this manual you need a few libraries. Open the library manager in Arduino IDE and download these below. 
- AdaFruit NeoPixel
- ArduinoJson by Benoit Blanchon
 <img width="208" alt="Scherm­afbeelding 2026-10-08 om 23 01 28" src="https://github.com/user-attachments/assets/23a1ce65-4cff-4279-89b0-ab87622cf725" />

 ### 3. Select the board
Connect the nodeMCU to your laptop with the usb cable. Go to tools > board > ESP2866 
Select NodeMCU 1.0 (ESP 12-E module)

<img width="250" alt="Scherm­afbeelding 2026-10-08 om 23 50 23" src="https://github.com/user-attachments/assets/f72ac168-510a-4265-911e-4090ea0d72fe" />
<img width="287" height="63" alt="Scherm­afbeelding 2026-10-08 om 23 50 31" src="https://github.com/user-attachments/assets/2f2fbd2c-d798-4df7-b62d-3b990f609185" />

### 4. Select the port
Now we need to select the right port. Go to tools > port 
Select the port that looks similar to '..usbserial-310'. For windows it may look different. Select something like 'COM3' or 'COM4'

<img width="200" alt="Scherm­afbeelding 2026-10-08 om 23 53 53" src="https://github.com/user-attachments/assets/68f5c855-a032-477b-9237-988d8da154f4" />

### Create a weather API account
We'll be getting our data and API key from OpenWeather. Create an account on the website. 
After creating an account, go to 'API keys' and create a key. Your key might not work directly 
so wait a few hours before going on. 

### Including libraries
Open a new sketch to write the code in. To start off, we need to include the libraries we downloaded earlier and the access to WIFI. Do this on the very top of the page. 

<img width="252" alt="Scherm­afbeelding 2026-10-09 om 10 15 02" src="https://github.com/user-attachments/assets/cab9e0d5-0f13-466c-a07c-2c2a2d86ae16" />

### WIFI
The next two lines are for the wifi. The first line is for the wifi name and the second for the password.
ESP2866 uses 2.4GHZ network, so make sure to be connected to your home wifi. 
If you are not at home, use your hotspot. 

<img width="286" alt="Scherm­afbeelding 2026-10-09 om 10 17 40" src="https://github.com/user-attachments/assets/1ee3de8e-e80a-400f-9a5a-25e4213bf913" />

### Open Weather API
Next we need to add a section to gain access to Open Weather and to be able to add our API key to our code. Add the key that you got from the website in the first line. If you are in another city or country, change the other lines to the correct place you are in.

<img width="298" alt="Scherm­afbeelding 2026-10-09 om 10 21 14" src="https://github.com/user-attachments/assets/5bb98f96-a0f5-457b-8ff4-8d1de831de93" />

### Connecting the led strip 
Make sure to change the line if you have more or less leds. 

<img width="511" alt="Scherm­afbeelding 2026-10-09 om 10 24 13" src="https://github.com/user-attachments/assets/b9a1f7f8-aacc-4590-9e9b-4ff7119b9fa5" />


### Setting up the serial monitor
We need the serial monitor to see useful information, such as if our wifi connection is working or not.
Put this in the void SetUp. The usual speed is 115200 baut. 
The second lines are for the led strip. It just prepares it for use. 

<img width="201" alt="Scherm­afbeelding 2026-10-09 om 10 33 19" src="https://github.com/user-attachments/assets/51f13b87-dbed-4e4b-a0aa-c54bce95cafe" />

! I forgot to set the serial monitor to the same baut which caused the code to not work. So when you open it check if its the right number.

<img width="131" alt="Scherm­afbeelding 2026-10-09 om 11 02 50" src="https://github.com/user-attachments/assets/02b82f23-1a62-494f-86e8-6748b12ee99b" />



### Connecting to WIFI
Add these lines to your code. It looks complicated, but the first line just means it's using the name and password we put in earlier. The next lines is the code trying to connect. And it keeps trying as long as the NodeMCU is not connected. If it does connect, you'll be able to see the last line in your serial monitor. 

<img width="250" alt="Scherm­afbeelding 2026-10-09 om 10 40 59" src="https://github.com/user-attachments/assets/d07c429d-dd20-40b0-bcb3-68b36c92450e" />

! Make sure to put the wife name and password correctly to the dot. Even if you miss a space or caps lock, the wifi won't work and you'll just see endless dots. That was what happened to me without realizing.. 

<img width="763" height="36" alt="Scherm­afbeelding 2026-10-09 om 10 45 09" src="https://github.com/user-attachments/assets/1ad12f23-4efc-4310-8fef-8fc4660a3546" />

### Getting the weather 
Now that we have done the wifi, we need to get the weather of course. This line retrieves the information we need. This is also the last line in the void setup. So for the next code make sure to write outside of it. 

<img width="122"  alt="Scherm­afbeelding 2026-10-09 om 10 48 32" src="https://github.com/user-attachments/assets/16abe945-9ee8-408e-8144-5d44ed43b3d0" />


### Updating the weather
We are going to create a loop. This loop constantly updates the weather every ten minutes. If you want it to be updated faster or slower, change the number, but make sure it's in milliseconds. 

<img width="250" alt="Scherm­afbeelding 2026-10-09 om 10 57 38" src="https://github.com/user-attachments/assets/fa5a5fe4-1d6d-4d87-8179-40a4259cd0cb" />

! Now you might see that the getWeather line is shown twice in the code. Don't delete neither of them because it looks wrong. I deleted one and the whole code stopped working but I realized it was because of that so I just added it back

### Checking the wifi 
Before requesting the weather, the system checks if the wifi is still connected, if not, well see it displayed in the serial monitor. 

<img width="377" alt="Scherm­afbeelding 2026-10-09 om 11 06 32" src="https://github.com/user-attachments/assets/70a5217d-49b7-423f-b635-da3b8f93c970" />

### Create an OpenWeather request
Copy these lines. The lines are a request of the information we need.

<img width="300" alt="Scherm­afbeelding 2026-10-09 om 11 13 07" src="https://github.com/user-attachments/assets/928945a0-82f0-4662-a3e3-ece33f1d18d3" />

### Receiving and reading the data 
The response is stored in the GetString, but only get shown what we need. In this case it's the temperature.

<img width="300"  alt="Scherm­afbeelding 2026-10-09 om 11 18 09" src="https://github.com/user-attachments/assets/c0115c6b-4505-42ca-9d77-51143ca77282" />

### Temperature
This part gets the temperature out of the OpenWeather and shows it in the serial monitor. 

<img width="300" alt="Scherm­afbeelding 2026-10-09 om 11 22 50" src="https://github.com/user-attachments/assets/b53071c0-b9a5-4dfa-a099-765f10022faa" />

### Choosing the led color
We are going to add colors. The system works in (R,G,B). If you want a certain color, set the letter to 255. For example if you want purple, we need red and blue, so (255, 0, 255) 

There are three ranges. The first is for temperatures under 20 which will display green, the second for temperatures under 25 that's orange and the last one for temperatures above 25, that will be red. 

It will also show a message in the serial monitor. The messages shown now are for the context of Binly, you can change it to whatever you want. 

<img width="750"  alt="Scherm­afbeelding 2026-10-09 om 11 27 48" src="https://github.com/user-attachments/assets/25ced6bb-2050-4dd4-a4a2-4a3b44b5cd3d" />

### Showing the led
This applies the color to every led. And lastly, it displays the selected color.

<img width="300"  alt="Scherm­afbeelding 2026-10-09 om 11 33 51" src="https://github.com/user-attachments/assets/47a3b3e0-2824-47b7-834a-229452276d15" />

### Running the code 
! My led strip didn't show any color at first and I got this error, first I thought my usb cable wasn't connected right, but it was my 3V pin. So if the strip doesn't work, check if all the pins are on the right place and also truly connected. 

<img width="300"  alt="Scherm­afbeelding 2026-10-09 om 11 47 20" src="https://github.com/user-attachments/assets/f49eb235-d4e7-4b32-b7e0-0668b3d05363" />


! I also got this error earlier, I found out I put the void weather in the loop. The sections should all be apart from each other. Not in the another void. 

<img width="300" alt="Scherm­afbeelding 2026-10-09 om 11 50 18" src="https://github.com/user-attachments/assets/785463fb-5d91-47e6-89c8-7df9915841db" />


! This error means that there's something wrong with the USB. For me the issue was that I once fried this port, so I cannot use it and I totally forgot about that. When I used the one on the other side it did work. 
If you get this error, try disconnecting the usb and wait a few seconds or if you have two ports, try the other one. 

<img width="500" alt="Scherm­afbeelding 2026-10-09 om 11 52 34" src="https://github.com/user-attachments/assets/27ed44ae-fa96-469e-bd5b-d53fa7b5b302" />




