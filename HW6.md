## Ram64

/**
 * Memory of 64 registers, each 16-bit wide.  
 * The chip facilitates read and write operations, as follows:
 *     Read:  out(t) = RAM64[address(t)](t)
 *     Write: If load(t-1) then RAM64[address(t-1)](t) = in(t-1)
 * In words: the chip always outputs the value stored at the memory 
 * location specified by address. If load == 1, the in value is loaded 
 * into the memory location specified by address.  This value becomes 
 * available through the out output starting from the next time step.
 */

CHIP RAM64 {
    IN in[16], load, address[6];
    OUT out[16];

    PARTS:
	DMux8Way(in=load, sel=address[3..5], a=loada, b=loadb, c=loadc, d=loadd, e=loade, f=loadf, g=loadg, h=loadh);
	RAM8(in=in, load=loada, address=address[0..2], out=outa);
	RAM8(in=in, load=loadb, address=address[0..2], out=outb);
	RAM8(in=in, load=loadc, address=address[0..2], out=outc);
	RAM8(in=in, load=loadd, address=address[0..2], out=outd);
	RAM8(in=in, load=loade, address=address[0..2], out=oute);
	RAM8(in=in, load=loadf, address=address[0..2], out=outf);
	RAM8(in=in, load=loadg, address=address[0..2], out=outg);
	RAM8(in=in, load=loadh, address=address[0..2], out=outh);
	Mux8Way16(a=outa, b=outb, c=outc, d=outd, e=oute, f=outf, g=outg, h=outh, sel=address[3..5], out=out);	
}

![](https://github.com/vin6969/co110a/blob/master/media/gates/ram64.png)

## Ram512

/**
 * Memory of 512 registers, each 16-bit wide.  
 * The chip facilitates read and write operations, as follows:
 *     Read:  out(t) = RAM512[address(t)](t)
 *     Write: If load(t-1) then RAM512[address(t-1)](t) = in(t-1)
 * In words: the chip always outputs the value stored at the memory 
 * location specified by address. If load == 1, the in value is loaded 
 * into the memory location specified by address.  This value becomes 
 * available through the out output starting from the next time step.
 */

CHIP RAM512 {
    IN in[16], load, address[9];
    OUT out[16];

    PARTS:
	DMux8Way(in=load, sel=address[6..8], a=loada, b=loadb, c=loadc, d=loadd, e=loade, f=loadf, g=loadg, h=loadh);
	RAM64(in=in, load=loada, address=address[0..5], out=outa);
	RAM64(in=in, load=loadb, address=address[0..5], out=outb);
	RAM64(in=in, load=loadc, address=address[0..5], out=outc);
	RAM64(in=in, load=loadd, address=address[0..5], out=outd);
	RAM64(in=in, load=loade, address=address[0..5], out=oute);
	RAM64(in=in, load=loadf, address=address[0..5], out=outf);
	RAM64(in=in, load=loadg, address=address[0..5], out=outg);
	RAM64(in=in, load=loadh, address=address[0..5], out=outh);
	Mux8Way16(a=outa, b=outb, c=outc, d=outd, e=oute, f=outf, g=outg, h=outh, sel=address[6..8], out=out);	
}



## Ram4k

/**
 * Memory of 4K registers, each 16-bit wide.  
 * The chip facilitates read and write operations, as follows:
 *     Read:  out(t) = RAM4K[address(t)](t)
 *     Write: If load(t-1) then RAM4K[address(t-1)](t) = in(t-1)
 * In words: the chip always outputs the value stored at the memory 
 * location specified by address. If load == 1, the in value is loaded 
 * into the memory location specified by address.  This value becomes 
 * available through the out output starting from the next time step.
 */

CHIP RAM4K {
    IN in[16], load, address[12];
    OUT out[16];

    PARTS:
	DMux8Way(in=load, sel=address[9..11], a=loada, b=loadb, c=loadc, d=loadd, e=loade, f=loadf, g=loadg, h=loadh);
	RAM512(in=in, load=loada, address=address[0..8], out=outa);
	RAM512(in=in, load=loadb, address=address[0..8], out=outb);
	RAM512(in=in, load=loadc, address=address[0..8], out=outc);
	RAM512(in=in, load=loadd, address=address[0..8], out=outd);
	RAM512(in=in, load=loade, address=address[0..8], out=oute);
	RAM512(in=in, load=loadf, address=address[0..8], out=outf);
	RAM512(in=in, load=loadg, address=address[0..8], out=outg);
	RAM512(in=in, load=loadh, address=address[0..8], out=outh);
	Mux8Way16(a=outa, b=outb, c=outc, d=outd, e=oute, f=outf, g=outg, h=outh, sel=address[9..11], out=out);	
}



## Ram16k

/**
 * Memory of 16K registers, each 16-bit wide.  
 * The chip facilitates read and write operations, as follows:
 *     Read:  out(t) = RAM16K[address(t)](t)
 *     Write: If load(t-1) then RAM16K[address(t-1)](t) = in(t-1)
 * In words: the chip always outputs the value stored at the memory 
 * location specified by address. If load=1, the in value is loaded 
 * into the memory location specified by address.  This value becomes 
 * available through the out output starting from the next time step.
 */

CHIP RAM16K {
    IN in[16], load, address[14];
    OUT out[16];

    PARTS:
	DMux4Way(in=load, sel=address[12..13], a=loada, b=loadb, c=loadc, d=loadd);
	RAM4K(in=in, load=loada, address=address[0..11], out=outa);
	RAM4K(in=in, load=loadb, address=address[0..11], out=outb);
	RAM4K(in=in, load=loadc, address=address[0..11], out=outc);
	RAM4K(in=in, load=loadd, address=address[0..11], out=outd);
	Mux4Way16(a=outa, b=outb, c=outc, d=outd, sel=address[12..13], out=out);	
}

![](https://github.com/vin6969/co110a/blob/master/media/gates/ram16k.png)

## PC

/**
 * A 16-bit counter with load and reset control bits.
 * if      (reset[t]==1) out[t+1] = 0
 * else if (load[t]==1)  out[t+1] = in[t]
 * else if (inc[t]==1)   out[t+1] = out[t] + 1  (integer addition)
 * else                  out[t+1] = out[t]
 */

CHIP PC {
    IN in[16],load,inc,reset;
    OUT out[16];

    PARTS:
    // increment the output of the register
    Inc16(in = feedback, out = pc);

    // "Sequential chips always consist of a layer of DFFs sandwiched
    // between optional combinational logic layers" - Figure 3.4
    // The next 3 lines are a combinational logic layer to figure 
    // out what gets fed to the register. Either the program counter,
    // the incremented pc, the input, or zeros on a reset

    Mux16(a = feedback, b = pc, sel = inc, out = w0);
    Mux16(a = w0, b = in, sel = load, out = w1);
    Mux16(a = w1, b = false, sel = reset, out = cout);

    // the output from the register also needs to get fed back through 
    // the combinational logic to get processed for the next clock cycle.
    Register(in = cout, load = true, out = out, out = feedback);
}

![](https://github.com/vin6969/co110a/blob/master/media/gates/pc.png)










