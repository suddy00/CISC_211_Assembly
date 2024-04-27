# Challenges
  Mostly finding documentation that explained well how Sys_sleek worked
  The newline should be placed in the at the beginning of the content or at the end of the previous input
  It's easy to overcomplicate this exercise if you have it do too many tasks.
  
```assembly
SECTION .data
        filename db 'quotes.txt', 0h    ; the filename to create
        contents db 'Better three hours too soon than a minute too late.', 0xa, 'No legacy is so rich as honesty. 0xa', 0h
        size dd 84

SECTION .text
        global  _start

_start:
        ;file open operation
        ;assuming that the file has already been created.
        ;If the readme.txt file is not created, then create a file
        ;using the example above.
        mov eax, 5          ;file handling system call
        mov ebx, filename
        mov ecx, 2
        mov edx, 0777o
        int 0x80

        mov [f_data], eax

        ;Sys_lseek
        mov eax, 19             ;file handling system call
        mov ebx, [f_data]       ;file descriptor
        mov ecx, 0              ;No offset
        mov edx, 2              ;Start input at end of file

        int 0x80

        ;file write operation
        mov eax, 4              ;file handling system call
        mov ebx, [f_data]       ;file descriptor
        mov ecx, contents       ;Data being written
        mov edx, size           ;number of bytes written
        int 0x80

        ;file close
        mov eax, 6
        mov ebx, [f_data]
        int 0x80

        mov eax, 1
        int 0x80

section .bss
        f_data resw 1
```
