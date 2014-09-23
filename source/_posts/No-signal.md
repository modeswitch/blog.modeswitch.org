title: No signal
tags: Mesh Networking
categories: Technology
date: 2014-09-22 00:00:00
---

My latest side project involves bringing wifi mesh network support to Firefox OS. This is the first of several articles on the subject, and in this part I'll cover the current state of device connectivity, the limitations of those approaches, and how adhoc mesh networking provides a way around those limitations.

<!-- more -->

Connectivity is rarely a problem if you have access to a cellular network. But what happens when you have no signal?

## Where we are today

Imagine you're waiting for the subway. When it arrives and you get on, three of your friends are there playing a multiplayer game on their phones. They invite you to join them. One of them is running a Wi-Fi hotspot, so she gives you the password and you connect. After a few stops she has to leave. Because her phone is the Wi-Fi hotspot through which the other three phones are connected, when she leaves the network will dissolve and the game will end. One of the remaining players will have to set up a new Wi-Fi hotspot before they can continue playing.

Now imagine your country is in the midst of a political revolution. The government has shut down the connection to the public internet and is monitoring phone and data traffic on cellular networks. (This may sound contrived, but it actually [happens](http://en.wikipedia.org/wiki/Internet_censorship_in_the_Arab_Spring).) There are some open Wi-Fi access points at cafes and in people's homes, but they no longer provide internet access. It's possible to connect to other devices on these open Wi-Fi LANs but communication across LANs is not possible and there's no coverage outside. Some people are running mobile Wi-Fi hotspots on their phones, but each hotspot can only support a few connected devices and users can't communicate with each other if they're on different hotspots.

There are several interesting problems encountered in the scenarios above:

* Centrally-controlled networks are not robust against government censorship or surveillance
* Cellular and Wi-Fi rely heavily on fixed infrastructure (access points or cell towers)
* Mobile Wi-Fi hotspots don't scale

## Ad-hoc Wi-Fi mesh networking

You're probably aware or Wi-Fi __STATION__ mode, where your device connects to an existing access point (in some cases prompting you for a password), and __AP__ (hotspot) mode that allows other devices to connect to yours and share your internet connection, if you have one. There's a third, __ADHOC__ mode that allows devices to connect peer-to-peer with other devices the share the same network ID. Devices in ad-hoc mode will scan for other devices that it can connect to, so nearby devices will become visible and connect even as your location changes. That's a big advantage over Wi-Fi hotspots.

Scaling is still an issue for ad-hoc networks. Normally, your device can only talk to other devices that it can see directly. By allowing each device to route data for other devices it can see, they can send messages to more devices (over multiple routing hops) than they would over the ad-hoc network alone. This is exactly the problem that mesh networking solves. Moreover, this is all we need to solve the problems from the scenarios above:

* Centrally-controlled networks are not robust against government censorship or surveillance

    Mesh networks are entirely distributed and cannot be shut down by a single entity. Connections to other nodes in the mesh aren't routed over the public internet, so mass surveillance is more difficult.

* Cellular and Wi-Fi rely heavily on fixed infrastructure (access points or cell towers)

    Although mesh networks can benefit from having some fixed nodes, the network doesn't rely on any fixed infrastructure. A mesh network can form from a group of mobile devices alone.

* Mobile Wi-Fi hotspots don't scale

    Mesh routing protocols allow mesh networks to scale beyond the limitations of mobile Wi-Fi hardware. More devices can join the network by routing packets through intermediate nodes.

### Public mesh networks

Having many small mesh networks doesn't make much sense because it has the same limitations as segregated Wi-Fi networks. Things get more interesting when we consider a public mobile mesh network such that devices can connect with other nearby devices and route traffic in the mesh, or out to the public internet through internet-enabled mesh nodes. The key here is that your device may route traffic for users you don't know, and that they will do the same for you. There are opportunities to leverage other emerging technologies as well; Using cryptocurrency microtransactions to pay mesh peers to route data over a certain size, for example.

### Future work

Mesh networking isn't a perfect solution. Features like service discovery and user presence pose additional problems in a mesh network. Mesh networking protocols can have a big impact on battery life for mobile devices. And __ADHOC__ mode is not always well supported by mobile device manufacturers. While these problems are solvable, they will need some careful engineering.

I've started doing some of this work for Firefox OS. So far I have ad-hoc mode working on several supported devices including the [Flame](https://developer.mozilla.org/en-US/Firefox_OS/Developer_phone_guide/Flame), which is the current developer reference phone. I'll dive into the technical details in my next post.