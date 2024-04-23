# Thoughts
  The loop instruction will loop for the value in the ECX register, decrementing the value with each iteration. 

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

Highest in Array
```assembly
section .text
        global _start

_start:
        mov eax, 3       ;array length
        mov ebx, 0       ;initializing  ebx 0
        mov ecx, array   ;move array's address from the memory to the register
                        ;the array address is equal to the address of
                        ;the first element

higher:
        mov edx, ebx    ;storing the highest value in edx
top:
        mov ebx, [ecx]   ;add content of the array's first element with the ebx
        add ecx, 4       ;fetch the next element in the array which is 4 bytes away


        mov [number], ebx


        dec eax         ;eax will work as a counter which is equal to the
                        ;array length

        push eax

        cmp ebx, edx    ;jump to update largest if necessary
        jg higher

        pop eax
        cmp eax, 0
        jg top         ;jump not zero to the label top

        mov [high], edx

        mov eax, 1
        int 0x80

segment .bss
        number resb 1
        high resb 1

section .data
        array dd 5,10,7        ;size double data 4 bytes
```
