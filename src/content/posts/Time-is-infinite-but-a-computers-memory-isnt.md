---
title: Time is infinite, but a computer’s memory isn’t
published: 2025-06-09
draft: false
lang: en
description: Time is infinite, but a computer’s memory isn’t
tags: []
---

In low-level coding, we usually have to specify the length of a variable. We have many types, including int32 and int64, which represent numbers in binary, using 32 bits or 64 bits, respectively.

The int32, of number 4 for example, looks like this:

```
 00000000 00000000 00000000 00000100
```

That’s it – 32 zeros or ones to represent a number.

There is a whole arithmetic system behind this concept, called binary arithmetic. It uses 0s and 1s to represent normal numbers. The concept is simple and by observing how binary changes with each increment, you can see how it works :
| Decimal	| Binary |
| --- | --- |
| 0	| 00000000 00000000 00000000 00000000 |
| 1	| 00000000 00000000 00000000 00000001 |
| 2	| 00000000 00000000 00000000 00000010 |
| 3	| 00000000 00000000 00000000 00000011 |
| 4	| 00000000 00000000 00000000 00000100 |
| 5	| 00000000 00000000 00000000 00000101 |
| 6	| 00000000 00000000 00000000 00000110 |

We use this system because computers can only store 0s and 1s, representing the states of electricity: charged (1) and not charged (0). A computer’s memory consists of millions of small metallic squares that are either electrically charged (1) or not (0).

In low-level programming, specifying the amount of memory needed means defining the maximum length of 0s and 1s for each number.
An int32 has 32 bits and can store values from -2147483648 to 2147483647 (if it’s a signed int, where the first bit indicates negativity). An int64 has 64 bits and can store values from -9223372036854775808 to 9223372036854775807 (again, if it’s signed).

| Type| Min (Decimal)	| Max (Decimal) |
| --- | --- | --- |
| Signed int32 | -2147483648	| 2147483647 |
| Signed int64	| -9223372036854775808	| 9223372036854775807 |

| Type	| Min (Binary)	| Max (Binary) |
| --- | --- | --- |
| Signed int32	| 10000000 00000000 00000000 00000000	| 01111111 11111111 11111111 11111111 |
| Signed int64	| 10000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000	| 01111111 11111111 11111111 11111111 11111111 11111111 11111111 11111111 |

Time in computing is often saved as a timestamp, which counts the seconds from a specific moment – usually that moment is “UNIX epoch”: 1970 Jan 1 12:00:00
| Unix Timestamp |	Comment	| Date |
| --- | --- | --- |
| 0	|	| 1970 Jan 1 1970 12:00:00 |
| 1	| | 1970 Jan 1 1970 12:00:01 |
| 2	|	| 1970 Jan 1 1970 12:00:02 |
| 86400	| an hour after “epoch”	| 1970 Jan 2 1970 12:00:00 |
| 1720080673	| seconds from “epoch” until now	| 2024 Jul 4 2024 08:11:13 |

This raises the question: What happens when we reach 2147483647, the maximum value for type signed int32, on systems that store timestamp using that type ? This will occur on 2038 Jan 19 03:14:07, which is not far from now – just 14 years from 2024. And to understand if this is important or not : do many systems store timestamps in int32? Yes, most used to, as it was the standard originating from UNIX.

Many systems have already implemented a solution to this issue.
 - Linux, as a successor to Unix, used to store timestamps in 32-bit integers for 32-bit systems. With version 5.6 (2020), it switched to 64-bit. Still, individual applications, protocols, and file formats must be updated as well. [1]
 - Windows, in the 32-bit version of gmtime in the C runtime libraries, stores timestamps in 32-bit integers. Many individual applications have already addressed this issue, like Oracle’s Access Manager from version 10.1.4.3. [2]

However, some systems have not addressed this issue. 
 - Many databases still store timestamps as int32 by default. 
 - SAP’s S/4HANA, used for business management and the successor of the world’s most used ERP (SAP’s ERP), supports only “finish” dates up to 2048 Jan 19. ( The situation is similar to the previously mentioned systems, except the timestamp starts from 1980 Jan 1, instead of the UNIX epoch which is 1970 Jan 1 12:00:00 )

A “panacea“ to this issue is to store timestamps as 64-bit integers in any new system design, avoiding future migrations and fixes. Storing in 64-bit, as Arnd Bergmann suggested for Linux [1], allows for a maximum timestamp of 9223372036854775807, or : 292277026596 April 12 15:30:07. This is 292 billion years from now [3], far beyond our immediate concerns.
| Type |	Min (Date)	| Max (Date) |
| --- | --- | --- |
| Signed int32	| 1901 Dec 13 20:45:52	| 2038 Jan 19 03:14:07 |
| Signed int64	| Before universe ! |	292277026596 Apr 12 15:30:07 |

However, this solution is not simple, as storing values with double the length is not always optimal. For a large database, this would result in significant and impractical memory usage.

This journey through a man-made abstraction of time – from infinity to plain 0s and 1s within a fixed size – leads us to a question : Does storing all timestamps as int64 justify the cost, or are there better scenarios for the future?
