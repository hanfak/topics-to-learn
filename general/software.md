# Software

- Software Is an Abstraction, Built Using Reasoning
- Computers do not have their own intelligence and they do not speak our languages.
- They can only understand electronic signals that have two states: on and off. - These electronic signals are represented in binary numbers of 0 and 1. A mixed string of 0’s and 1’s can constitute instructions or commands that instruct computers what to do
- comprised of machine instructions that are processed by the CPUs of physical machines and/or virtual machines

### Links

- https://www.javacodegeeks.com/2018/09/what-is-software.html

## Programming

- It is the act of creating instructions, the software
- Programming has always been about analysing a problem and codifying it so unambiguously that it can be executed by a machine.
  - Thus trying to turn natural language into machine instructions was doomed to fail, it is too ambigious, not the syntax

## Assembly Language

- the symbolic version of the computer instructions that is a step closer to our language.
- An assembly statement is translated into a mixed string of 0’s and 1’s by an assembler whose job is to translate instructions from symbolic version to binary version.
  - So it can be understood by the hardware
- assembly language is still not flexible enough for constructing complicated programs, as it requires programmers to write one line for every instruction that a computer can understand, forcing programmers to think like machines

## Compilers

- an assembler is a software program, that was written to translate assembly language into binary instructions that can be read by the hardware
- we can write another program to translate programs written in some high-level programming languages (more human like and think as a human) into a program in the format of assembly language
  - This is a compiler
- Using higher level programming language allowed more natural language expressed in English words and algebraic notation.
- It allowed the creating of programs for dedicated purposes such as I/O (input/output) libraries and common system management software, which is called operating system
- Compilers were designed and implemented for yielding the optimal performance for the programs they compile by targeting specific underlying computer hardware.

## Higher level programming languages

- What the majority of software is written in
- Have different paradigms
  - functional
  - procedural
  - object oriented
  - logical
  - or allows for all of them (multi paradigm)
- Different languages have different characteristics/features which make them good for use in creating different software
- Programs written in these languages are enabled to call libraries for common functions such as I/O
  - They are made executable by being compiled and then assembled into machine code
  - Their executable form is called binaries, which are run with the coordination of operating systems
- Majority of languages, along with libraries can be used to create a lot of software

## Binaries

- Software created in a language is transformed into an executable program called a binary (artifact/jar/war)
  - This allows users to run and use the software developed on their computers
- procedure of developing software binaries
  - Coding the logic of a program in a high-level programming language
  - Compiling the developed program with linking to libraries to be called
  - Assembling the developed program into machine code
  - Running the developed program on specific computer hardware with the assistance of a specific operating system

## Software stack

- This is for common languages like C
- From top to bottom dependencies
  - your programs
  - libraries
  - compilers
  - assembler
  - operating system
  - hardware
- Performance depends on all these features not just the logic in your programs

## JVM and virtualisation

- JVM was designed to bridge the gaps among different operating systems by abstracting various program run-time environments
- The programs written in Java (jvm languages) can be run on different platforms (operating systems) without being modified or recompiled
- all programs written in Java are a universal abstraction in the format of byte code
-  virtual systems (an extension of jvm) that can be configured with virtualization software such as VMWare
  -  allows you to run multiple applications on multiple operating systems on a single physical system
-  Software stack
  - your programs
  - libraries
  - compilers
  - assembler
  - JVM
  - one or more virtual machines
  - operating system or virtual server
  - hardware
- Anothe level of improvement in virtualisation, came with containerisation like Docker

## Types

- Software is built in a layered approach
- Three main layers
  - System: The layer that is closest to the hardware
  - Middleware: the layer between the two, connecting them
  - Application: layer that is closest to the user

### System Software

- is anything that has to be part of hardware in order for the entire system to function as a complete computing platform
- provides a platform or run-time environment for application software to run on computers
- Three types
  - BIOS (Basic Input/Output System)
    - firmware
    - It is run when a PC computer is powered on, booting up
    - primary function of the BIOS is to set up the stage for other software programs stored on hard drives, floppies, and CDs to load, execute, and assume control of the PC
    - At bootup, can look at the config for BIOS, and set them
  - Device Drivers
    - interfaces in the form of software that control how various hardware components interact with the operating system.
    -  a layer between a hardware device and an operating system
    -  It translates commands written in high-level programming languages into the machine language that the hardware devices can understand
    -  Adding new hardwar, ie printer, it needs a way for the OS to talk to it, this is down via piece of software (driver) that is already bundled with OS or needs to be added (manually or on connection with hardware it adds it)
  -  Operating System (OS)
    -  An operating system is software that can translate user commands into machine instructions for the computer hardware to execute
    -  coordinates the use of hardware resources by performing basic tasks such as
      -  controlling and allocating memory
      -  scheduling system requests
      -  controlling input and output devices
      -  facilitating networkin
      -  managing disk storage usage through a file system.

### Application Software

- class of software that can help individuals or business organizations do something more efficiently by employing the capabilities of a computer or networked computers
- These can also act as middleware software at the same time or be seen as middleware software, all depends on the architecture of the system
- Types
  - Business Software
    - application software that addresses the needs of business organizations for more efficient business processes and management
    - any type of software used in an enterprise that helps facilitate accessing and managing enterprise data belongs to the category of business software.
    - For example,
      - ERP (Enterprise Resource Planning) is one of the typical types of business software, which has modules such as CRM (Customer Relation Management), HR (Human Resources), SC (Supply Chain), Financials, Manufacturing, etc
      - ITSM (IT Service Management) is another typical type of business software, which includes components such as HD (Help Desk), CM (Change Management), PM (Problem Management), and IM (Incident Management).
  - Media and Entertainment Software.
    - ddresses the needs of individuals or organizations for consuming digital media such as video gaming, video conferencing, and streaming media
  - Product Engineering Software
    - addresses the needs of professional individuals for enhancing their productivity and efficiency
    - ie CAD (Computer Aided Design), CAE (Computer Aided Engineering), and IDE (Integrated Development Environment).
  - Internal Applications
    - developed for internal use only. They are also called in-house applications.
  - Single-User Applications
    - intended for individual users such as Microsoft Office Suite, Turbo Tax for filing tax returns, and any other applications you can run on a PC or website (google docs)
  - Web Applications
    - This class of applications is made available through the Internet.
    - Users employ a Web browser (on different hardware platforms) to access such applications.
    - All online search portals such as Google, Yahoo, and MSN belong to this category.
    - Pure play online retailers such as Amazon.com and eBay, as well as the Web shopping sites from traditional retailers,
  - Database-Centric Applications
    - applications is characterized by its strong dependencies on databases.
    - Most of the business software applications are typical database-centric applications

### Middleware software

- Any application that connects it to another application
- Messaging software
  - ie activemq, kafka, ibm mq
- Application server
  - ie IBM’s WebSphere, BEA’s WebLogic, and Microsoft’s .NET
- Specialized infrastructure server software such as email servers and network and security management servers
- Platforms/PaaS
  - Windows Azure, Heroku,
