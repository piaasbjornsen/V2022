
# Computers as they are no more
## von Neumann-style computer
* 3 major components
  * CPU 
    * Processor 
    * Address memory locations and fetch instructions/data from memory
    * Send request to io-devices and read or write data
    * 
  * (Unified) memory
    * Contains instructions and data 
  * Device 
    * I/O
    * Can interrupt 
      * Enable us to waste less computer 
    * DMA (Direct memory access) 
      * Can write directly to memory, and not go through the CPU
# Introducing a memory hierarchy
* Additional types of memory into our computer, called caches
* Idea: introduce caches 
  * Small, but fast intermediate levels of memory
  * Hides the slow speed of our large main memory 
* Caches can only hold a partial copy of the whole memory
  * Unified cached (hold instruction and data) vs. separate caches (hold instruction or data, and are faster)
  * expensive to manufacture (-> small)
  * Later: Introduction of multiple levels of cache (L1, L2, ... )
    * Each one bigger, but slower than the previous one (hierarchy)
* Caches work efficiently due to locality principles (2):
  * *Temporal locality*: a program accessing some part of memory is likely to access the same memory soon thereafter
  * *Spatial locality*: a program accessing some part of memory is likely to access nearby memory next. 
* The further from the CPU:
  * Increasing size
  * Decreasing speed
  1. Regs
  2. L1 Cache
  3. L2 Cache
  4. RAM
  5. DIsk

## Memory impact: non-functional properties 
* Memory has a large influence on non-functional properties of a system
  * Average, best and worst case performance, throughput and latencies 
  * Power and energy consumption 
  * Realiabaility and security
* Non-functional properties depend on many parameters of memory, e.g. 
  * Cache architecture
  * Memory type
  * Alignment and aliasing of data

## When one processor is not enough 
* Moore's law (observation) (4):
  * Observation that the number of transistors in a dense integrated circuit (IC) doubles about every two year
  * Accordingly, increase in CPU speed due to smaller semiconductors structures 
* This development is hitting physical limitations
  * CPU frequencies "stuck" at 3GHz
  * Energy consumption is additional limiting factor
* Even though we cannot get a better frequency out if our CPU chips with more transistors we can use the transistors for something else

## When one processor is not enough 
* What can we do with all these transistors? 
  * Bigger caches - energy hungry and prone to faults
    * When this was used, users complained that the computer was crashing 
    * These caches are memory cells consisting of a number of transistors, and they are very suspicious to cosmic 
    rays and electromagnetic interferences, so when this occurs it's very likely that it can flip a bit in your cache,
    or crash your computer.
  * Put more processors on a chip
    * Earlier high-end systems already used multiple separate processor chips
    * But we can put the processors on the chip, we could enable faster communication between the processors 
    * So the new trend, in stead off increasing frequencies, where we hit a limit, we increase the number of processors 
* Old as well as new problems:
  * Memory throughput now has ta satisfy demands of n processors
  * Software now has to support execution on multiple processors 
  * Caches need to be coherent, so they hold the same copies of main memory data 

## More processors, more memories
* Memory throughput now has to satisfy demands of n procressors
  * Provide each processor with its own main memory
  * NUMA - Non unified memory architecture
* And new problems show up
  * How to access data in another CPU's memory?
  * Who decides which CPU is allowed to use the bus?
  * Is common bus still efficient?

## On-chip communication
* Use high-speed networks instead of conventional buses
  * Using ideas from computer networking 
  * On-chip network can achieve high throughput and low latencies

## Heterogeneous sysmtems: GPGPUs
* In modern computers, not only CPUs can execute code
* GPGPUs (general purpose graphics processing units)
  * Massively parallel processors for typical parallel tasks 
  * Used ofr: 3D graphics, signal processing, machine learning, bitcoin mining...
  * Few features for protection, security...
* Traditionally, GPUs were accessible to a single program only (in Unix: "X window server") for drawing 
  * Other programs had to ask the X server for services
* In modern systems, multiple programs want direct access to the GPGPU
  * How can the OS multiplex the GPGPU safely and securely?

## Security 
* ...there's another important non-functional property!
* Multiple programs running simultaneously
  * e.g. online banking application and video player
* How can we avoid the video player accessing memory of the banking app?
  * e.g. your account number and password, which the video player could share online!
* Restrict access to non permitted memory ranges
  * The memory management unit (MMU) only makes memory ranges visible to a running program "belonging" to it 
* The MMU decides which part of the memory each CPU can access 

## The MMU 
* Idea: intercept "virtual" addresses generated by the CPU
  * MMU checks for "allowed" addresses 
  * It translates allowed addresses to "physical" addresses in main memory using a translation table
* Problem: translation table for each single address would be large 
  * Split memory into pages of identical size 
  * Apply the same translation to all addresses in the page:
    * Page table
      * Split memory into pages of identical size (power of 2)
      * Apply the same translation to all addresses in the page: page table
      * Find a compromise page size allowing flexibility and efficiency
      * Can use *sparse* tp reduce the page table size (when we dont want to use to much of the memory))
* MMUs were originally seperated ICs sitting between CPU and RAM
  * Or even realised using discrete components 
  * Higher integration due to Moore's La --> fit on CPU chip now 

## The memory translation process 
* The MMU splits the virtual address coming from the CPU into three parts
  * 10 bits(31-22) page directory entry (PDE) number
  * 10 bits (21-12) page directory entry (PTE) number
  * 12 bits (11-0) page offset inside the references page (untranslated)
* Translation process
1. Read PDE entry from directory: --> address of one page table
2. Read PTE entry from table: --> physical base address of memory page
3. Add offset from original virtual address (bits 11-0) to obtain the complete physical memory address

### Speeding up translation 
* Where is the page table stored? 
  * Can be several MB in size  --> doesn't fit on the CPU chip
  * Page directory and page tables are in main memory
* Using virtual memory address translation requires three main memory accesses
  * Same idea as with regular slow memory access: use cache
* The MMU uses a special cache on the CPU chip: the Translation Lookaside Buffer (TLB)
  * Caches commonly (most often? most recently?) used PTEs
  * The locality principle at work again
* More details on this an upcoming lecture 

## What about the operating system?
* New hardware capabilities have to be used efficiently 
* The operating system has to manage and multiplex the related resources
  * The OS has to adapt to new hardware capabilities
  * It has to provide code for all new capabilities
  * These often interact with other parts of the system, making the overall OS more complex
* A modern OS also has to ensure adherence to non-functional requirements (security, energu, real-time..)
  * The OS has to do more bookkeeping and statistics 
  * Some of the non-functional properties contradict each other
  * Unexpected problems may show up
* Finally, the OS itself has to be efficient

#Summary 
A computer, put in a simple fashion, consists of a device, memory and a processor. The CPUs are getting better and better,
but not the memory. The reason is that the transistors are getting smaller (Moore's law). But we are hitting physical
limitations, and the CPUs frequencies are 'stuck' at 3GHz. But we can use the transistors for something else. One thing
we can do is create bigger caches, but this causes computers to crash or in worst case flip bits. So, the most popular
way to make use of the transistors, is now to have more processors on the chip. New problems rises with this. Memory and
caches needs to satisfy n processors. This problem can be fixed with NUMA (non-unified memory architecture). And new
problems rises again. How to access data in another CPU's memory? Who decides which CPU is allowed to use the bus? 
Is common bus still efficient? On-chip network can achieve high throughput and low latencies. One can also include GPGPUs.
These are graphic processing units, which can run code. But what about security? Who can access each part of the memory?
This can be fixed by implementing MMUs. This device interprets 'virtual' addresses to physical addresses, and checks for
allowed access using a translation table. And again a new problem, translation table for each single address would be large.
We fix this by splitting memory into pages, and apply the same translation to all the addresses on the same page. 