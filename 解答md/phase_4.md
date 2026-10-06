rdi=x



   0x0000000000401bb9 <+0>:     push   %rbp
   0x0000000000401bba <+1>:     mov    %rsp,%rbp
   0x0000000000401bbd <+4>:     sub    $0x20,%rsp
   0x0000000000401bc1 <+8>:     mov    %rdi,-0x18(%rbp)  (rbp-18)=rdi=x
   0x0000000000401bc5 <+12>:    mov    %fs:0x28,%rax
   0x0000000000401bce <+21>:    mov    %rax,-0x8(%rbp)
   0x0000000000401bd2 <+25>:    xor    %eax,%eax



   0x0000000000401bd4 <+27>:    lea    -0xc(%rbp),%rcx   ;rcx=rbp-0xc(地址)
   0x0000000000401bd8 <+31>:    lea    -0x10(%rbp),%rdx  ;rdx=rbp-0x10(地址)
   0x0000000000401bdc <+35>:    mov    -0x18(%rbp),%rax  ;rax=(rbp-0x18)=x
   0x0000000000401be0 <+39>:    mov    $0x402330,%esi    ；rsi=0x402330(%d %d)
   0x0000000000401be5 <+44>:    mov    %rax,%rdi         ;rdi=x
   0x0000000000401be8 <+47>:    mov    $0x0,%eax         ;rax=0
   0x0000000000401bed <+52>:    call   0x4010c0 <__isoc99_sscanf@plt>     ;第一个输入放rbp-0x10,第二个放rbp-0xc,设为b，c
   0x0000000000401bf2 <+57>:    cmp    $0x2,%eax              ;输入等于两个不爆炸 
   0x0000000000401bf5 <+60>:    je     0x401bfc <phase_4+67>
   0x0000000000401bf7 <+62>:    call   0x401825 <explode_bomb>
   0x0000000000401bfc <+67>:    mov    -0x10(%rbp),%eax       ;rax=b
   0x0000000000401bff <+70>:    cmp    $0xe,%eax          
   0x0000000000401c02 <+73>:    jbe    0x401c09 <phase_4+80>   ;(0<=b<=0xe不爆炸)
   0x0000000000401c04 <+75>:    call   0x401825 <explode_bomb>
   0x0000000000401c09 <+80>:    mov    -0x10(%rbp),%eax      ;eax=b
   0x0000000000401c0c <+83>:    mov    $0xe,%edx             ;edx=0xe
   0x0000000000401c11 <+88>:    mov    $0x0,%esi             ;esi=0
   0x0000000000401c16 <+93>:    mov    %eax,%edi             ;edi=b
   0x0000000000401c18 <+95>:    call   0x401b43 <func4>      

func4:
rdi=b,rsi=0,rdx=0xe


   0x0000000000401b43 <+0>:     push   %rbp
   0x0000000000401b44 <+1>:     mov    %rsp,%rbp
   0x0000000000401b47 <+4>:     sub    $0x20,%rsp
   0x0000000000401b4b <+8>:     mov    %edi,-0x14(%rbp)    ;(rbp1-0x14)=b
   0x0000000000401b4e <+11>:    mov    %esi,-0x18(%rbp)    ;(rbp1-0x18)=0 
   0x0000000000401b51 <+14>:    mov    %edx,-0x1c(%rbp)    ;(rbp1-0x1c)=0xe
   0x0000000000401b54 <+17>:    mov    -0x1c(%rbp),%eax    ;eax=0xe
   0x0000000000401b57 <+20>:    sub    -0x18(%rbp),%eax    ;eax=0xe
   0x0000000000401b5a <+23>:    mov    %eax,%edx           ;edx=0xe
   0x0000000000401b5c <+25>:    shr    $0x1f,%edx          ;edx>>0x1f
   0x0000000000401b5f <+28>:    add    %edx,%eax           ;eax=0xe+edx=0xe+0xe>>0x1f=0xe+0xe/(2^37)=0xe
   0x0000000000401b61 <+30>:    sar    $1,%eax             ;eax=eax>>1=0x7(算术右移)
   0x0000000000401b63 <+32>:    mov    %eax,%edx           ;edx=eax=(0xe+0xe/(2^37))>>1=0x7
   0x0000000000401b65 <+34>:    mov    -0x18(%rbp),%eax    ;eax=0
   0x0000000000401b68 <+37>:    add    %edx,%eax           ;eax=edx=(0xe+0xe/(2^37))>>1=0x7
   0x0000000000401b6a <+39>:    mov    %eax,-0x4(%rbp)     ;(rbp1-0x4)=(0xe+0xe/(2^37))>>1=0x7
   0x0000000000401b6d <+42>:    mov    -0x4(%rbp),%eax     ;rax=(0xe+0xe/(2^37))>>1=0x7
   0x0000000000401b70 <+45>:    cmp    -0x14(%rbp),%eax    ;rax<=b,即 7<=b 跳转到75,>75再次调用函数
   0x0000000000401b73 <+48>:    jle    0x401b8e <func4+75>
   0x0000000000401b75 <+50>:    mov    -0x4(%rbp),%eax     ;rax=(0xe+0xe/(2^37))>>1=0x7
   0x0000000000401b78 <+53>:    lea    -0x1(%rax),%edx     ;rdx=(0xe+0xe/(2^37))>>1-1=0x6
   0x0000000000401b7b <+56>:    mov    -0x18(%rbp),%ecx    ;rcx=0
   0x0000000000401b7e <+59>:    mov    -0x14(%rbp),%eax    ;rax=b
   0x0000000000401b81 <+62>:    mov    %ecx,%esi           ;rsi=rcx=0
   0x0000000000401b83 <+64>:    mov    %eax,%edi           ;rdi=rax==b
     rdi=b,rsi=0,rdx=6
   0x0000000000401b85 <+66>:    call   0x401b43 <func4>    ;调用函数
   0x0000000000401b8a <+71>:    add    %eax,%eax
   0x0000000000401b8c <+73>:    jmp    0x401bb7 <func4+116>
   0x0000000000401b8e <+75>:    mov    -0x4(%rbp),%eax   ;rax=(0xe+0xe/(2^37))>>1=0x7
   0x0000000000401b91 <+78>:    cmp    -0x14(%rbp),%eax  ;rax>=b,即7>=b跳转到111
   0x0000000000401b94 <+81>:    jge    0x401bb2 <func4+111>
   0x0000000000401b96 <+83>:    mov    -0x4(%rbp),%eax   ;rax=(0xe+0xe/(2^37))>>1=0x7
   0x0000000000401b99 <+86>:    lea    0x1(%rax),%ecx    ;rcx=(0xe+0xe/(2^37))>>1+1=0x8
   0x0000000000401b9c <+89>:    mov    -0x1c(%rbp),%edx  ;rdx=0xe
   0x0000000000401b9f <+92>:    mov    -0x14(%rbp),%eax  ;rax=b
   0x0000000000401ba2 <+95>:    mov    %ecx,%esi         ;rsi=(0xe+0xe/(2^37))>>1-1=0x8
   0x0000000000401ba4 <+97>:    mov    %eax,%edi         ;rdi=b
   
   rdi=b,rsi=8,rdx=0xe

   0x0000000000401ba6 <+99>:    call   0x401b43 <func4>  ;返回错误rax,rax!=0
   0x0000000000401bab <+104>:   add    %eax,%eax         ;rax=rax*2
   0x0000000000401bad <+106>:   add    $0x1,%eax         ;rax=rax+1
   0x0000000000401bb0 <+109>:   jmp    0x401bb7 <func4+116>;跳到结束
   0x0000000000401bb2 <+111>:   mov    $0x0,%eax  rax=0   ;返回正确rax=0
   0x0000000000401bb7 <+116>:   leave
   0x0000000000401bb8 <+117>:   ret



;第一个输入放rbp-0x10,第二个放rbp-0xc,设为b，c

   0x0000000000401c1d <+100>:   test   %eax,%eax
   0x0000000000401c1f <+102>:   je     0x401c26 <phase_4+109>  ;rax=0不爆炸
   0x0000000000401c21 <+104>:   call   0x401825 <explode_bomb>
   0x0000000000401c26 <+109>:   mov    -0xc(%rbp),%eax         ;eax=c
   0x0000000000401c29 <+112>:   test   %eax,%eax               ;
   0x0000000000401c2b <+114>:   je     0x401c32 <phase_4+121>  ;eax=0不爆炸，也就是c=0
   0x0000000000401c2d <+116>:   call   0x401825 <explode_bomb> 
   0x0000000000401c32 <+121>:   nop



   0x0000000000401c33 <+122>:   mov    -0x8(%rbp),%rax
   0x0000000000401c37 <+126>:   sub    %fs:0x28,%rax
   0x0000000000401c40 <+135>:   je     0x401c47 <phase_4+142>
   0x0000000000401c42 <+137>:   call   0x401050 <__stack_chk_fail@plt>
   0x0000000000401c47 <+142>:   leave
   0x0000000000401c48 <+143>:   ret






   