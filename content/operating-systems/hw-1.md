---
title: assignment 1
date: 2023.02.24
slug: hw-1
category: Homework
---


### Various Topics from Programming Assignments


### Know how to print characters to the screen. In particular, know about VGA text mode, the text mode video memory address, and how to make characters appear with a background and foreground color (you will not have to know the color values).


### Know how to call a function written in assembly from C. Know how to write a function in assembly that accesses values passed as parameters in C. Know how to call a function written in C from assembly, and know how to pass parameters to the C function.


### Understand How and why the build process works. For example, know why you strip the binary with objcopy, and understand why segment directives are not useful for our OS code. You will ***not*** have to know the specific commands of the build process (the gcc, objcopy, ld, and nasm, mformat, etc.syntax). Be able to identify the steps of the build process.


### Know the boot procedure for your OS, from powering up, booting up in real mode (BIOS), loading the boot loader from sector 0 into memory location 0x7c00 (BIOS), loading your boot2 file (boot1, the boot loader), putting the computer into protected mode (boot1, the boot loader), to finally jumping to the first instruction in boot2 (boot1, the boot loader).