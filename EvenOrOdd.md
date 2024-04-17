# Challenges
 - Every printed line requires a space allocation in edx.
 - For the least opportunity for error, each print using a different output should have it's own edx

```assembly
section .text
        global _start

_start:
        mov eax, [num]
        and eax, 1
        jz _evn                 ;jump to evnn block when 0
        jnz _odd

_evn:
        mov ecx, evn
        jmp _print

_odd:
        mov ecx, odd
        jmp _print

_print:

        mov eax, 4
        mov ebx, 1
        mov edx, len2
        int 0x80

        mov eax, 1
        int 0x80

section .data
        num dd 20

        evn db 'even', 0xA, 0xD
        odd db 'odd' , 0xA, 0xD

;       len equ $ - evn   ;;Using this length results in additional output, when printing 'odd' perhaps because it has occupied space
        len2 equ $ - odd
```
