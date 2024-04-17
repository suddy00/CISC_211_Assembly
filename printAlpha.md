# Challenges
  Remembering the output will display as ASCII

```assembly
section .text
        global _start
_start:
        mov eax,65

runloop:
        mov [res], eax
        mov ecx, res    ;Send letter to be printed
        call output

        mov eax, [res]
        inc eax
        cmp eax, 91
        jl runloop

        call exit

output:
        ;Print
        mov edx,1       ;output length
        mov ebx,1       ;stdout
        mov eax,4       ;system call (sys_write)
        int 0x80        ;interrupt kernel

        ;Print newline
        mov edx,1       ;output length
        mov ecx, nL
        mov ebx,1       ;stdout
        mov eax,4       ;system call (sys_write)
        int 0x80        ;interrupt kernel

        ret

exit:
        mov eax,1
        int 0x80

segment .bss
        res resb 1

section .data
        nL db 0xa

```
