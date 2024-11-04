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
          
