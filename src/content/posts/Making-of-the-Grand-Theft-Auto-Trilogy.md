---
title: Making of the Grand Theft Auto Trilogy
published: 2025-06-03
customPostAuthors: ["Rantouan Achmet"]
draft: false
lang: en
description: Making of the Grand Theft Auto Trilogy
tags: []
---

I was lucky enough to read all the posts of Obbe Vermeij at the blog "Insider Rockstar North", before he had to take it down. 

Obbe Vermeij was a developer working at Rockstar North game studio, during the GTA Trilogy era (III, Vice City, San Andreas...).

For computer games, the GTA Trilogy is a reference point, as it was one of the first game series offering such an open-world experience, that you could travel around and do whatever, without limitations.

Obbe seems to have been one of the key people who contributed to this freedom with his mindset, even while there were considerations of minimizing this freedom to make the game less heavy.


> Gta1 had 3 cities and we wanted to do the same. 
>
> There was one particular meeting that I still have nightmares about. In R*N we would usually make the big game decisions with 5 people. We had a meeting where 3 people wanted the cities to be on different maps. This would save memory as the models for the skylines of the cities wouldn't need to be in memory at the same time. Gta1 had 3 cities on different maps. The player would take planes/buses/trains to travel between maps.
>
> I wanted the cities to be on the same map as it is important to be able to drive between cities. Even if this meant we'd have to find some memory elsewhere. The 5th guy wasn't there that day. I wasn't able to convince the others. It was super frustrating as it seemed we were about to make a massive mistake.
>
> The following day we had another meeting. The 5th guy agreed with me and was much more persuasive than me. He talked them round and the cities ended up on the same map. Disaster averted.
Obbe Vermeij
>
> The 3 cities with the country side in between, almost killed the map artists. gtaIII and Vice had maps of 4x4km and even then there was loads of water. The SA map was 6x6 and densily packed.
>
> ~ Obbe Vermeij

It was precisely this freedom that everyone, including myself, relished in the game. 

Developers and game artists found inspiration in this as well.

> We took the code from Vice City as the foundation for SA. Many things were improved but no structural improvements were needed.
>
> R*NY organized another 'research' trip. They hired a bunch of town cars and we drove between Vegas, LA and San Fransisco. The artists took pictures. It was loads of fun.
>
> ~ Obbe Vermeij

> The artists gave me a texture for the moon in III. I placed the moon in the sky, made sure it was visible at night and that it was a reasonable size.
>
> A few days later 4 artists were at my desk asking me to change the size of the moon.
>
> "No problem" I said.
>
> It turned out they couldn't decide what the size of the moon should be. 2 of them wanted it smaller to be more realistic. The other 2 wanted it larger to be more cinematic.
>
> This went on a bit and I suggested to make the size of the moon changeable in the game. This way they could decide in their own time and let me know the conclusion. Since I was working on the sniper rifle, I made it so that the moon toggled through 3 sizes (small, medium, large) as the player sniped it.
> 
> The artists never got back to me so I just left it in. It was still there in SA.
> 
> ~ Obbe Vermeij

Everything you see in a videogame, must be loaded. From the hard drive, to the RAM / graphics card's VRAM and then to your screen. And if the game is huge, it can't be all loaded at once. There needs to be a mechanism that knows when to load something and when to unload it, according to your location in the map. As you move around, specially to such an open-world and huge game, this mechanism must do this job and it must done it well.

GTA Trilogy was ahead of it's time, and to make this streaming mechanism work well, they did lot of tricks.

> For example, from GTA III until GTA San Andreas, the game could manage up to seven different car models around the player simultaneously due to the lack of RAM memory in that era. This meant that during intense situations, like when the police were chasing you and the game had to load police cars and helicopters, the number of pedestrian cars loaded decreased, often to just one or two.
>
> For instance; if the player has a 6 star wanted level, the game would load the fbi car and the helicopter.
>
> There may still be police cars and swat vans around from when the player had a lower wanted level.
>
> If there are any injured pedestrians, the game had to load the ambulance.
>
> Before you know it, the game only has 1 or 2 models left for regular civilian cars.
>
> Even without the wanted level, the game was often forced to load certain car models.
>
> ~ Obbe Vermeij

As a cherry on top, all those things had to be loaded using a slow CD-ROM, as this was the storage medium in many consoles at the time. And CDs are not only slow, but they have another problem as well : if the thing you want to load, exists on a point before the current point the CD is on the CD reader, you need to wait for the CD to re-spin. Now, imagine doing this for many things. To address this, they grouped related data together.

> They meticulously arranged data on the CD, ensuring that elements closely linked in the 3D game world were also physically close on the CD for simultaneous reading, and
in problematic areas, they fine-tuned details, such as creating inclines or increasing air resistance, to slow down vehicle movement subtly (without the player realizing the reasons behind it).
>
> ~ Obbe Vermeij

> The hardest technical challenge to solve during the development of gta3 was the streaming. Streaming involves loading and un-loading models as the player moves over the map. The streaming was coded by Adam Fowler.
> 
> When we started out with gta3 the hope was that the entire map would fit in memory. The map would simply be loaded at the start of the game.
> 
> Memory was limited on the PS2 and the artists were forced to reduce the texture sizes and to re-use textures everywhere. This resulted in the city looking bland. They eventually asked Adam whether he could develop a streaming system.
> 
> The idea of streaming is to load the map only around the player. As the player moves, the models for nearby models are loaded from the CD into memory and buildings that are now far away are removed.
> 
> Streaming is also used for vehicle models, pedestrian models, sound effects, music and scripts but the map posed the greatest difficulty as this involved more data than everything else combined.
> 
> Unfortunately the CD was quite slow in loading the models. The loading speed depends on the location of the models on the CD (the track). Models that are close together are loaded quickly but models that are far away are slow. (This is because the CD needs to accelerate/decelerate as the head moves to a different track). This is causing a lot of the sounds coming from the CD drive when playing gta.
> 
> Adam spent a lot of time ingenuously moving the models around on the CD. The idea was to place models close together in the CD if they were also close together in the world.
> 
> Even after all these optimizations, streaming was still not fast enough. You can literally think of it as a race between the player travelling and the streaming loading the models. At times the player would be too fast and the world just wasn't there yet. These problems seemed to get worse with older CDs.
> 
> If we couldn't speed the streaming up any further, we had no option but to slow the player down.
> 
> In Portland (first island in gta3) there used to be a big strip running all along the island. This was a worst case scenario. The player could go fast and there were loads of buildings to load. The streaming couldn't cope here. Eventually the artists had to change the layout and basically put a building on top of the strip. The player had to go around which would slow him down allowing the streaming to catch up.
> 
> Over time we identified other areas where the streaming was not coping and we would set up zones here. Within these zones we increased the drag (air resistance) on the vehicles a little. Maybe 5 or 10%. It was hardly noticeable but it helped.
> 
> ~ Obbe Vermeij

Cheats were heavily optimized as well. To make it hard to find the cheats, instead of storing them as strings (which would result to be easy to find by searching in the binary), they used a number for each of them. If the sum of the pressed keys, matched the number of the cheat, the cheat was activated.

> The cheats in the trilogy were activated by simply typing a sequence of characters.
> 
> On PC the sequence would be something like
> 
> ILOVESCOTLAND to make it rain or
> 
> GUNSGUNSGUNS to give the player loads of weapons.
> 
> The game remembers the last 20 or so keypresses and every time a new key is pressed, these keypresses are compared with the cheats. If there is a match, the cheat will activate.
> 
> The straightforward way of doing this would be to compare the string "ILOVESCOTLAND" with the string of keypresses. This approach would mean that the strings for the cheats would be in memory as readable text. Any hacker could easily find the cheats and they would all be discovered on the day of release.
> 
> This is why I used 'hash codes' to store the cheats. A hash code is a number that is calculated from a string. As an example; a simple hash algorithm could add up the ASCII values of each character of the string.
> 
> The hash code for ILOVESCOTLAND would be 983.
> 
> For GUNSGUNSGUNS it would be 951.
> 
> This is just an example. The actual Hash algorithm used is more complicated.
> 
> The game would also calculate the Hash code for the last 20 or so keypresses and compare the numbers.
> 
> The good news is that it is harder to hack the cheat because the code only stores the number (ie 983) and not the full string (ILOVESCOTLAND). This part worked because the cheats were not hacked. (They were eventually discovered by people trying random input until a cheat happened)
> 
> The bad news is that different strings can result in the same hash code.
> 
> This is why initially when cheats were discovered people found random strings (ie HDLMAAXOPK) and not the string I had set up (ie ILOVESCOTLAND)
> 
> This also meant the cheats triggered more often than I had planned. This caused cheats to sometimes happen unintentionally. This has actually happened during peoples' speed runs. These speed runs had to be aborted as the rules are clear. No cheats.
> 
> ~ Obbe Vermeij

The weather, on the other hand, wasnt optimized at all. It was just a fixed look-up table, that according to time, there was a weather value.

> Every in-game hour, the next weather type is picked from a table. The table is 40 (or maybe 34, can't quite remember) entries long. If it is raining now, it will be raining again in 40 in-game hours.
> 
> The visual effects for the weather type will transition over the hour.
> 
> For instance:
> 
> At 2:00 it would be 100% sunny.
> 
> At 2:15 it would be 75% sunny and 25% overcast
> 
> At 2:30 it would be 50/50
> 
> etc
> 
> The table frequently has the same weather type for several hours so the weather isn't always in-flux.
> 
> There are script commands to override the weather type. This allows the level designers to force the weather type for a particular mission or cut-scene.
>
> ~ Obbe Vermeij

It's nice reading how all those things were made ! 

I hope Obbe will come up with many more details.
