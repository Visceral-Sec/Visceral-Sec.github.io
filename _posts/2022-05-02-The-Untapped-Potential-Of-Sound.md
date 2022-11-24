---
layout: post
title:  "The Untapped Potential of Sound"
date:   2022-10-28 13:37:00 -0700
categories: Psychology, Cyber-Security
---
# The Untapped Potenital of Sound within Cyber-Security

-----

Other areas of IT such IOT, VR and modern game consoles have adopted incorpating new senses in full swing, so why does cyber-security refuse to budge from it's traditional monitor/mouse and terminal setup? 


The answer is simple: **There's no point.** 

What benefit would a gesture-control meterpreter shell really offer? 

Would being able to interact with your SIEM using your voice really provide anything other than *wow-factor* for stakeholders?

From a cyber-sec perspective, vision is really the only relevant sense. However I think with how easily we can answer this question, we might be missing something.

This line-of-thought was what brought me and some collegues from university into quesitoning how we could find anyway at all we could make additional senses impactful. [I'd heard of sound having some strange niche
impact on disk latency](https://www.youtube.com/watch?v=tDacjrSCeq4), Therefore I brought up how sound probably *sounded* the most promising.

At some-point we joked around about how if we linked up network traffic to a synthesier we could pull some trickery to emulate the [Imperial March](https://www.youtube.com/watch?v=-bzWSJG93P8) or [Vivaldi's winter](https://youtu.be/TZCfydWF48c?t=70). 

After letting this thought sit for a hot minute, letting my brain run through the possibilites; The **potential** this joke idea had dawned on me.

# The marvelous simplicity


Understanding the inner intericates of hearing is a huge topic, one which is wayyyyy out of scope for this blog. I'm a cyber-security student, so I'm going to take a couple liberities in the applying the theories and ideas proposed here.

Imagine living in a flat, you're lucky enough to have a on-suite but your unlucky enough to have an loud extractor fan. Every-day this fan drones on; emitting it's characteristic hum so much so that it's reduced to background noise. However, one-day the tone shifts. It's such a minimal detail, but you notice it practically instantly. Brought to the full-front of your consciousness without a choice.

If we apply the same logic of noticing a changes in background noise from a cyber-security perspective, we can see a similar pattern to anomlouous based detection. <sub><sup>generally</sup></sub> Anomlous based detection consists of using a baseline (the background noise) to identify anomlous activity. (The tonal shift).

Which leads me to the proposed idea:

What if we could potentially use our own couscious processing as a anomlous detection system?

# Code Proof Of Concept

I develve into this idea a little further, I decided to whip up a quick python proof concept to try and replicate something close to what I envisoned.

I decided to use [scapy](https://scapy.net/) to handle the intrsicates of the network stack and through the magic of python libraries managed to start reading network traffic with just one line:
```
sniff = scapy.sniff(prn=lambda x:protocolExtractor(x.summary()))
```
The "prn" paramater allows me to individually execute a lambda function on each packet. This prevents me from having to code a queue system for the packets and as the code isn't multi-threaaded they should automatically queue. Additionally, I can pass a summarisation of the packet using .summary, which as we only really need to know what type of packet is saves me a lot of parsing. This one line of code alone really allowed me to get this proof of concept going without too much issue. Highly recommend scapy if anyone wants to mess around anything network based in python.

With network traffic now flowing, I needed to develop a method of identifying what a packet was. For this POC I decided that protocols were the eaiest way to differentiate between packets.
Thankfully, using .summary, scapy present the packets in the following format:
```
Ether / ARP who has 172.16.3.76 says 172.16.0.1 / Padding
```
Using python's .split method I can pretty simply differate the different protocol layers and it's summarised data:
```
packetSplit = scapyPacket.split("/") # Splits up the layers
    # Loops through the split array
    for i in range(len(packetSplit)):
            protocolHandler(packetSplit[i], i)
```
Afterwards I load in the packet into a class using a simple switch statement (requires python 3.10+ to use) and then the objecti s passed to the synthesier function.
```
 def protocolHandler(protocol,layer):
        # Loads the Classes
        if "Raw" in packetSplit[i]:
            #call the synthesier
            PacketSynthesizer(packetProtocols)
        else:
            match layer:
                case 0:
                    packetProtocols.L1 = protocol
                case 1:
                    packetProtocols.L2 = protocol
                case 2:
                    packetProtocols.L3 = protocol
                case 3:
                    packetProtocols.L4 = protocol
                case 4:
                    packetProtocols.L5 = protocol
                case 5:
                    packetProtocols.L6 = protocol
                case 6: 
                    packetProtocols.L7 = protocol
```
Not exactly the most eloequent of solutions but works well enough for a proof of concept.

The synthezier function quite simply searchs for substrings within the different protocols and plays a sound accordingly. For example HTTP packets will play "Sounds/Piano11.mp3". 
```
def PacketSynthesizer(packetProtocols):
    #https://docs.oracle.com/cd/E19455-01/806-0916/ipov-10/index.html
        # Called Once transport layer is reached (Done for readability, not the most efficiency)
    def transportLayer(packetProtocols, networkinterface):
        if "TCP" in packetProtocols.L3:
            if "HTTP" in packetProtocols.L3:
                playsound('Sounds/Piano11.mp3', False)
            elif "DHCP" in packetProtocols.L3:
                playsound('Sounds/Piano15.mp3', False)
            elif "BGP" in packetProtocols.L3:
                playsound('Sounds/Piano18.mp3', False)
            elif  "HTTPS" in packetProtocols.L3:
                playsound('Sounds/Piano122.mp3', False)
            elif  "TLS" in packetProtocols.L3:
                playsound('Sounds/Piano17.mp3', False)
            else:
                playsound('Sounds/Piano13.mp3', False)
        elif "UDP" in packetProtocols.L3:
            if "DNS" in packetProtocols.L3:
                playsound('Sounds/Piano11.mp3', False)
            elif "SSDP" in packetProtocols.L3:
                playsound('Sounds/Piano19.mp3', False)
            if "SSDP" in packetProtocols.L3:
                playsound('Sounds/Piano114.mp3', False)
            if "QUIC" in packetProtocols.L3:
                playsound('Sounds/Piano18.mp3')
            else:
                playsound('Sounds/Piano125.mp3', False)
        else: 
            print("not fully implemented (POC)")

    if packetProtocols.L1 == "Ether ":
        match packetProtocols.L2:
            case " IP ":
                transportLayer(packetProtocols, "IP")
            case "ARP":
                playsound('Sounds/Piano125.mp3', False)
            case "ICMP":
                playsound('Sounds/Piano113.mp3', False)
    elif packetProtocols.L1 == "Token Ring":
        print("Not Implemented")
    else:
        print("Not fully implemented (POC)")
```

All Code can be found here:
[Git-Hub Siren.py](https://github.com/Visceral-Sec/Siren.Py)

# Conclusion

For a more specific example, I envison security operation theatres (SOCs) using this noise at just a low enough volume as to where it becomes meer background noise but any major changes are audible. 
