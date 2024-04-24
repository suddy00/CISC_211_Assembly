SECTION .data
        filename db 'quotes.txt', 0h    ; the filename to create
        contents db 'To be, or not to be, that is the question.', 0xa, 'A fool thinks himself to be wise, but a wise man knows himself t>
        newcontents db 'Better three hours too soon than a minute too late.', 0xa, 'No legacy is so rich as honesty.'

SECTION .text
        global  _start

_start:
        ;file open operation
        ;assuming that the file has already been created.
        ;If the readme.txt file is not created, then crrate a file
        ;using the example above.
        mov eax, 5          ;file handling system call
        mov ebx, filename
        mov ecx, 1
        mov edx, 0777o
        int 0x80

        mov [fd_out], eax

        ;file write operation
        mov eax, 4          ;file handling system call
        mov ebx, [fd_out]   ;file descriptor
        mov ecx, contents
                mov edx, 119         ;number of bytes written
        int 0x80


        mov eax, 1
        int 0x80

section .bss
        fd_out resb 1
