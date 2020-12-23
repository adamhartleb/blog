---
title: "Computing Concepts Part 1"
date: 2020-12-23
draft: false
---

### Defining a Computer

A computer is any digital device such as a smartphone, desktop PC, smart watch, game console that can be programmed to carry out a set of instructions. Notice that the definition contained the word _digital_. Undoubtedly, you've probably heard some devices described as digital and others as analog. Consider a scale that measures the weight of an object. A scale contains a needle that points to a number and this number is not the weight of the object, it's a number that represents the weight. The scales works as an _analogy_ for the weight of the object which is why we call it an analog device. Additionally, the needle only approximates the weight of the object, it's limited by the physical constraints of the device. However, sometimes analog simply mean non-digital. When speaking of an analog signal, it refers to a signal that varies continuously rather than having discrete values. Analog representations of data are hard for computers to work with because they vary wildly in form that it's impractical to create a common device to understand them all, plus analog data is difficult to measure precisely. Instead, computers use a digital approach which represents data as a set of discrete values (typically 0 or 1).

From the photo you took on your phone, the music you're listening to, or the text you're currently reading, all of this data can be represented digitally as a series of 1s and 0s. The symbols 1 and 0 are just that -- symbols that represent some physical difference. For example, data stored on a CD ROM is represented as a bump (1) or flat space (0). 

### Number Systems

Now that we've established computers are digital devices that operate on 1s and 0s, a natural question arises: why only 1 or 0? Why do computers not use the decimal system that humans are familiar with? To understand that, we must first review number systems.

We typically write numbers in positional notation. When I write the number 378, we know that the position of each number means something. The "3" represents the hundreds place, the "7" the tens place and the "8" the ones place. Another way of writing it is:

```
(3 * 100) + (7 * 10) + (8 * 1) 
``` 

Why is the rightmost number the ones place though? The decimal system is a base 10 system and therefore each place is a power of 10. We can re-write the above using powers of 10 like so:

```
(3 * 10^2) + (7 * 10^1) + (8 * 10^0)
```

Using this base system, we can create a number system using any positive number provided we have enough symbols to represent each number. A number system containing only two symbols (1 and 0) is a binary system. The number 101 in binary means something entirely different than 101 in decimal. Each position in a binary number is a power of 2. Following the above example, we can re-write 101 as:

```
(1 * 2^2) + (0 * 2^1) + (1 * 2^0)
```

Adding the numbers together yields the number 5 in decimal. Since 101 can mean different things depending on the number system, we prefix binary numbers with "0b". 

### Bits and Bytes

Each number in a decimal number is referred to as a digit. Similarly, in binary, each number is referred to as a bit. Since a single bit can only convey a limited amount of information, we tend to working with multiple bits together. A group of 8 bits together is referred to as a byte. 