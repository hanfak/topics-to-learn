# Turing Machine

- original idea of a computing machine was described by Alan Turing
- theoretical model of a computer, which a lot of computers are based on
- Turing machine consists of the following four basic elements
  - **A tape**, which is divided into cells, one next to the other. Each cell contains a symbol from some finite alphabet. This tape is assumed to be infinitely long on both ends. It can be read or written
    - memory and disks
  - A **head** that can read and write symbols on the tape.
    - I/O controllers (memory bus, disk controllers, and network port)
  - A **table** of instructions that tell the machine what to do next, based on the current state of the machine and the symbols it is reading on the tape
  -  A **state register** that stores the states of the machine
    -  state + table = cpu
-  Turing machine has two assumptions, which is not real in live software:
  -  unlimited storage space
  -  completing a task regardless of the amount of time it takes
