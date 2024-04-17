# Challenges
  The increment values are also incrementing the filename string being used to desinate the file as .txt 

```assembly
section .text
        global _start
_start:
        mov edx, 5
        mov eax, [filename]
        mov [newname], eax
body:
        mov eax, [filename]             ;'.txt'
        mov [newname], edx      ;places incrementing file name in newname
        add [newname], eax      ;add '.txt' to newname
        dec edx

        mov     ecx, 0744o ; set all permissions to read, write, execute (oct>
        mov     ebx, newname       ; filename we will create
        mov     eax, 8              ; invoke SYS_CREAT (kernel opcode 8)
        int     0x80                ; call the kernel

        cmp edx, 0
        jg body

        mov     eax,1
        int     0x80

SECTION .data
filename db '.txt'    ; the filename to create

SEGMENT .bss
        newname resb 2
```
