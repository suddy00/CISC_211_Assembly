# The loop instruction will loop for the value in the ECX register, decrementing the value with each iteration. 

Counter
```assembly
  GNU nano 6.2                               counter4.asm                                         
section .text
        global _start

_start:
        mov ecx, 10  ;ecx is a counter register

label:
        inc eax
        loop label

        mov eax,1
        int 0x80
```

Fibonacci
```assembly
section .text
        global _start

_start:
        mov ebx, 0
        mov eax, 1
        mov ecx, 10

        mov [num], eax
        add edx, eax    ;getting the total value of all

fi_loop:

        mov [num], eax

        add eax, ebx
        mov ebx, [num]

        add edx, eax

        loop fi_loop
        jmp exit

exit:
        mov eax,1
        int 0x80

segment .bss
        num resb 1

```
