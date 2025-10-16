---
title: When is a program good ? Reverse engineering HOU’s compiler
published: 2025-06-10
customPostAuthors: ["Rantouan Achmet"]
draft: false
lang: en
description: When is a program good ? Reverse engineering HOU’s compiler
tags: []
---

> UPDATE: The Linux port of the compiler now works even with printing Greek characters. Everything works now, basically.
> 
> [https://github.com/rept0id/hou-compiler-linux/](https://github.com/rept0id/hou-compiler-linux/)

At the university I’m attending, Hellenic Open University, they have developed, years ago, a custom programming language and a custom compiler for it. The language is ok, feels a bit like Pascal and the commands are all in Greek. For example:

```plaintext
ΑΛΓΟΡΙΘΜΟΣ ΔΟΚΙΜΗ
	ΔΕΔΟΜΕΝΑ x:INTEGER;
ΑΡΧΗ
	ΤΥΠΩΣΕ ("PLEASE ENTER A NUMBER: ", EOLN);
	ΔΙΑΒΑΣΕ (x);
	ΤΥΠΩΣΕ ("YOU GAVE: ", x, EOLN)
ΤΕΛΟΣ
```

The compiler on the other hand… is one of the worst compilers I’ve used ever. It’s very buggy and it’s also having millions of encoding problems which originate from the fact that it expects files to be in Windows-1253 encoding while most editors nowadays use UTF-8. It’s a compiler you can use, but it doesn’t fit its purpose. So it’s bad.

What I mean by this is that there is a way to use this compiler: use Notepad++ and constantly check if your encoding is Windows-1253; workaround the compiler’s bugs by writing your code with the same logic but a bit differently. All this makes coding in that language and using this compiler harder than coding in C, which is touted later and is considered harder… oh sweet summer child, if you only knew (!!! 😂 !!!).

But the purpose of this compiler was to be introducing and easy, so this compiler has failed its purpose for good. And it’s not only me who will say this. Aristotle argued that something is good when it fulfills its “τέλος” (purpose or function), so there are good chances Aristotle would consider this compiler “bad”.

As a cherry on top, this compiler doesn’t work on Linux. So it’s trash.

---

It was clear that something needed to be done with this compiler.

I managed to get this compiler to work on Linux after lots of tweaking with the “wine” compatibility tool and because I didn’t want anyone else to go through all this, I made a public repository with a ready solution. You can find everything here:
[https://github.com/rept0id/hou-compiler-linux/](https://github.com/rept0id/hou-compiler-linux/)

This “wine” solution makes using this compiler on Linux not only possible but actually better than it is on other platforms. This is because before it runs the compiler and the produced executable through wine, it also encodes the provided file from UTF-8 to Windows-1253.

This way, you write with a sane person’s tools, you know, the average editor of the simple layman out there that uses UTF-8, and then another file with the same content but Windows-1253 gets created and provided to the compiler. But you don’t care about the other file as it’s just a middle step. You write UTF-8.
Now you can focus on your code instead of the encodings.

---

This solution mentioned above is “good” (by Aristotle) but it’s not “perfect” (by me, even though Aristotle’s opinion matters more). Because something with this compiler and wine bugs, if you try to print Greek characters through your program it will display them wrong (as a workaround, use Greek with Latin characters, Greeklish, or just English).

Such a thing is very annoying for a compiler and whole concept meant to work with Greek. This actually still makes the program “not good” by Aristotle. This must be fixed as well, else the solution is not perfect. I believe there are 2 ways to fix this: one is to keep fuck-around-find-out with Wine and the second is to reverse engineer this compiler totally and make a better one. Guess which one I find more fun!

> UPDATE: The Linux port of the compiler now works even with printing Greek characters. Everything works now, basically.

---

First step into reverse engineering was to throw this compiler into a classic .NET reverse engineering tool, like .NET Reflector and the newer DotPeek, because only those ones I knew from a friend.

Actually, .NET is the best case of reverse engineering a program because the code that you write in C#, VB, F# or whatever, gets transposed into bytecode for “Common Language Runtime” which is considered easier to reverse engineer than raw binary machine code.

Those tools, if the code is not “obfuscated” against them, will give you a very good result. This bytecode thing makes me consider all those languages to be in the same basket as Java; even though they don’t claim that they run inside a VM, they aaalmost do something that could be labeled as similar.

Turns out this compiler is not a .NET program and I couldn’t get something out of using those tools.

Next step was to guess better what this program was made with. I ran

```bash
strings ./pli10.exe
```

in a Linux terminal and saw a little bit the result. I saw many “GCC” (filtered with `strings ./pli10.exe | grep "GCC"`), and made a conclusion that this may be a C/C++ program, since GCC is a C compiler.

I can’t be 100% sure as this compiler uses tdm-gcc to generate the machine code, so maybe it’s written in something different than C/C++ and it just calls the GCC compiler.

So I had to do what any programmer that likes math would have done and say the poem:
“let’s assume this program is C/C++” and continue based on this.

I didn’t know any good C/C++ disassembler so ChatGPT and Google were my friends and I found that actually there are out there 2 very good ones:

* Ghidra, made by NSA
* Interactive Disassembler (IDA), made by Ilfak Guilfanov

I managed to get Ghidra and disassemble the compiler back to code. But still, I wasn’t able yet to find many things. Not yet.

By the way, Ghidra can disassemble other languages too like Go and Rust as far as I’ve read.

---

Still, the journey doesn’t end here, as I’ve already found a line that is very interesting:

```c
system("chcp 1253 > nul");
```

Maybe this program could work much better if this legacy Windows-1253 encoding wasn’t enforced.

---

> UPDATE: The Linux port of the compiler now works even with printing Greek characters. Everything works now, basically.
> 
> [https://github.com/rept0id/hou-compiler-linux/](https://github.com/rept0id/hou-compiler-linux/)
