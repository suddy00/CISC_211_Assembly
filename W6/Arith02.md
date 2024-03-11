```assembly
section .text

        global _start

_start:
        mov eax,a       ;puts a value in eax
        mov dl, b       ;buts b value in dl
        mul dl          ;multiply a x b store in eax
        mov [result], eax ;store result in result

        mov eax,c       ;mov c value to eax
        mov dl,d        ;mov d value to dl
        mul dl          ;mul c by d store in eax

        add eax, [result] ;add eax and result
        mov [result], eax ;store in result

        jmp exit        ;exit

exit:
        mov eax,1
        int 0x80

segment .bss
        result resb 1


section .data
        a equ 1
        b equ 2
        c equ 3
        d equ 4
```
