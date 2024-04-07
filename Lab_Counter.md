
```Assembly
section .text
        global _start

_start:
        mov eax, 49             ; Set eax to 1

label1:

        mov [number], eax

    ;Printing first number
        mov eax, 4
        mov ebx, 1
        mov ecx, number
        mov edx, 1
        int 0x80

    ;Printing a space
        mov eax, 4
        mov ebx, 1
        mov ecx, space
        mov edx, 1
        int 0x80

    ;Compare and loop limit
        mov eax, [number]
        add eax, 2
        cmp eax, limit
        jl label1        ;Loop if less than 10

        mov eax, 49

label2: ;Second loop for greater than 10

        mov [number], eax       ; Placing 1 in number

    ;Printing 1
        mov eax, 4
        mov ebx, 1
        mov ecx, num2
        mov edx, 1
        int 0x80

    ;Printing second digit
        mov eax, 4
        mov ebx, 1
        mov ecx, number
        mov edx, 1
        int 0x80

    ;Printing a space
        mov eax, 4
        mov ebx, 1
        mov ecx, space
        mov edx, 1
        int 0x80

        ;Compare eax to loop limit
        mov eax, [number]
        add eax, 2
        cmp eax, limit
        jl label2        ;jump if less than 20

    ;Printing a newline
        mov eax, 4
        mov ebx, 1
        mov ecx, newline
        mov edx, 1
        int 0x80

        ;Exit program
        mov eax,1
        int 0x80

segment .bss
        number resb 2

section .data
        limit equ 58
        num2 db '1'
        space db ' '
        newline db 0xa

```
