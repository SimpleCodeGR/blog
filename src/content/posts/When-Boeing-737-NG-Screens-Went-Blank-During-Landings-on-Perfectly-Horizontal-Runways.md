---
title: When Boeing 737-NG Screens Went Blank During Landings on Perfectly Horizontal Runways
published: 2025-06-07
customPostAuthors: ["Rantouan Achmet"]
draft: false
lang: en
description: When Boeing 737-NG Screens Went Blank During Landings on Perfectly Horizontal Runways
tags: []
---

The pilots of the new Boeing 737-NG, around 2019-2020, encountered a particularly vexing issue: all six display units would go blank during landings at certain airports, including:

 - La Mina, La Guajira, Colombia
 - Barrow, Alaska, USA
 - Pine Bluffs, Wyoming, USA
 - Wayne County, Ohio, USA
 - Chippewa County, Michigan, USA
 - Cavern City, New Mexico, USA
 - Cheddi Jagan, Georgetown, Guyana

Since the Boeing codebase is closed-source, the exact cause of the issue remains unknown. We only know the nature of the bug, the timeframe in which it occurred, and that it has since been resolved. Thus, we can only speculate about the details.

…So, let our imaginations take flight !…

First of all, let’s consider the airports themselves. These locations form our sample space.

If we examine the airports on maps, we will find a common factor: each of these airports has at least one perfectly horizontal runway!

[La Mina, La Guajira, Colombia](https://www.openstreetmap.org/?ref=blog.simplecode.gr#map=16/11.2342/-72.4913)

[Barrow, Alaska, USA](https://www.openstreetmap.org/?ref=blog.simplecode.gr#map=14/71.2856/-156.7695)

[Pine Bluffs, Wyoming, USA](https://www.openstreetmap.org/?ref=blog.simplecode.gr#map=16/41.1507/-104.1349)

[Wayne County, Ohio, USA](https://www.openstreetmap.org/?ref=blog.simplecode.gr#map=16/40.8744/-81.8877)

[Chippewa County, Michigan, USA](https://www.openstreetmap.org/?ref=blog.simplecode.gr#map=16/46.2548/-84.4747)

[Cavern City, New Mexico, USA](https://www.openstreetmap.org/?ref=blog.simplecode.gr#map=16/32.3422/-104.2601)
(a horizontal runway is located in the middle of the map)

[Cheddi Jagan, Georgetown, Guyana](https://www.openstreetmap.org/?ref=blog.simplecode.gr#map=16/6.4988/-58.2571)
(a horizontal runway is located in the middle of the map)

If all the aforementioned airports have a runway that is perfectly horizontal—meaning it forms a 270 or 90-degree angle, depending on the approach direction—then we can hypothesize about the issue by identifying mathematical functions :

```
( f ) where ( f(x) = 0 ) for ( x = 270° ) or ( x = 90° )
```

One such function is the very simple : `f(x) = 1 / cos(x)`

That, because :
```
cos(270°) = 0

cos(90°) = 0
```

So, we end up with :
```
f(270°) = 1 / cos(270°) = 1/0

f(90°) = 1 / cos(90°) = 1/0
```

And division by 0 is impossible.

In this scenario, the Boeing 737-NG’s software may have crashed, causing the screens to turn off on these perfectly horizontal runways. However, we don’t truly know the reason, and the above is merely one of many possible assumptions we can make using our imagination and the given context.

Below is the U.S.A. Federal Aviation Administration’s record of the bug:

The FAA received reports earlier this year of three incidents of display electronic unit (DEU) software errors on Model 737 NG airplanes flying into runway PABR in Barrow, Alaska. All six display units (DUs) blanked with a selected instrument approach to a runway with a 270-degree true heading, and all six DUs stayed blank until a different runway was selected [(source)](https://www.federalregister.gov/documents/2019/12/27/2019-27966/airworthiness-directives-the-boeing-company-airplanes?ref=blog.simplecode.gr).
