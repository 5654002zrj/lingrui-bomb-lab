    rdi=x（字符串首地址）        fs:0x28=y

0x00000000004019ef <+0>:     push   %rbp
   0x00000000004019f0 <+1>:     mov    %rsp,%rbp
   0x00000000004019f3 <+4>:     sub    $0x40,%rsp 
   0x00000000004019f7 <+8>:     mov    %rdi,-0x38(%rbp)     ；(rbp-0x38)=x
   0x00000000004019fb <+12>:    mov    %fs:0x28,%rax  ;rax=y
   0x0000000000401a04 <+21>:    mov    %rax,-0x8(%rbp)     ;rax=(rbp-0x8) 
   0x0000000000401a08 <+25>:    xor    %eax,%eax            ; eax=0


   0x0000000000401a0a <+27>:    lea    -0x20(%rbp),%rdx      ; rdx=rbp-0x20
   0x0000000000401a0e <+31>:    mov    -0x38(%rbp),%rax       ;rax=(rbp-0x38) 
   0x0000000000401a12 <+35>:    mov    %rdx,%rsi          ;rsi=rdx=rbp-0x20
   0x0000000000401a15 <+38>:    mov    %rax,%rdi           ; rdi=(rbp-38)=x
   0x0000000000401a18 <+41>:    call   0x4017bc <read_six_numbers>        读取六个数字

   read six numbers：
   0x00000000004017bc <+0>:     push   %rbp
   0x00000000004017bd <+1>:     mov    %rsp,%rbp
   0x00000000004017c0 <+4>:     sub    $0x20,%rsp
   0x00000000004017c4 <+8>:     mov    %rdi,-0x18(%rbp)   ; rbp-18=x
   0x00000000004017c8 <+12>:    mov    %rsi,-0x20(%rbp)   ; (rbp-20)=旧的rbp-20
   0x00000000004017cc <+16>:    mov    -0x20(%rbp),%rax   ；rax=旧的rbp-0x20
   0x00000000004017d0 <+20>:    lea    0x14(%rax),%rdi    ; rdi=旧的rbp-0x20+20
   0x00000000004017d4 <+24>:    mov    -0x20(%rbp),%rax   ;rax=旧的rbp-0x20
   0x00000000004017d8 <+28>:    lea    0x10(%rax),%rsi    ;rsi=旧的rbp-0x20+16
   0x00000000004017dc <+32>:    mov    -0x20(%rbp),%rax   ; rax=旧的rbp-0x20
   0x00000000004017e0 <+36>:    lea    0xc(%rax),%r9      r9=旧的rbp-0x20+12
   0x00000000004017e4 <+40>:    mov    -0x20(%rbp),%rax   rax=旧的rbp-0x20
   0x00000000004017e8 <+44>:    lea    0x8(%rax),%r8      r8=旧的rbp-0x20+8
   0x00000000004017ec <+48>:    mov    -0x20(%rbp),%rax   rax=旧的rbp-20
   0x00000000004017f0 <+52>:    lea    0x4(%rax),%rcx     rcx=旧的rbp-0x20+4
   0x00000000004017f4 <+56>:    mov    -0x20(%rbp),%rdx   rdx=rbp-0x20
   0x00000000004017f8 <+60>:    mov    -0x18(%rbp),%rax   rax=x       (rax=x,rdx=rbp-0x20,rcx=rbp-0x20+4,r8= +8,r9= +12,rsi= +16,rdi= +20)
   0x00000000004017fc <+64>:    push   %rdi  ;多余参数放栈
   0x00000000004017fd <+65>:    push   %rsi  ;多余参数放栈
   0x00000000004017fe <+66>:    mov    $0x402210,%esi   ;esi=0x402210,这是格式字符串地址即六个%d,sscanf(字符串地址，格式字符串地址，参数地址)
   0x0000000000401803 <+71>:    mov    %rax,%rdi      rdi=x
   0x0000000000401806 <+74>:    mov    $0x0,%eax      rax=0
   0x000000000040180b <+79>:    call   0x4010c0 <__isoc99_sscanf@plt>   
   0x0000000000401810 <+84>:    add    $0x10,%rsp  
   0x0000000000401814 <+88>:    mov    %eax,-0x4(%rbp)  rbp-4=eax
   0x0000000000401817 <+91>:    cmpl   $0x5,-0x4(%rbp)  
   0x000000000040181b <+95>:    jg     0x401822 <read_six_numbers+102>  eax>5不爆炸
   0x000000000040181d <+97>:    call   0x401825 <explode_bomb>
   0x0000000000401822 <+102>:   nop
   0x0000000000401823 <+103>:   leave
   0x0000000000401824 <+104>:   ret

   0x0000000000401a1d <+46>:    mov    -0x20(%rbp),%eax        eax=(rbp-20)=num[0]
   0x0000000000401a20 <+49>:    cmp    $0x1,%eax   
   0x0000000000401a23 <+52>:    je     0x401a2a <phase_2+59>   eax=1就不爆炸
   0x0000000000401a25 <+54>:    call   0x401825 <explode_bomb>
   0x0000000000401a2a <+59>:    movl   $0x1,-0x24(%rbp)  ;(rbp-0x24)=1
   0x0000000000401a31 <+66>:    jmp    0x401a57 <phase_2+104>
   0x0000000000401a33 <+68>:    mov    -0x24(%rbp),%eax ;eax=(rbp-0x24)=1
   0x0000000000401a36 <+71>:    cltq 
   0x0000000000401a38 <+73>:    mov    -0x20(%rbp,%rax,4),%edx //edx=(rbp+4*rax-20)=(rbp-0x1c)=num[i]
   0x0000000000401a3c <+77>:    mov    -0x24(%rbp),%eax   rax=(rbp-0x24)=1
   0x0000000000401a3f <+80>:    sub    $0x1,%eax   //rax=(rbp-24)-1=i-1
   0x0000000000401a42 <+83>:    cltq
   0x0000000000401a44 <+85>:    mov    -0x20(%rbp,%rax,4),%eax  //eax=(rbp+4*rax-20)=rbp-0x20=num[i-1]
   0x0000000000401a48 <+89>:    add    %eax,%eax  eax=eax*2
   0x0000000000401a4a <+91>:    cmp    %eax,%edx  //eax=edx就不爆炸,num[i]=2*num[i-1]
   0x0000000000401a4c <+93>:    je     0x401a53 <phase_2+100>
   0x0000000000401a4e <+95>:    call   0x401825 <explode_bomb>  //eax=edx就不爆炸
   0x0000000000401a53 <+100>:   addl   $0x1,-0x24(%rbp)  (rbp-0x24)=(rbp-0x24)+1=i+1
   0x0000000000401a57 <+104>:   cmpl   $0x5,-0x24(%rbp)  i<=5就循环
   0x0000000000401a5b <+108>:   jle    0x401a33 <phase_2+68>
   0x0000000000401a5d <+110>:   nop


   0x0000000000401a5e <+111>:   mov    -0x8(%rbp),%rax
   0x0000000000401a62 <+115>:   sub    %fs:0x28,%rax
   0x0000000000401a6b <+124>:   je     0x401a72 <phase_2+131>
   0x0000000000401a6d <+126>:   call   0x401050 <__stack_chk_fail@plt>
   0x0000000000401a72 <+131>:   leave
   0x0000000000401a73 <+132>:   ret