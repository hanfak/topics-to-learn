# Input/Output Management

- manage various input/output (I/O) devices, including
  -  mouse
  - keyboards
  - touch pad
  - disk drives
  - display adapters
  - USB devices
  - Bit-mapped screen
  - LED
  - Analog-to-digital converter
  - On/off switch
  - network connections
  - audio I/O
  - printers
- An I/O system is required to take an application I/O request and send it to the physical device, then take whatever response comes back from the device and send it to the application
- I/O devices can be divided into two categories:
  - Block devices:
    - A block device is one with which the driver communicates by sending entire blocks of data.
    - For example, hard disks, USB cameras, Disk-On-Key, and so on.
  - Character Devices:
    - A character device is one with which the driver communicates by sending and receiving single characters (bytes, octets).
    - For example, serial ports, parallel ports, sounds cards, and so on.
- The CPU must have a way to pass information to and from an I/O device.
  - Special Instruction I/O
    - This uses CPU instructions that are specifically made for controlling I/O devices.
    - These instructions typically allow data to be sent to an I/O device or be read from an I/O device.
  - Memory-mapped I/O
    - When using memory-mapped I/O, the same address space is shared by memory and I/O devices.
    - The device is connected directly to certain main memory locations so that the I/O device can transfer block of data to/from the memory without going through the CPU.
    - While using memory mapped I/O, the OS allocates buffer in the memory and informs the I/O device to use that buffer to send data to the CPU.
    - The I/O device operates asynchronously with the CPU, and interrupts the CPU when finished.
    - The advantage to this method is that every instruction which can access memory can be used to manipulate an I/O device. Memory-mapped I/O is used for most high-speed I/O devices like disks and communication interfaces.
  - Direct memory access (DMA)
    - Slow devices like keyboards will generate an interruption to the main CPU after each byte is transferred. If a fast device, such as a disk, generated an interruption for each byte, the operating system would spend most of its time handling these interruptions. So a typical computer uses direct memory access (DMA) hardware to reduce this overhead.
    - Direct Memory Access (DMA) means the CPU grants the I/O module authority to read from or write to memory without involvement.
    - The DMA module itself controls the exchange of data between the main memory and the I/O device. The CPU is only involved at the beginning and end of the transfer and interrupted only after the entire block has been transferred.
    - Direct Memory Access needs special hardware called a DMA controller (DMAC) that manages the data transfers and arbitrates access to the system bus.
      - The controllers are programmed with source and destination pointers (where to read/write the data), counters to track the number of transferred bytes, and various settings. These include the I/O and memory types and the interruptions and states for the CPU cycles.
