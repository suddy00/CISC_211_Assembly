```assembly
section .text
        global _start

_start:
        mov eax, 57       ; reset eax to 10
label:
        mov [number], eax

        ;Printing process
        mov eax, 4
        mov ebx, 1
        mov ecx, number
        mov edx, 1
        int 0x80

        ;Compare and loop
        mov eax, [number]
        dec eax
        cmp eax,48
        jg label        ;jump if greater than 0

        ;Exit program
        mov eax,1
        int 0x80

segment .bss
        number resb 2

```
