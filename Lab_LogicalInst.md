# Challenge
This project uses xor with a value against another value and then itself.
This is to prove that xor changes a value to 0
 
 ```assembly
section .text
        global _start

_start:
        mov eax, var1
        xor eax, var2
        test eax,1              ;Test value is even or odd
        jnz evnn

        mov eax, var1
        xor eax, var1
        test eax,1              ;Test value is even or odd
        jnz evnn

        mov eax,'n'
        mov [result],eax        ;this will print 'n', ascii 110

        jmp exit
evnn:
        mov eax,'y'
        mov [result],eax ; this will print 'y', ascii 121
exit:
        mov eax,1
        int 0x80
segment .bss
        result resb 1
section .data
        var1 equ 5
        var2 equ 4

```
