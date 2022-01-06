## ALU-nostat

CHIP ALU {

    IN  
        x[16], y[16],  // 16-bit inputs        
        zx, // zero the x input?
        nx, // negate the x input?
        zy, // zero the y input?
        ny, // negate the y input?
        f,  // compute  out = x + y (if 1) or out = x & y (if 0)
        no; // negate the out output?

    OUT 
        out[16], // 16-bit output
        zr, // 1 if (out==0), 0 otherwise
        ng; // 1 if (out<0),  0 otherwise


    PARTS:
    Mux16(a=x,b[0..15]=false,sel=zx,out=zdx); //Zero the x
    Not16(in=zdx,out=notx);                  //Not the x
    Mux16(a=zdx,b=notx,sel=nx,out=ndx);      //chose x or notx
    // ditto for y
    Mux16(a=y,b[0..15]=false,sel=zy,out=zdy);
    Not16(in=zdy,out=noty);
    Mux16(a=zdy,b=noty,sel=ny,out=ndy);

    Add16(a=ndx,b=ndy,out=xplusy); //x+y
    And16(a=ndx,b=ndy,out=xandy);  //x&y
    Mux16(a=xandy,b=xplusy,sel=f,out=fxy);  //chose function

     Not16(in=fxy,out=nfxy);      //not the output or not
    Mux16(a=fxy,b=nfxy,sel=no,out=oo);  //chose which


    Or16Way(in=oo,out=o);  //for zr
    Not(in=o,out=zr);

    And16(a[0..15]=true,b=oo,out[15]=ng,out[0..14]=drop); //ng

    Or16(a=oo,b[0..15]=false,out=out); //oo=output
}




![](https://github.com/vin6969/co110a/blob/cfd6ca1a2ed0f628fdf05fae07a71ff6d5cffa89/media/gates/alu.png)
