multi:

    // This file is part of www.nand2tetris.org
    // and the book "The Elements of Computing Systems"
    // by Nisan and Schocken, MIT Press.
    // File name: projects/04/Mult.asm

    // Multiplies R0 and R1 and stores the result in R2.
    // (R0, R1, R2 refer to RAM[0], RAM[1], and RAM[2], respectively.)

    // Put your code here.
    @2    // r2=0(歸0)
    M=0
    @0   //r0=M 
    D=M
    @21  //IF r0=0 , 跳至 r21結束  0*任何數=0
    D;JEQ 
    @1  //r1=M
    D=M
    @3
    M=D //計算次數(最後會歸0)
    @21 //IF r1=0,跳至 r21結束 任何數*0=0
    D;JEQ
    @14 //LOOP 
    D;JNE
    @0
    D=M
    @2
    M=M+D // 相加x次(乘法)
    @3
    M=M-1
    D=M
    @12 //LOOP
    D;JNE
    @21 //卡迴圈
    0;JMP

![image](https://github.com/vin6969/co110a/blob/master/media/gates/mult.png)





Fill:

    // This file is part of www.nand2tetris.org
    // and the book "The Elements of Computing Systems"
    // by Nisan and Schocken, MIT Press.
    // File name: projects/04/Fill.asm

    // Runs an infinite loop that listens to the keyboard input.
    // When a key is pressed (any key), the program blackens the screen,
    // i.e. writes "black" in every pixel;
    // the screen should remain fully black as long as the key is pressed. 
    // When no key is pressed, the program clears the screen, i.e. writes
    // "white" in every pixel;
    // the screen should remain fully clear as long as no key is pressed.

    // Put your code here.
    //16384>>螢幕
    //24576>>鍵盤


    @8192           //所有螢幕範圍       
    D=A               
    @0                
    M=D                
    @24576
    D=M
    @18                  
    D;JNE            // 按下鍵盤(out!=0) 跳至 18

    @0
    D=M               
    M=M-1                
    @0              
    D;JEQ           //IF 輸出==0 跳至 0    
    @16383          //16384開始是螢幕
    A=D+A                
    M=0              
    @8                
    0;JMP         //開始下次迴圈       
    //畫黑線
    @0
    D=M
    M=M-1
    @0
    D;JEQ        //IF 輸出==0 跳至 0        
    @24576
    A=A-D
    M=-1
    @18
    0;JMP       //開始下次迴圈
