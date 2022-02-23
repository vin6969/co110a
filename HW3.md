## Half adder

CHIP HalfAdder {
    IN a, b;    // 1-bit inputs
    OUT sum,    // Right bit of a + b 
        carry;  // Left bit of a + b

    PARTS:
    // Put you code here:
    Xor(a=a, b=b, out=sum);
    And(a=a, b=b, out=carry);
}

![](https://github.com/vin6969/co110a/blob/58254bf8a335f4c78be208c9ea5ff3239f8890c5/media/gates/Half%20adder.png)


## Full Adder

CHIP FullAdder {
    IN a, b, c;  // 1-bit inputs
    OUT sum,     // Right bit of a + b + c
        carry;   // Left bit of a + b + c

    PARTS:
    // Put you code here:
    Xor(a=a, b=b, out=t1);
    Xor(a=t1, b=c, out=sum);
    And(a=a, b=b, out=t2);
    And(a=a, b=c, out=t3);
    And(a=b, b=c, out=t4);
    Or(a=t2, b=t3, out=t5);
    Or(a=t4, b=t5, out=carry);
}

![](https://github.com/vin6969/co110a/blob/58254bf8a335f4c78be208c9ea5ff3239f8890c5/media/gates/Full%20adder.png)

## Adder16

CHIP ADDER16 { 
	IN a[16], b[16];
	OUT out[16];
  
	PARTS:
	FULLADDER(a=a[0], b=b[0], c=false, sum=out[0], carry=car1);
	FULLADDER(a=a[1], b=b[1], c=car1, sum=out[1], carry=car2);
	FULLADDER(a=a[2], b=b[2], c=car2, sum=out[2], carry=car3);
	FULLADDER(a=a[3], b=b[3], c=car3, sum=out[3], carry=car4);
	FULLADDER(a=a[4], b=b[4], c=car4, sum=out[4], carry=car5);
	FULLADDER(a=a[5], b=b[5], c=car5, sum=out[5], carry=car6);
	FULLADDER(a=a[6], b=b[6], c=car6, sum=out[6], carry=car7);
	FULLADDER(a=a[7], b=b[7], c=car7, sum=out[7], carry=car8);
	FULLADDER(a=a[8], b=b[8], c=car8, sum=out[8], carry=car9);
	FULLADDER(a=a[9], b=b[9], c=car9, sum=out[9], carry=car10);
	FULLADDER(a=a[10], b=b[10], c=car10, sum=out[10], carry=car11);
	FULLADDER(a=a[11], b=b[11], c=car11, sum=out[11], carry=car12);
	FULLADDER(a=a[12], b=b[12], c=car12, sum=out[12], carry=car13);
	FULLADDER(a=a[13], b=b[13], c=car13, sum=out[13], carry=car14);
	FULLADDER(a=a[14], b=b[14], c=car14, sum=out[14], carry=car15);
	FULLADDER(a=a[15], b=b[15], c=car15, sum=out[15], carry=car16);
}

![](https://github.com/vin6969/co110a/blob/58254bf8a335f4c78be208c9ea5ff3239f8890c5/media/gates/adder16.jpg)


## Inc16

CHIP Inc16 {
    IN in[16];
    OUT out[16];

    PARTS:
Add16(a=in,b[0]=true,out=out);
}

![](https://github.com/vin6969/co110a/blob/58254bf8a335f4c78be208c9ea5ff3239f8890c5/media/gates/inc16.jpg)


