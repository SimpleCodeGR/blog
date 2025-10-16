---
title: The Tragic Software Failure of Ariane Flight V88
published: 2025-06-10
customPostAuthors: ["Rantouan Achmet"]
draft: false
lang: en
description: The Tragic Software Failure of Ariane Flight V88
tags: ["Aerospace", "History"]
---

On the 4th of June 2024, we mark 28 years since the tragic failure of Ariane flight V88.

Ariane 5 rocket was designed to carry massive payloads -up to 21,000 kg- into the cosmos, following in the footsteps of its predecessor, the Ariane 4.

The Ariane 4 had its own success story, with a smaller payload capacity of 10,500 kg, thanks in part to its reliable software. This software, made up of intricate lines of code, was meant to guide the rocket flawlessly through space. When it came time for the Ariane 5 to take flight, engineers saw no reason to reinvent the wheel, so they incorporated much of the same code.

But on June 4, 1996, at the Guiana Space Centre, located on an overseas region of France in South America, during what was supposed to be a routine launch, disaster struck. Just thirty-six seconds into the flight, a tiny flaw in the code caused set off a chain reaction, halting the inertial navigation system, surrendering the rocket to intense aerodynamic forces. Consequently, the rocket veered 90 degrees off course, invoking the self-destruct mechanism leading to a massive explosion.

[https://www.openstreetmap.org/?mlat=5.239703070014162&mlon=-52.76889940050002&zoom=17#map=17/5.239703/-52.768899](https://www.openstreetmap.org/?mlat=5.239703070014162&mlon=-52.76889940050002&zoom=17#map=17/5.239703/-52.768899)

**Thankfully, no humans were harmed** as the rocket was carrying a constellation of four European Space Agency research satellites, the “Cluster“.

The failure line of code was the last line below, written in ADA :

```
L_M_BV_32 := TBD.T_ENTIER_16S((1.0 / C_M_LSB_BH) * G_M_INFO_DERIVE(T_ALG.E_BH));


if L_M_BV_32 > 32767 then
	P_M_DERIVE(T_ALG.E_BV) := 16#7FFF#;
elseif L_M_BV_32 < -32768 then
	P_M_DERIVE(T_ALG.E_BV) := 16#8000#;
else
	P_M_DERIVE(T_ALG.E_BV) := UC_16S_EN_16NS(TBD.T_ENTIER_16S(L_M_BV_32));
end if;

P_M_DERIVE(T_ALG.E_BH) := UC_16S_EN_16NS(TBD.T_ENTIER_16S((1.0 / C_M_LSB_BH) *G_M_INFO_DERIVE(T_ALG.E_BH));
```

The error was an overflow of memory limit set for the variable `T_ALG.E_BH`.

Both variables T_ALG.E_BV and T_ALG.E_BH represents the velocity of the rocket.T_ALG.E_BVdoes it for vertical velocity (thus ends in “V”) and T_ALG.E_BH for horizontal (thus ends in “H”).

Since those two variables were signed 16-bit type, that meant that they could hold from number -32768 until 32767. It’s just how things are for this type of variables. Any attempt to store a smaller or greater number would result in a memory overflow and a crash, like the ones that happen to your personal computer as well from time to time.

In the code, we can easily see that an overflow case is correctly managed for variable `T_ALG.E_BV` from the line if L_M_BV_32 > 32767 then until end if; below it. All that happens there actually is that :

 - if the value to be assigned toT_ALG.E_BVis smaller than -32768, it would take -32768 (or `16#7FFF#` in hexadecimal numbering system)
 - if the value to be assigned toT_ALG.E_BVis greater than 32767, it would take 32767 (or `16#8000#` in hexadecimal numbering system)

So simple !

All great for `T_ALG.E_BV` but for `T_ALG.E_BH` things were different : it’s completely on it’s own luck.

It was the bigger scale of Ariane 5, compared to Ariane 4, that resulted in that number stored directly on `T_ALG.E_BH` actually to reach a value greated than 32767, revealing this tiny mistake of not handling that case for this variable as well by… a huge explosion.

Following the accident, they resolved the issue quite simply removing the scandalous line and by copying & pasting the same code for `T_ALG.E_BV` to do the same thing for `T_ALG.E_BH` as well.

```
L_M_BV_32 := TBD.T_ENTIER_16S((1.0 / C_M_LSB_BH) * G_M_INFO_DERIVE(T_ALG.E_BH));

if L_M_BV_32 > 32767 then
 P_M_DERIVE(T_ALG.E_BV) := 16#7FFF#;
elseif L_M_BV_32 < -32768 then
 P_M_DERIVE(T_ALG.E_BV) := 16#8000#;
else
 P_M_DERIVE(T_ALG.E_BV) := UC_16S_EN_16NS(TBD.T_ENTIER_16S(L_M_BV_32));
end if;

L_M_BH_32 := TBD.T_ENTIER_16S((1.0 / C_M_LSB_BH) * G_M_INFO_DERIVE(T_ALG.E_BH));

if L_M_BH_32 > 32767 then
 P_M_DERIVE(T_ALG.E_BH) := 16#7FFF#;
elseif L_M_BH_32 < -32768 then
 P_M_DERIVE(T_ALG.E_BH) := 16#8000#;
else
 P_M_DERIVE(T_ALG.E_BH) := UC_16S_EN_16NS(TBD.T_ENTIER_16S(L_M_BH_32));
end if;
```

The Ariane Flight V88 is a great example of how memory safety is a field with lot of work that needs to be done.
