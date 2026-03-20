
2026-03-12 00:49

Tags: [[RISC-V]]

# YT Video Script Risc-v
Script and ideas for my first youtube video explaining the design and verification proccess of my own RISC-V proccessor. The focus is learning more about processors and how code is being ran aswell as doing a cool project with a goofy goal

#### Goal
To implement a simple RISC-V proccessor that can run programs and possibly Doom. I want to show each stage of the proccessor and explain why it is needed and how it is structured.
I want beginners to be able to watch my video and follow along, the target group is people who have never handled HDL.
Some other potential goals are as follows:
- Explain HDL and how it differs from conventional coding
	- clocked vs combinatorial logic
	- maybe explain what a flip flop is
	- Explain how an adder works
- Go through a simple assembly program
- Explain Data and structural hazards, possibly in the context of where I encountered that problem
#### Intro
Some starting points to hit:
- FPGA - HDL vs Coding
- Running Doom
##### Script intro
I'm an electrical engineer who have gone through countless lectures on programming, hardware design and computer architecture. It also happens to be my job as an ASIC developer. I got curious and inspired to put my skills to test and build my own processor, diving in to each of the building blocks that enables us to enjoy this modern world filled with instagram reels and late night gaming sessions with friends. 

So! I dusted of my old university literature and started researching. The goal would be to create a RISC-V processor that would be capable of running programs, even as advanced as the all famous Doom from 19.. , this to show that it is actually a fully functional processor and not too different from the one you are watching this video on.

I want to make this video useful and understandable for everyone and maybe inspire someone to dive in to the field of hardware. It can be a very eye opening experience getting to understand this magic boxes and screens we start at 8 hours a day.

We will go through all of the 5 main building blocks of this processor and make sense of them all. We will see the difference between writing hardware and software code aswell as two fundamental building blocks of a almost all hardware, the flip-flop (chancla) - to understand the flow of information in hardware and the adder - to understand some of the computation.

We will also explain the code or instructions being executed on the processor. In the end we will see what kind of sick performance late night coding and entry level FPGAs can get you. 

I hope you will learn something and have your interest sparked for hardware design. Lets get to it!


#### AI script Intro
"I’m an electrical engineer and ASIC developer, which means I design the physical circuits that go into microchips. I’m obsessed with the low-level details, how things work, and breaking them down into their individual, digestible parts. But for me and a lot of others, a computer processor is often seen as this 'black box' that just works. I wanted to peel back those layers and show how a pile of static components actually becomes the 'brain' of a machine.

I got curious so I decided to put my skills to the test. I’m going to build my own processor from scratch. I want to dive into the actual building blocks that let us enjoy everything from Instagram reels to late-night gaming sessions with friends.

To do that, I’m using an open-source architecture called **RISC-V**. The goal? To see if this home-grown processor can pass the ultimate test for any computer: **Can it run Doom?**

In this video, we’re going to break down the five main stages or parts of a processor so they actually make sense. We’ll look at the difference between writing software and designing the hardware it runs on, and we’ll meet two fundamental pieces of almost all electronics: the **Flip-Flop** ('Chancla') which controls the flow and the **Adder** does computing.

By the end, we’ll see what kind of performance you can get out of some late-night coding and a basic FPGA board. I hope this sparks some interest in how these 'magic' boxes we stare at all day actually work. Let’s get to it!"



# References
