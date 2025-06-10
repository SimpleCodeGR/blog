---
title: Plan 9 - The Utopian OS and Lessons in Inflexible Architecture
published: 2025-06-09
draft: false
lang: en
description: Plan 9 - The Utopian OS
tags: []
---

The biggest art in software design is to know when to be flexible and when not to. I believe it's such a wonderful art, that none accomplish to master it.

A great example of lack of flexibility is Plan9. Plan9, was the successor of Unix, made from the same team, at the same place, Bell Labs.

In Unix, "everything is a file", which means that even parts of hardware from your computer are binded to a file existing under `/dev` (from "devices") and you can alter their state, read, delete from those devices, just by playing with their co-related file. I will give an example from Linux, which is a more modern successor of Unix and has more cool things, as right now, writing this, I'm able to manipulate my "Caps Lock" LED from my keyboard, without really changing to caps lock, simply by setting the value of the co-related file to 1 (for on) or 0 (for off) :

```
  echo 1 | sudo tee /sys/class/leds/input2::capslock/brightness; # Caps Lock's LED fake on
  sleep 2;
  echo 0 | sudo tee /sys/class/leds/input2::capslock/brightness; # Caps Lock's LED fake off
```
(remember to set it back to as it was !)

Now, Plan9, seeing the networked future that we live in coming, they wanted to take this concept to the next level. They wanted to take the "everything is a file" concept to the next level and each computer to be able to share those files through network.
By doing this, you could be literally be able to :
 - share your computing resources, your computing power, through network
 - share your hard disk over network
 - share your screen over network
Without using any additional software that mimics this functionality. It would had been native.
For exaple, you want to share your screen with your friend ? You wouldn't need to use a program for this, you could just share your GPU with him. Or even, think of those services nowdays that you rent a GPU online and they give you access to a remote desktop to play there games... again, you wouldn't even had to connect to a remote desktop, you could just attach the remote GPU to your computer, again, natively.

The question is, why such an innovative idea didn't became the norm ? Specially today, the posibilities could had been amazing. It could had been literally an software abstraction of Von Neumann architecture that would make you forget about Von Neumann architecture. With such innovation, we would had... flying cars at 2025 for sure, or maybe we wouldn't, but I wouldn't be thinking if my PC will be able to play GTA6 without renting... a remote, different than mine PC on the cloud... I would be able to play and have my local setup at the same time.

The reason is simple: It wasn't simple. It wasn't flexible. Going from Unix to Plan9 was like going from bike to spaceship. Every program had to be rewriten and follow a different style, far away than what we're used to. There wasn't even a compatibility layer to address this.

Even if Plan9 didn't made it, I'm sure that this next step will take place in the future of operating systems, but it will not be a revolution, as Plan9 wanted to be, but a reform. 

From Plan9, Go came out, well not as Go but as Alef and later Limbo (from successor of Plan9, Inferno) and from them Go came out. Go was made from people working on Plan9. Those languages tried to handle memory in a distributed context that you are not sure where things are not needed anymore and also they focused a lot on concurrency, again a distrubuted context thing - specially back then, without multi-core CPUs.

Also, Linux is abstracting more and more the hardware, as in the given example with my keyboard LEDs at the beggining, which makes me feel positive to believe that the time that I will be able to mount a remote graphics card as it's part of my PC, instead of logging in to a remote desktop session, is not that far away.

Our computers are getting more and more connected, so Plan9 didn't made it -because of not being simple and flexible- but it's concept did !
