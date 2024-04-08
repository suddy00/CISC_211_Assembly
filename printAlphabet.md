```assembly
section .text
        global _start
_start:
        mov eax,65

runloop:
        mov [res], eax
        mov ecx, res
        call output

        mov eax, [res]
        inc eax
        cmp eax, 91
        jl runloop

        call exit

output:
        mov edx,1       ;output length
        mov ebx,1       ;stdout
        mov eax,4       ;system call (sys_write)
        int 0x80        ;interrupt kernel
        ret

exit:
        mov eax,1
        int 0x80

segment .bss
        res resb 1

```
