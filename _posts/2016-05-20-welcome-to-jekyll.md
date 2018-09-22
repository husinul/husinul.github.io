---
layout: page
title:  "IoT Protocols Introduction"
subtitle: "A minimal Jekyll theme"
date:   2018-05-20 21:21:21 +0530
categories: ["IoT"]
---

1. **Infrastructure**(ex: 6LowPAN, IPv4/IPv6, RPL)
2. **Identification**(ex: EPC, uCode, IPv6, URIs)
3. **Comms / Transport** (ex: Wifi, Bluetooth, LPWAN)
4. **Discovery**(ex: Physical Web, mDNS, DNS-SD)
5. **Data Protocols**(ex: MQTT, CoAP, AMQP)
6. **Device Management**(ex: TR-069, OMA-DM)
7. **Semantic**(ex: JSON-LD, Web Thing Model)
8. **Multi-layer Frameworks**(ex: Alljoyn, IoTivity, Weave, Homekit)

#### IoT Data Protocols:
1. **CoAP** (Constrained Applications)
2. **MQTT** ( Message Queue Telemetry Transport)
3. **XMPP** (Extensible Messaging And Presence Protocol)
4. **AMQP** (Advanced Message Queuing Protocol)

**CoAP** (Constrained Applications):

The Constrained Application Protocol (CoAP) is a specialized web transfer protocol for use with constrained nodes and constrained networks in the Internet of Things.
The protocol is designed for machine-to-machine (M2M) applications such as smart energy and building automation.Constrained networks means It is particularly targeted for small, low-power sensors, switches, valves and similar components that need to be controlled or supervised remotely, through standard Internet networks

CoAP was developed as an Internet Standards Document, RFC 7252. The protocol has been designed to last for decades. The Internet of Things cannot spread as long as it can be exploited by hackers nilly-willy. CoAP does not just pay lip service to security, it actually provides strong security. CoAP’s default choice of DTLS parameters is equivalent to 3072-bit RSA keys, yet still runs fine on the smallest nodes

CoAP Security:

. DTLS (TLS on UDP Datagrams)

. Pre-shared key or not

. DTLS is not really light


**MQTT** ( Message Queue Telemetry Transport):

This is a light weight protocol for Internet of things and it is mainly used for the wireless applications.It is designed for connections with remote locations where a “small code footprint” is required or the network bandwidth is limited. The publish-subscribe messaging pattern requires a message broker.

And it is worked on the TCP/IP Protocol.

The protocol uses a publish/subscribe architecture in contrast to HTTP with its request/response paradigm

MQTT was invented by Dr Andy Stanford-Clark of IBM, and Arlen Nipper of Arcom (now Eurotech), in 1999.

MQTT Security :

. Uses SSL/TLS on top of the TCP stream.

. Pre-shared key encryption is supported.

 
**XMPP* (Extensible Messaging And Presence Protocol):

**XMPP** is a communications protocol for message-oriented middleware based on XML (Extensible Markup Language).It enables the near-real-time exchange of structured yet extensible data between any two or more network entities.

XMPP provides a general framework for messaging across a network, which

offers a multitude of applications beyond traditional Instant Messaging (IM) and the distribution of Presence data, Gtalk and Whatsapp services is using the XMPP.

**AMQP** (Advanced Message Queuing Protocol):

AMQP is a binary wire protocol which was designed for interoperability between different vendors. Where other protocols have failed, AMQP adoption has been strong. Companies like JP

Morgan use it to process 1 billion messages a day.

. It is used in one of the world’s largest biometric databases India’s , Aadhar project—home to 1.2 billion identities.
. It is used in the Ocean Observatories Initiative—an architecture that collects 8 terabytes of data per day.
