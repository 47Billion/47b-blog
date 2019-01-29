---
layout: post
title:  "Introduction to Raspberry pi"
author: prakhar
categories: [ programming, technology ]
image: assets/images/2019-01-15-introduction-to-raspberry-pi-1.jpeg
featured: false
hidden: false
---

If you are related to IT industry in any way, you must have come across the name Raspberry Pi. If not, you are not doing your job right. Anyway, let us discuss what Raspberry Pi is and why you need it in your life (No this article is not click bait and I do not sell Raspberry Pi). Let’s start with what is raspberry pi. To quote the official website –

“The Raspberry Pi is a low cost, credit-card sized computer that plugs into a computer monitor or TV, and uses a standard keyboard and mouse. It is a capable little device that enables people of all ages to explore computing and to learn how to program in languages like Scratch and Python.”

Now that description may make it sound like a children’s learning toy, but don’t let it fool you. Raspberry Pi is one of the most powerful and flexible platforms available in the market. Originally it was created with the purpose of teaching children but the specifications of the product combined with reviews of alpha releases and proof of concept Linux image were more than enough to make developers realize its true potential causing this on the day of launch –

*“The web-shops of the two licensed manufacturers selling Raspberry Pi’s within the United Kingdom, Premier Farnell, and RS Components, had their websites stalled by heavy web traffic immediately after the launch (RS Components briefly going down completely). Unconfirmed reports suggested that there were over two million expressions of interest or pre-orders. The official Raspberry Pi Twitter account reported that Premier Farnell sold out within a few minutes of the initial launch, while RS Components took over 100,000 pre-orders on day one.”*

## Why you should get one

1. It’s a complete computer at the size of a credit card that runs with your phone charger.

2. It has onboard Wi-Fi, Bluetooth, RJ-45, 4 USB ports, HDMI and 3.5mm audio.

3. It has 26 GPIO (general purpose input output) pins that allow you to interact with a wide range of sensors and peripherals. And programming them is as simple as importing a library and calling a method with the desired output.

4. It costs just Rs.3,000 (Pi zero is smaller and much cheaper).

5. It has support for all popular languages including C++, Java, Python, NodeJS etc.

6. The community is simply awesome. You can get step by step instructions on how to build practically anything you can think of, including the code. In case you run into a very specific problem, just post it online and people will help you with all kinds of solutions.

Most technical minded people can figure out what that means but still let me give a basic explanation

1. Because of its size and power option, it can be installed anywhere and automate anything.

2. Since everything is onboard, you don’t have to worry about all the attachments and dongles and whatnot just to connect to the device.

3. The low cost means that you do not have to worry about project cost whether you are making something as a hobby or trying to build something commercially.

4. The low cost also means that you have the option to go with a distributed implementation and use multiple devices.

5. The applications of GPIO are limitless but the general idea is that you can use any real-world event as a digital trigger for your program using sensors and automate things using simple code.

## Purchasing guide
If you are planning on buying a new raspberry pi, it’s really important to know which one best suit your needs and what extra things you need to get. Here is a list of things you will need –

### Board

  You will obviously need the Raspberry Pi board but there are options available. If you have nothing in particular in mind and buying it just as a hobby, you will have to choose between 3b and 3b+. Although there is not much difference in price and 3b+ as the name would suggest is the newer and better version, the problem is compatibility. The 3b+ is NOT backward compatible with 3b, so if you have found some project online and just want to build it, make sure to get the right version. The older operating systems do not boot on 3b+. But if you think long term the 3b+ is definitely a better option. Another option is Raspberry Pi Zero W. If you are planning on building something that requires low processing and you want the project to be low cost then this is the option for you. Its size and configuration are half of the regular model. It also requires additional connectors since it comes with micro USB and micro HDMI as inputs. DO NOT buy Raspberry Pi Zero, which is the older model without Bluetooth and Wi-Fi. Zero W and Zero WH are the same except WH comes with the header pins soldered.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-01-15-introduction-to-raspberry-pi-2.jpeg" alt="Board"/>
  <figcaption>Board</figcaption>
</figure>

_Raspberry Pi 3b_
Pros — Compatible with most online available projects

Cons — Lower configuration than 3b+ at almost the same prize

_Raspberry Pi 3b+_
Pros — Latest model with higher configuration and better support for future products.

Cons — No backward compatibility

_Raspberry Pi Zero_
Pros — Half in both size and price.

Cons — Lower configuration than both 3b and 3b+ and requires adapters for micro USB and HDMI

### SD card

  RPi uses a micro SD card for storage. Usually, 8 GB is enough space, even 4GB is fine if you don’t need much storage space but going above 16 GB will require additional tools for formatting the card. The important thing to keep in mind that since OS is installed on the card the performance of your system is greatly affected by the speed of your card. If possible go for class 10 card or above. As for installing the OS, there are preinstalled cards available but the installation process is not much different from installing a regular software so I wouldn’t recommend them if they cost extra.

### Case 

  Raspberry Pi is an open board with metal contacts everywhere, so to avoid any short-circuits you should consider buying a case.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-01-15-introduction-to-raspberry-pi-3.jpeg" alt="Case"/>
  <figcaption>Case</figcaption>
</figure>

### Breakout kit 

  If you are planning on playing with the GPIO pins and do not have experience with handling electronic components, you should consider purchasing a breakout kit. It will make your work much easier and it will reduce the chances of causing damage to the pins. Just search for t-cobbler with cable. You should also get a breadboard and some Dupont cables.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-01-15-introduction-to-raspberry-pi-4.jpeg" alt="Breakout Kit"/>
  <figcaption>Breakout Kit</figcaption>
</figure>

### Sensors 
  
  There2019-01-15-introduction-to-raspberry-pi-1. are all kinds of sensors available for raspberry pi from motion and proximity to touch and rain sensors. They are usually quite cheap. Just look for them on any online electronic components store.

## Getting Started
The first thing you will need to do is choose an OS for your pi. The best way to install the OS is to download NOOBS (New Out Of Box Software) zip file from here extract files to the formatted card and plug it in the pi. When you turn it on it will give you the choices for available OSs through a simple UI and downloads and install the selected one for you. Another option is to download an image of the OS of your choice and write it to the card using etcher. Select image file, select drive (your card), click flash and you are done. The official OS by Raspberry Pi Foundation is Raspbian. It is a Debian based Linux distribution optimized for raspberry pi hardware. The Lite version comes without a desktop so it is much smaller but, for beginners, I would recommend going for the desktop version. At the first start, you will get a popup that will guide you through the configuration. In case you don’t you can set up your Wi-Fi through Menu (logo on the top left) > Preferences > Raspberry Pi configurations. You will need to set up Wi-Fi country under the localization tab before you can connect to a Wi-Fi.

In case you want to experiment a bit there are some interesting operating systems available like-

### RISC OS

  It is a really small and fast operating system. The desktop version image with applications installed is about 120 MB and the command line version is just 4 MB.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-01-15-introduction-to-raspberry-pi-5.png" alt="RISC OS Desktop"/>
  <figcaption>RISC OS Desktop</figcaption>
</figure>

### RetroPie 

  Retro pi is built on top of Raspbian. It converts your raspberry pi into a retro gaming machine. It contains emulators for a large number of old gaming platforms including Nintendo, Gameboy and Sony consoles. With some effort, you can build your own arcade machine.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-01-15-introduction-to-raspberry-pi-6.jpeg" alt="RetroPie"/>
  <figcaption>RetroPie</figcaption>
</figure>

### OSMC 

  Open Source Media Center, or OSMC, is a standalone Kodi operating system. I basically turn your raspberry pi into a media player. If you are planning on building something serious then there are various soundcards available too.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-01-15-introduction-to-raspberry-pi-7.jpeg" alt="OSMC"/>
  <figcaption>OSMC</figcaption>
</figure>

## Projects
The best thing about raspberry pi is that its applications are limitless. It is a really small computer that can connect to your wired or wireless network and run headless, that itself can give you a lot of ideas if you are a tech guy. But what increases these possibilities exponentially are the GPIO pins. These pins are capable of taking input from all kinds of sensors and give it to your code as input. Now you can take that input, process it as you wish and give an output locally, to your network or to any device connected to your GPIOs. There is no limit to what you can achieve through that. As for the ideas, you can search for Raspberry Pi projects and you will get thousands of them with full instructions. A good place to look for projects is Hackster.io.
2019-01-15-introduction-to-raspberry-pi-5.
Raspberry Pi’s are being used for all kinds of projects from home automation and voice AI projects to serious 750 node cluster used as supercomputing testbed. There are stack cases and liquid cooling potions available when used in clusters for heavy processing. Here is a simple 7 node cluster.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-01-15-introduction-to-raspberry-pi-8.jpeg" alt="Raspberry Pi Cluster"/>
  <figcaption>Raspberry Pi Cluster</figcaption>
</figure>

## How do we use Raspberry Pi at 47Billion

At 47Billion, we use Raspberri Pi boards in both production and pre-production testing modes.

. We used Raspberry Pi to run a streaming media server. This server is used to stream movies and songs to a mobile app running on the same wifi network as Raspberry Pi. This setup is deployed in buses and trains to provide streaming media services to passengers on local WiFi without need of expensive and flaky provider internet data connection.

. We use Raspberry Pi to run Amazon Alexa services as an alternative to Amazon Echo 

. Raspberry Pi is a perfect hardware to test home automation and connected sensors. We have multiple projects where it is being used for testing sensor and automation.

. Our latest project involves running Google's TensorFlow on Raspberry Pi to develop products with Artificial Intelligence on the edge.
