# x86arch
My personal guide for the x86 architecture
(x86-32)



I will be using the Intel 80x86 ISA

The architecture has not really changed much from the 16x and because of that backwards compatibility is much more possible

To write assembly for an ISA you *must* know the names for the registers (as you store and compute data with them)

For the 8086 you have 4 general 16-bit registers being (AX,BX,CX,DX)

                 AX               BX               CD               DX   
            |__________|     |__________|     |__________|     |__________|
             *AH*  *AL*       *BH*   *BL*      *CH*  *CL*       *DH*  *DL*


Each of the registers have 8 "high" bits and 8 "low" bits, "low" being less inportant (significant) than the "high" bits

The ISA makes it possible to refer to the low bits and high bits individually

(AH,AL| BH,BL| CH,CL| DH,DL)

**XH and XL registers can be used as -1 byte registers to store 1-byte quantities**

 -(Important) Both are "tied" to the 16-bit register
 
  -Changing the value of AX will change the value of AH and AL
  
   -Changing the value of AH or AL will change the value of AX
   

*Two 16-bit registers*
 SI      |      DI

**These are basically general-purpose registers** 

 -But by convention they are often used as "pointers" (I.E they hold addresses)
 
  -and they *cannot* be decompressed into "high" or "low" 1-byte registers
  

**Two special 16-bit registers:**

 -BP: Base Pointer
 
  -SP: Stack Pointer
  
  (Will be written in-depth later)

**Four 16-bit segment registers**

 -CS: Code Segment
 
  -DS: Data Segment
  
   -SS: Stack Segment
   
  -ES: Extra Segment
     (will be talked about later but wont be used much)

**The 16-bit instruction pointer (IP) register:**

 -Points to the next instruction to execute
 
  -Never really used directly when writing assembly code

**The 16-bit FLAGS registers**

 -Information is stored in individual bits of the FLAGS register
 
  -Whenever an instruction is executed and produces a result, It can modify some bit(s) of the FLAGS register
  
   -EXAMPLE: Z (or ZF) denotes one bit of the FLAGS register, which is set to "1" if the previously executed instruction produced "0" or "0" overwise and lots of use (the FLAGS register)

    |    AH  |  |   AL  | = AX
    |    BH  |  |   BL  | = BX
    |    CH  |  |   CL  | = CX
    |    DH  |  |   DL  | = DX
    |         SI        |
    |___________________|
    |         DI        |
    |___________________|
    |         BP        |
    |___________________|
    |         SP        |
    |___________________|
    |         IP        |
    |___________________|
    |_|_|_|_|_|_|_|_|_|_| = FLAGS
    |         CS        |
    |___________________|
    |         DS        |
    |___________________|
    |         SS        |
    |___________________|
    |         ES        |
    |___________________|
    ---------------------
    \                   /
     \                 /
      \              /
       \            /
    {______16-bits______}
         ^       v
      [     ALU      ]
         ^        v
       Control unit

**As mentioned above, There are several registers that are used for holding addresses for memory locations**

-Segments (CS,DS,SS,ES)

 -Pointers:
 
 SI,DI: indices (Typically used for pointers)
 
 SP: Stack Pointer
 
 BP: (Stack) Base pointer
 
 IP: Pointer to next instruction
 
 **In a 8086 processor, a program iimited to referencing an address space of size 1mb (Thats 2^20 bytes)**
 -therefore, addresses are 20-bit long
 -A d-bit long address allows to reference 2^d diffrent "things"
 -Example:
  2-bit "00 01 10 11" (4 "things")
  3-bit "000 001 010 011 100 101 110 111" (8 "things")

  In this case, these things are "bytes" 
  -One does not address anything smaller than a byte
  -Therefore, a 20-bit address makes it possible to address 2^20 individual bytes, or 1MIB
