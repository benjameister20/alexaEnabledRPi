# Alexa Enabled Raspberry Pi

Most of this tutorial is taken directly from [Amazon's website](https://developer.amazon.com/en-US/docs/alexa/alexa-voice-service/register-a-product.html).

---------------------------------------------------------------------------
# Register a Product

## Create an Amazon developer account
Unless you already have one, go ahead and create a free developer account at [developer.amazon.com](https://developer.amazon.com/dashboard).

## Register your prototype and create a security profile
After you've created an Amazon developer account, you'll need to create a product and security profile. This will enable your software client to connect to AVS.

Log in to [developer.amazon.com](https://developer.amazon.com/dashboard). You should be in the Dashboard by default - click the __ALEXA VOICE SERVICE__ button in the global navigation to start building products with Alexa built-in.

If your screen doesn't look like this, try the direct link to [AVS dashboard](https://developer.amazon.com/alexa/console/avs/home).

![](https://i.imgur.com/BRuqOBs.png)

If this is your first time using AVS, you'll see a welcome screen. Click __GET STARTED__, then __PRODUCTS__, then __ADD NEW PRODUCT__.

If you're a returning developer, click __PRODUCTS__ then __ADD NEW PRODUCT__.

## Fill in product information

| Note: These instructions are for developers prototyping on Raspberry Pi. If you are registering a commercial product profile, you will want to use your own custom information here. 
------------------------

1. _Product Name_: Use __AVS Tutorials Project__.
2. _Product ID_: Use __PrototypePi__. No spaces are allowed for the _Product ID_ field.
3. Select __Device with Alexa built-in__ for _Please Select Your Product Type_. Select __No__ for _Will your device use a companion app?_
4. Choose __Other__ for Product Category and write __Prototype__ in the _(please specify)_ and _Brief product description field_.
5. Select __Hands-free__ for _How will users interact with your product?_
6. Skip the _Upload_ an _image_ step. This is not required for prototyping.
7. Select __No__ for _Do you intend to distribute this product commercially?_
8. Select __No__ for _Will your device be used for Alexa for Business?_
9. Select __No__ for _Is this device associated with one or more AWS IoT Core Accounts?_
10. Select __No__ for _Is this a children’s product or is it otherwise directed to children younger than 13 years old?_
11. Click __NEXT__ to continue.

See the image below for reference

![](https://i.imgur.com/XhtWFCa.png)


## Set up your security profile

1. Click __CREATE NEW PROFILE.__
2. Enter your own custom __Security Profile Name__ and __Security Profile Description__ for the following fields - or use the below example names:
    - _Security Profile Name_: __AVS Tutorials Project__
    - _Security Profile Description_: __AVS Tutorials__
    - Click __NEXT__.
    - __Security Profile ID__ will be generated for you.
3. Select __Other devices and platforms__ from the _Web - Android/Kindle - iOS - Other devices and platforms options_ in the __Platform Information__ section.
![](https://i.imgur.com/Y1e5T4B.png)
4. Write a name for your Client ID here - you can just use __Prototype__.
5. Click __Generate ID__. You should get a Client ID and an option to download it.
![](https://i.imgur.com/DKQl950.png)
6. If you're creating this product profile on your Raspberry Pi, click __Download__ to get your credentials onto your AVS prototype. Save the config.json file to your '`/home/pi` directory. If you are creating this profile from a different PC, that's OK - you can leave the file to be downloaded later.
7. Check the box beside _I agree to the AVS agreement and the AVS Program Requirements._
8. Click __FINISH__.

Congratulations! You now have access to the Alexa Voice Service APIs. Click __OK__ on the prompt to continue.
Your device should now be listed on your [AVS dashboard](https://developer.amazon.com/avs/home.html#/avs/homes).

## Enable your security profile for commerical distribution
This tutorial is purely for prototyping on a RaspberryPi. However, if you decide later you would like to make a commerical product, you'll need to provide your customer a link to your privacy policy - follow the instructions [here](https://developer.amazon.com/en-US/docs/alexa/alexa-voice-service/activate-security-profile.html) to configure your profile.


---------------------------------------------------------------------------
# Activate Security Profile

## Enable your security profile

1. Open a web browser, and visit https://developer.amazon.com/lwa/sp/overview.html.
![](https://i.imgur.com/H8te9mI.png)

2. Near the top of the page, select the commercial device security profile you created earlier (e.g., __AVS Tutorials Project__ if you used the example values) from the drop-down menu and click the __CONFIRM__ button.
![](https://i.imgur.com/K0rD28h.png)

3. Enter your privacy policy URL beginning with http:// or https://.
4. You may upload an image. The image will be shown on the Login with Amazon consent page to give your users context.
5. Click the __SAVE__ button.
![](https://i.imgur.com/684jPHi.png)

Now that you've created your product profile, it's time to get your hardware and start building!


---------------------------------------------------------------------------
# Required Hardware
The following guide provides step-by-step instructions to set up the Alexa Voice Service (AVS) Device 1.17 SDK on a Raspberry Pi. It uses a handful of scripts to download, build, and run the AVS Device SDK with wake word detection enabled. When finished, you'll have a working sample app to test interactions with Alexa.

## Basic Tutorial
You need the following equipment to finish the basic tutorial — [Prototype with Raspberry Pi](https://developer.amazon.com/en-US/docs/alexa/alexa-voice-service/set-up-raspberry-pi.html).

- __Raspberry Pi__ - Use a Raspberry Pi 3 or 4.
- __Micro SD card__ - Minimum 8 GB.
- __USB 2.0 microphone__ - Raspberry Pi does not have a built-in microphone. To interact with Alexa you must plug in an external microphone.
- __External speaker or headset__ - Your audio source needs to connect to the Pi with 3.5mm audio cable.
- __USB keyboard and mouse__ - Choose any compatible keyboard and mouse.
- __HDMI monitor__ - Choose any compatible monitor. Alternatively, you can remote [SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/) into your Pi.
- __Internet connection__ - Ethernet connection or a 2.4 GHZ Wi-Fi.

For a list of Amazon's recommended parts, see [here](https://www.amazon.com/ideas/amzn1.account.AGPAZ4ESD2KHDFMOAYU7NDDYNBAA/8JYBRL3A82AN?ref=idea_share). For the exact parts in this tutorial, see [here]().

Next, [set up your Raspberry Pi](#Set-Up-Raspberry-Pi) and install the software required to run the SDK.


---------------------------------------------------------------------------
# Set Up Raspberry Pi

## Download Raspbian NOOBS to a Micro SD Card

|  Note: Some Raspberry Pi kits ship with a preinstalled version of NOOBS. Check your device packaging for verification. Amazon's parts list includes an SD card that does not have NOOBS installed. This guide's recommended parts list comes with a pre-installed NOOBS card. 
------------------------

Before powering on your Raspberry Pi, you must download an operating system (OS) — using your Linux, MacOS or Windows PC — and copy it to an SD Card. For this tutorial, we're using Raspbian NOOBS OS version 2.9.0.

1. With your PC, download [NOOBS_v2_9_0.zip](http://downloads.raspberrypi.org/NOOBS/images/NOOBS-2018-10-11/NOOBS_v2_9_0.zip), and unzip it locally.
2. Open the unzipped __NOOBS_v2_9_0__ folder and drag and drop the entire folder contents onto an empty 8/16/32gb microSD card.

![](https://i.imgur.com/LfNH6GZ.png)

## Connect Hardware to your Raspberry Pi

Make sure you're not missing any required hardware — otherwise, you'll get stuck at some point. For example, the sample app doesn't run without a USB microphone plugged in.

1. Insert your micro SD card into the card reader on the Pi. The SD card contacts should face up.
2. Plug in a USB microphone.
3. Plug in earbuds — or a speaker — into the 3.5mm audio jack on the Pi.
4. Connect a USB keyboard and mouse. Make sure you don't cover the USB mic.
5. Connect a monitor using the HDMI port.
6. Connect an Ethernet Cable — if your not using Wi-Fi.
7. Plug the micro USB power supply into the Pi.

Your setup should look similar to the following images.

![](https://i.imgur.com/HPX5Rca.jpg)

## Power on your Raspberry Pi
Connect the Pi to a power source. A loading screen automatically launches and walks you through some steps before booting to desktop. If you run into any errors, try booting from a different pre-imaged micro SD card. If nothing happens after that, make sure that your micro SD card is facing the correct direction with the contacts facing up.

## Install the Raspbian OS

| Note: Use Raspbian Stretch or Raspbian Buster with the AVS Device 1.17 SDK.
------------------------

Upon successful startup, you're prompted to select an operating system and locale. NOOB always retrieves the latest version of Rasbian that is avaialble.

1. Check the box next to __Raspbian [RECOMMENDED]__.
2. Select your language and keyboard preferences at the bottom of the screen.
    - Make sure you select the correct locale/keyboard layout for your region, otherwise you might have problems with pre-existing passwords that contain special characters. Some keyboard layouts don't support special characters. To test your layout, enter a special character and confirm that it appears on the screen, before proceeding to the next step.
3. Click __Install__ in the upper left corner of the pop-up box.

It should take around 15 minutes to fully install. After it's done, you'll see a success message. Click __OK__ and the desktop loads — feel free to close the window when it asks you to change your password or do any other setup steps.

## Setting up Virtual Network Computing (VNC)
TODO

## Configure OS Settings
Configure the following OS settings before building the AVS Device SDK.
![](https://i.imgur.com/P14xNn5.png)

### Network
Connect your Pi to a network. You can choose either option.

- __Ethernet__: Plug an ethernet cable into the Pi. The OS automatically connects to your network.
- __2.4 GHz Wi-Fi__: Click the __connectivity__ icon in the __top-right corner__ of the toolbar, select an SSID, and enter your credentials.

Verify that you're connected to a network by opening a web browser — click on the __globe icon__ in the top-left toolbar and navigate to a website.

### Audio
A Raspberry Pi can output sound through two different channels, an HDMI port or a 3.5mm audio jack. HDMI is the default selection when you install a fresh OS. To output sound to your speaker, change the output channel on your Pi to __3.5mm audio jack__.

1. Right-click on the speaker graphic in the upper-right hand corner of your Pi.
2. Select __Analog__.
3. 
You should also turn up the volume the microphone.

1. Go to __Audio Device Settings__.
2. Select __Change Sound Card__.
3. Select the drop down and select __USB PNP (Asla mixer)__.
4. Select __Controls__.
5. Click the microphone and change the volume to max.


### Keyboard
You can change your keyboard settings.

1. Click on the Raspberry icon in the top right of your desktop.
2. Select __Mouse and Keyboard settings__ from the __Preferences__ menu.
3. Click __Keyboard Layout__ from the __Keyboard__ tab.
4. Select the appropriate configuration. Make sure whatever you pick, you can write characters such as "quotes" and @ symbols.


### Update Pi Packages List
Now that you're connected to a network, check if your Pi needs updating — the SDK might not run properly with outdated packages.

Open a terminal by clicking on the black window logo near the top left corner of your toolbar. You should be in the `/home/pi` directory. Enter the following command.

```
cd /home/pi/
sudo apt-get upgrade
```

| Note: This guide presumes that you're using the default home directory of `/home/pi`. If you choose to use different folder names, update the commands throughout this guide accordingly.
------------------------
 
Next, [register an AVS product and create a security profile](#Input-AVS-Credentials) for your device.



---------------------------------------------------------------------------
# Input AVS Credentials
Before you build the AVS Device SDK, you need to register an AVS product and create a security profile. When finished, you download a config.json file that contains your client ID and client secret. These retrieve access and refresh tokens that authorize your interactions with Alexa.

## Download your Config.json File
|  Note: If you haven't registered your product yet, complete the Create Product Profile tutorial to generate your config.json file.
------------------------

You need to download your config.json file and move into your `/home/pi` folder. You might have already done these steps if you completed the [Create Product Profile]() tutorial. If so, skip to the next section, [Build the AVS Device SDK]().

1. Log into your [AVS dashboard](https://developer.amazon.com/alexa/console/avs#/avs/home).
2. Click on your Product Name (it should be __AVS Tutorials Project__ or whatever you named it when creating the product profile).
3. Under the __Product Details__ menu, select __Security Profile__.
4. Choose __Other devices and platforms from the Web - Android/Kindle - iOS - Other devices and platforms__ from the menu.
5. Click __Download__. The config.json file appears in your `/home/pi/downloads` folder. In the file manager, copy this file from the `/downloads` folder and place it in your `/home/pi` folder as shown in the picture below.

![](https://i.imgur.com/J3XeIFf.png)

Next, [build the AVS Device SDK]() to voice-enable your prototype.



---------------------------------------------------------------------------
# Build the AVS Device SDK
## Download the SDK Configuration Scripts
Next, get the AVS Device SDK configuration scripts from the AVS SDK Github repo. These scripts contain all the logic to build the SDK with single command. When you run them, they download the AVS Device SDK and install any required dependencies. These scripts get updated with each SDK release and automatically download the latest SDK for you.

Open your terminal to the `/home/pi` directory. Enter the following command as single block statement:
```
wget https://raw.githubusercontent.com/alexa/avs-device-sdk/master/tools/Install/setup.sh \
wget https://raw.githubusercontent.com/alexa/avs-device-sdk/master/tools/Install/genConfig.sh \
wget https://raw.githubusercontent.com/alexa/avs-device-sdk/master/tools/Install/pi.sh
```
![](https://i.imgur.com/irvo4Jr.png)

## Run the Install Script
The __setup.sh__ script builds the SDK and installs dependencies that allow your device to the following.

- Maintain an HTTP/2 connection with AVS.
- Play Alexa TTS and music.
- Record audio from the microphone.
- Store records in a database (persistent storage).

To run the install script, open a terminal and run __setup.sh__ using your __config.json__ file and a device serial number (DSN) as arguments. If you get an error, make sure your config.json file is in the same folder as the setup.sh script.

```
cd /home/pi/
sudo bash setup.sh config.json [-s 1234]
```

The field in brackets is the __Device Serial Number__ which is unique to each instance of the SDK. In the example, it's pre-populated with 1234. If you don't supply a DSN, the SDK generates of default value of 123456.

![](https://i.imgur.com/sr5fAgW.png)

## Agree to the Terms and Conditions

### Third-party Libraries
When prompted with the licensing terms from our third-party libraries, enter __AGREE__ — Unless, of course, you disagree! Agreeing to the conditions starts the installation process which might take over 20 minutes.

### Sensory Wake Word
At some point, the SDK installation pauses and asks you to accept Sensory Wake Word's terms and conditions — you must type __yes__ to accept. The __Wake Word Engine__ (WWE) from Sensory compares incoming audio to an onboard model of a wake word (e.g., __"Alexa"__), and initiates the transmission of audio to the cloud when triggered.

The WWE is for __prototyping devices only__. If you intend to ship a commercial device, you must get a WWE license.

| Note: The AVS Device SDK is modular and flexible. When you're ready to build your product, you're able to change your WWE. Remember that for AVS products, the wake word must be __Alexa__ so that your customers aren't confused about how to interact with your device.
------------------------

Once you've finished compiling, a success message appears — __[100%] Built Target SampleApp__. If your device freezes - don't worry, restart it by unplugging your Pi's power cord. When you get back to your desktop, re-run the above setup.sh command to finish your install.

![](https://i.imgur.com/C2T5our.png)

Next, [launch the sample app and get a refresh token from AVS](). A refresh token allows your device to authenticate with the cloud via Login With Amazon (LWA).



---------------------------------------------------------------------------
# Get a Refresh Token
Your Raspberry Pi now has the AVS Device SDK installed and your credentials loaded, but your device still needs a __refresh token__ so your client maintains a connection to the Alexa Voice Service. If you design an Alexa-enabled product and ship a million of them to your customers, they can all use the same Client ID and ProductID - but each _individual_ device will require a __unique refresh token__ to authenticate with AVS through Login With Amazon (LWA).

Normally, your customer gets a refresh token delivered when they activate your (their) device using a companion app, companion site, or [code-based linking](https://developer.amazon.com/en-US/docs/alexa/alexa-voice-service/code-based-linking-other-platforms.html) (CBL). For this tutorial, you're both the device maker _and_ the customer. You use the __startsample.sh__ script to launch the Sample App and request a refresh token for your prototype device.
## Start the Sample App
In a terminal window, navigate to the `/home/pi` directory and run __tartsample.sh__.

```
cd /home/pi/
sudo bash startsample.sh
```
|  Warning: The sample app won't run without a working USB microphone connected to your Pi.
------------------------

## Get your Authorization Code
Once the sample app starts, you'll see a series of rapidly scrolling debug messages in the terminal window stating, __Checking for authorization__. Scroll through the debug messages and look for a box with a URL, it contains your Alexa authorization code.

| Note: Don't close the sample app after you find the authorization code.
------------------------

## Submit your Authorization Code

1. Go to amazon.com/us/code. Use any internet-connected device (for example, your phone).
1. Log in with your Amazon developer credentials.
3. Enter the authorization code, provided by your sample app, into the authorization box.

It might take up to 30 seconds for `CBLAuthDelegate` to successfully get a refresh token from Login With Amazon (LWA). You'll get a success message, and your sample app should be ready to go!

![](https://i.imgur.com/ybonPFI.png)

Your hard work has paid off, and now it's time to [Talk with Alexa]()



---------------------------------------------------------------------------
# Talk with Alexa
Congratulations on creating your first prototype with Alexa built-in! If your sample app is still running, you should see ASCII art indicating that Alexa's status is `IDLE`, meaning the client is waiting for you to initiate a conversation.

To test your prototype, put your earbuds in, and say __"Alexa"__ into the microphone to trigger the __Wake Word Engine__. Because you're using an inexpensive USB microphone, you might need to speak closer to your microphone to ensure your voice is heard. When you build a commercial Alexa-enabled product, you can use a high-performance __Audio Front End__ (AFE) to pick up your customer's voice. Check out the [dev kits for AVS page](https://developer.amazon.com/en-US/alexa/alexa-voice-service/dev-kits) to learn more.

When you say __"Alexa"__, you should see a bunch of messages scroll in your terminal window. One of those will show the status changing to `Listening`, indicating the wake word has been recognized. Then say __"Tell me a joke."__ If Alexa responds with `Thinking...`, then `Speaking`, you have a working prototype… and probably, a very bad joke.

![](https://i.imgur.com/XSk9n4m.png)

## Troubleshooting
If you don't hear anything over your earbuds, check that your audio output is set to __"Analog"__ by right-clicking on the speaker icon in the top-right corner of your Pi's screen. Your audio output might be set to HDMI by default. Also ensure your speaker/earbuds are turned on and plugged into your Raspberry Pi's __3.5mm audio jack__.

If Alexa isn't responding or your Sample App appears __stuck__ (or displaying error messages when you try to speak), just type __"s"__ and hit return to stop that interaction. You can also type __"q"__ and hit return to exit from the Sample App, or just close the terminal window to force quit the Sample App.

At any time, to relaunch the sample app you can just type the following into a terminal window:

```
cd /home/pi/
sudo bash startsample.sh
```

## Interactions
### Talk with Alexa!
- Say "Alexa", then ask "What time is it?"
- Say "Alexa", then ask "What's the volume of a sphere?"
- Say "Alexa", then say "Who is Rich King?"
- Say "Alexa", then say "How did the stock market do today?"
- Say "Alexa", then ask "Where were you born?"
- Say "Alexa", then say "How do you say friend in Russian?"

### Try a multi-turn interaction
Say __"Alexa"__, then ask __"Set an alarm"__. When she asks what time, just say a number, like __"8"__. She'll want to know if that's __"AM"__ or __"PM"__.

You probably noticed that despite having a bit of back and forth with Alexa, you only said the wake word once at the start of the conversation. This is called a __multi-turn interaction__ and it's a more natural method of communication because you can continue speaking without starting every phrase with "Alexa."

In your terminal window, you can scroll up until you see the UI state `Listening...`. Right above that you'll see that the state of the __Audio Input Processor__ (AIP) has changed from `IDLE` to `EXPECTING_SPEECH` and then `RECOGNIZING` - without you speaking the wake word!

![](https://i.imgur.com/yTtdsWY.png)

__Alexa only listens when customers indicate that they want to speak to the cloud.__ Typically, this means the AIP was triggered by the Wake __Word Engine__ running on the client. In this case, it's been activated via a Directive delivered down to your client from the cloud. When Alexa asks __you__ a question, the AIP activates because it knows the customer wants to provide a response.

You can learn more about multi-turn interactions [here](https://developer.amazon.com/en-US/docs/alexa/alexa-voice-service/speechrecognizer.html#expectspeech).

#### Other multi-turn interactions to try
- Say "Alexa, Wikipedia." You'll have the option to request information on a number of topics without speaking the wake word before the subject.
- Say "Alexa, let's chat." Initiate a conversation with a chatbot.
- Say "Alexa, play Yes Sire." Play a medieval-themed game using your voice, entirely in multi-turn interactions.

### Multi-lingual interactions
Today, Alexa can speak Japanese, German, and many global dialects of English. To try some of these settings, type `c` and hit return. Then type `1` to see language options. When you ship your product with Alexa Built-in and your customer wishes to change languages, your device will need to send a `SettingsUpdated` event to the cloud. Learn more by clicking [here](https://developer.amazon.com/en-US/docs/alexa/alexa-voice-service/settings.html#settingsupdated).

![](https://i.imgur.com/W5OCRly.png)

There's lots more to learn - let's start by setting our [device location]()!



---------------------------------------------------------------------------
# Set Device Location

On your brand-new prototype, ask Alexa what's the weather. She probably doesn't give you the exact response you were hoping for. This is because the __Alexa Voice Service__ doesn't know where your device is. You need to set your location to get local movie times, weather, and other __location-specific information__.

1. Open a web browser on any device and go to Alexa.amazon.com. On a commercial product, your customer could also specify this in the Amazon Alexa App on their phone.
2. Navigate down to the __Settings__ tab.
3. Select the device you created. You identify it by your unique __Product Name__ you created earlier. If your sample app is still up and running, you should see status as "Online".
4. Select your device, and change the location by __Zip Code__ to whatever you prefer.

![](https://i.imgur.com/XCYuVVR.png)


You don't need to restart your sample app to see the change. As soon as you update your settings in the cloud, you'll receive data for that location. Try asking Alexa what the weather is again and see where your device is now "located".

Feel free to click back on your __"Home"__ tab on the left-side menu of Alexa.Amazon.com. You'll find a lot of interesting settings to experiment with. When you're ready to do more with your Alexa-enabled prototype, check out the [Advanced Pi Tutorials]()!