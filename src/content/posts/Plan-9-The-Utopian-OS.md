---
title: Plan 9 - The Utopian OS
published: 2025-06-09
draft: false
lang: en
description: Plan 9 - The Utopian OS
tags: []
---

The biggest art in software design is to know when to be flexible and when not to.

In operating systems, many that have went down the "Plan9" rabbit hole, are wondering why Plan9 failed.

Plan9 was the successor of Unix, made from the same people that made Unix. The core concept, was to take the Unix's "everything is a file" and take it to the next level, in a way that computers could share everything accross network, even hardware (since even hardware "is a file").

This was very innovative. Many programs we use today, wouldnt be needed. Take for example screen sharing programs. You wouldn't need them, as you could just share the graphics card's "file" over network.



---

Many enthusiasts in OS development often wonder why “Plan9” from Bell Labs (not “Plan 9 from Outer Space“, the movie) met its demise despite its promising features.

The successor of Unix, Plan9 and its later iteration, Inferno, were conceived as evolutionary steps – some might label Plan9 as “Unix 2.0” and Inferno as “Unix 3.0”. Plan9, departing from Unix conventions, presented a revolutionary concept by treating “everything as a file“. In contrast to Unix and Linux, where this idea remains somewhat aspirational, Plan9 took it quite literally.

For instance , even the windowing system, was considered a file. This approach allowed someone using “Rio” Plan9’s second window manager following its first “8½” window manager, with the correct permissions, to observe and manage a screen from the network by simply mounting the folder containing the windowing system. This process eliminated the need for tools like the “X forwarding” in the Linux world… (or modern remote desktop software on Windows).

In Plan9’s “everything is a file” philosophy, many tasks that typically demand dedicated tools in the Unix (thus Linux) realm were seamlessly integrated by design logic.

However, this innovation came at the cost of flexibility. While Unix (thus Linux), often requires specialized tools for various functions, Plan9 opted for a one-size-fits-all approach. In Unix (thus Linux), tools are tailored for specific tasks, each with its unique functionality. Plan9, on the other hand, implemented a default logic for everything, expecting the entire world to conform to its methodology rather than adapting to diverse scenarios. Despite its superiority in certain aspects, this lack of flexibility proved to be a stumbling block. The world, enamored with the adaptable Unix (thus Linux) and its… myriad tools, never fully embraced the less-flexible, albeit innovative, Plan9.

