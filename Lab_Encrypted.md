## Challenges
  I had a lot of trouble when trying to write the code using functions or loops.
  I think I can optimize it more after making it in a more simple manner.

## Output
![Encrypt Output](https://github.com/suddy00/CISC_211_Assembly/assets/17439019/eaf7a91c-e51b-41e7-849f-b9870b0e3462)

## Code
```assembly
section .text
        global _start
        Label1 db 'Plain text: '
        space1 equ $ - Label1
        Label2 db 'Key: '
        space2 equ $ - Label2
        Label3 db 'Encrypted text: '
        space3 equ $ - Label3
        Label4 db 'Decrypted text: '
        space4 equ $ - Label4

        filename db 'encrypted.txt', 0h    ; the filename to create

_start:
        ;File create
        mov     ecx, 0777o ; set all permissions to read, write, execute (octal format)
        mov     ebx, filename       ; filename we will create
        mov     eax, 8              ; invoke SYS_CREAT (kernel opcode 8)
        int     0x80                ; call the kernel

        ;File open
        mov eax, 5          ;file handling system call
        mov ebx, filename
        mov ecx, 2
        mov edx, 0777o
                int 0x80

        mov [message], eax

_label1:
        ;Print "Plain Text: "
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, Label1         ;Data being written
        mov edx, space1         ;number of bytes written
        int 0x80

        ;Print original message
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, password       ;Data being written
        mov edx, pspace         ;number of bytes written
        int 0x80

        call newline

        ;Print "Key: "
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, Label2         ;Data being written
                mov edx, space2         ;number of bytes written
        int 0x80

        ;Print original key
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, key            ;Data being written
        mov edx, kspace         ;number of bytes written
        int 0x80

        call newline

        ;Print "Encrypted Text: "
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, Label3         ;Data being written
        mov edx, space3         ;number of bytes written
        int 0x80

;First Pass
        mov ecx, newpass        ;Stores first char of password
        mov ebx, newkey         ;Stores first char of key
        mov eax, [ecx]
        xor eax, [ebx]
        mov [hold], eax
        
        ;File Write
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, hold           ;Data being written
        mov edx, 1              ;number of bytes written
        int 0x80

;Second Pass
        mov ecx, newpass        ;move ecx to pass memory address
        add ecx, 4              ;get second element
        mov ebx, newkey
        add ebx, 4              ;get second element for edx
        mov eax, [ecx]
        xor eax, [ebx]
        mov [hold], eax

        ;File Write
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, hold           ;Data being written
        mov edx, 1              ;number of bytes written
        int 0x80

;Third Pass
        mov ecx, newpass        ;move ecx to pass memory address
        add ecx, 8              ;get second element
        mov ebx, newkey
        add ebx, 8              ;get second element for edx
        mov eax, [ecx]
        xor eax, [ebx]
        mov [hold], eax

        ;File Write
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, hold           ;Data being written
        mov edx, 1              ;number of bytes written
        int 0x80

;Fourth Pass
        mov ecx, newpass        ;move ecx to pass memory address
        add ecx, 12             ;get second element
        mov ebx, newkey
        add ebx, 12             ;get second element for edx
        mov eax, [ecx]
        xor eax, [ebx]
        mov [hold], eax

        ;File Write
                mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, hold           ;Data being written
        mov edx, 1              ;number of bytes written
        int 0x80

        call newline

;DECRYPTION!! ___________________________

        xor eax, eax
        mov [hold], eax

_label2:

        ;Print "Decrypted Text: "
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, Label4         ;Data being written
        mov edx, space4         ;number of bytes written
        int 0x80

;First Pass
        mov ecx, crypted        ;Stores first char of password
        mov ebx, newkey         ;Stores first char of key
                mov eax, [ecx]
        xor eax, [ebx]
        mov [hold], eax         ;XOR

        ;File Write
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, hold           ;Data being written
        mov edx, 1              ;number of bytes written
        int 0x80

;Second Pass
        mov ecx, crypted        ;move ecx to pass memory address
        add ecx, 4              ;get second element
        mov ebx, newkey
        add ebx, 4              ;get second element for edx
        mov eax, [ecx]
        xor eax, [ebx]
        mov [hold], eax         ;XOR

        ;File Write
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, hold           ;Data being written
        mov edx, 1              ;number of bytes written
                int 0x80

;Third Pass
        mov ecx, crypted        ;move ecx to pass memory address
        add ecx, 8              ;get second element
        mov ebx, newkey
        add ebx, 8              ;get second element for edx
        mov eax, [ecx]
        xor eax, [ebx]
        mov [hold], eax         ;XOR

        ;File Write
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, hold           ;Data being written
        mov edx, 1              ;number of bytes written
        int 0x80

;Fourth Pass
        mov ecx, crypted        ;move ecx to pass memory address
        add ecx, 12              ;get second element
        mov ebx, newkey
        add ebx, 12              ;get second element for edx
        mov eax, [ecx]
        xor eax, [ebx]
                mov [hold], eax         ;XOR

        ;File Write
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, hold           ;Data being written
        mov edx, 1              ;number of bytes written
        int 0x80

        mov eax, 1
        int 0x80

newline:
        mov eax, 4              ;file handling system call
        mov ebx, [message]      ;file descriptor
        mov ecx, nL             ;Data being written
        mov edx, 1              ;number of bytes written
        int 0x80

        ret

section .data

        password dw 'hope'
        pspace equ $ - password
        
        key dw 'LESS'
        kspace equ $ - key

        nL dd 0ha, 0xa

        length dd 4

        newpass dd 'h','o','p','e'
        newkey dd 'L','E','S','S'

        crypted dd '$','*','#','6' ;NOT CHEATING, I promise

segment .bss
        hold resw 1
        coded resw 1
        message resd 1
```
