# Writing Bash Shell Scripts

- **Author**: Luke Marren
- **Recent Updates**:
  - Date: 5-27-25
  - Maintainer(s): Luke Marren

## Table of Contents

- Introduction to Bash Shell Scripting
  - What is Bash?
  - What is a Shell?
  - What is a Script?
- Strengths and Weaknesses of Shell Scripts
  - Interpreted Nature
  - (Lack of) Capability
  - Why You Should Use Shell Scripting
- Note About the RaspberryPi OS
- Basic Commands
- Variables
- Functions
- Conditionals
- Loops
- Advanced commands

## Introduction to Shell Scripting in Bash

Bash shell scripting abstracts away the complicated internals of the operating system so that we can automate simple tasks, particularly surrounding the filesystem.

This high level of abstraction, paired with its lack of complexity makes shell scripting a powerful command-line tool, if used properly.

### What is a Shell?

A shell refers to the interactive command-line interface (CLI), which users employ to communicate with the operating system (OS). The shell acts as the middleman between a user's commands (e.g., ls, cd, mkdir, ... , etc) and the operating system, which executes said commands. This buffer gives users simpler error diagnostics and a more comprehensible visual of the computer's filesystem than the operating system, which deals in bytes of incomprehensible bits.

### What is Bash?

Bash stands for the "Bourne Again Shell," which is the modernized version of the original Bourne Shell developed at Bell Labs in the 1960s. Bash, like its counterparts (e.g., Zsh, Fish, Csh, ... , etc), is the environment the operating system's command-line interface works in. As of the writing of this document, bash is the most popular implementation of the shell environment. Linux users typically defer to the Bash Shell, and MacOS just recently switched to Zsh.

### What is a Script?

A script, particularly in reference to a shell script, is a batch of commands to be executed together in a `.sh` file.

## Strengths and Weaknesses of Shell Scripts

### Interpreted Nature

Shell is considered an interpreted programming language, meaning that Shell code is interpreted line-by-line by the Shell interpreter before it is executed on your machine. As such, syntax errors are caught prior to execution, which makes development much, much faster compared to a complied language like C/C++.

### (Lack of) Capability

Shell is nowhere near as capable as other interpreted programming languages, like Python, though. Shell performs complex and data-heavy operations poorly as it lacks virtually any data structures to deal with them. Likewise, Shell is just a slow language in general; it's an interactive, interpreted CLI tool meant to carry-out very small operations on files and sometimes strings.

If you're doing math, implementing an algorithm, or in need of an array or other data structure, look to another, more powerful language like Python or C/C++. Another thing to note is that Shell has almost no external support (i.e., libraries), so building off the shell is also not a popular option.

### Why You Should Use Shell Scripting

So, the shell is an under-supported, harder-to-read, slower version of Python with a quarter of a percent of the development capability Python offers.

So why use it?

Shell scripts are excellent for small, system-level automation. They are great for dealing with filesystems, processes, and network tasks, all of which we encounter on a daily basis with our Internet-of-Things (IoT) RaspberryPi system.

On top of that, getting used to writing shell scripts translates directly to improved navigation of Unix-like (e.g., Linux) terminals, which is an invaluable tool to learn as a software developer.

## Note About the RaspberryPi OS

Before jumping into shell scripting for our RPis, it's important that you keep in mind general details about the technology you're interfacing with.

RaspberyPis run on a version of the Debian distrubtion (i.e., 'distro') of Linux aptly called "Raspbian." Since Linux is an open-source operating system, unlike its parent Unix, developers have created different distros/implementations of the system while still maintaining the overarchign compatibility, security, ... , etc that makes Linux great. Raspbian is just the Debian distro with some more tailored support for RPi users like us.

The most important thing to remember is that while writing Shell scripts, you're effectively writing a bunch of Linux-compatible commands to an interactive interpreter that communicates with Linux on how to execute your commands.
