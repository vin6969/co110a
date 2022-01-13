Memory:

// This file is part of www.nand2tetris.org
// and the book "The Elements of Computing Systems"
// by Nisan and Schocken, MIT Press.
// File name: projects/05/Memory.hdl

/**
 * This chip implements the complete address space of the 
 * computer's data memory, including RAM and memory mapped I/O. 
 * The chip facilitates read and write operations, as follows:
 *     Read:  out(t) = Memory[address(t)](t)
 *     Write: If load(t-1) then Memory[address(t-1)](t) = in(t-1)
 * In words: the chip always outputs the value stored at the memory 
 * location specified by address. If load == 1, the in value is loaded 
 * into the memory location specified by address. This value becomes 
 * available through the out output in the next time step.
 * Address space rules:
 * Only the upper 16K+8K+1 words of the Memory chip are used. 
 * Access to address>0x6000 is invalid. Access to any address in 
 * the range 0x4000 to 0x5FFF results in accessing the screen memory 
 * map. Access to address 0x6000 results in accessing the keyboard 
 * memory map. The behavior in these addresses is described in the 
 * Screen and Keyboard chip specifications given in the book.
 */

CHIP Memory {
    IN in[16], load, address[15];
    OUT out[16];

    PARTS:
	DMux4Way(in=load, sel=address[13..14], a=loadram1, b=loadram2, c=loadscreen, d=loadkbd);
	Or(a=loadram1, b=loadram2, out=loadram);
    RAM16K(in=in, load=loadram, address=address[0..13], out=ramout);
    Screen(in=in, load=loadscreen, address=address[0..12], out=scrout);
    Keyboard(out=kbout);
    Mux4Way16(a=ramout, b=ramout, c=scrout, d=kbout, sel=address[13..14], out=out);
}
// 0000 000 RAM start
// 0011 FFF RAM end
// 0100 000 Screen start
// 0101 FFF Screen end
// 0110 000 Keyboard


Computer:

![Memory](https://github.com/vin6969/co110a/blob/master/media/gates/computer.png)

// This file is part of www.nand2tetris.org
// and the book "The Elements of Computing Systems"
// by Nisan and Schocken, MIT Press.
// File name: projects/05/Computer.hdl

/**
 * The Computer chip, i.e. the top-most chip of the Hack architecture.
 * The Computer chip consists of CPU, ROM and RAM chip-parts.
 * It is assumed that the ROM is pre-loaded with some Hack program.
 * The Computer chip has a single 1-bit input, named "reset".
 * When reset is 0, the stored program starts executing.
 * When reset is 1, the program's execution restarts. 
 * Thus, to start a program’s execution, reset must be pushed "up" (1)
 * and "down" (0). From this point onward the user is at the mercy of 
 * the software. In particular, depending on the program loaded into
 * the computer, the screen may show some output and the user may be 
 * expected to interact with the computer via the keyboard.
 */

CHIP Computer {

    IN reset;

    PARTS:
    ROM32K(address=pc, out=instruction);
    CPU(inM=memOut, instruction=instruction, reset=reset, outM=outM, 
        writeM=writeM, addressM=addressM, pc=pc);
    Memory(in=outM, load=writeM, address=addressM, out=memOut);
}
