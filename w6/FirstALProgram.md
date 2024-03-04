
```assembly
section .text

;Declaring constants
SYS_EXIT  equ 1
SYS_WRITE equ 4
STDIN     equ 0
STDOUT    equ 1
section  .text

   global _start                ;must be declared for linker (ld)
                                ;global is used to export the _start label. 
                                ;This will be the entry point to the program. 

_start:                         ;tells linker entry point

   mov  eax, SYS_WRITE          ;system call number (sys_write)
   mov  ebx, STDOUT             ;file descriptor (stdout)
   mov  ecx,msg1                ;message to write, A pointer to the variable 'msg'
   mov  edx,len1                ;message #1 length
   int  0x80                    ;call kernel


   mov  eax, SYS_WRITE          ;system call number (sys_write)
   mov  ebx, STDOUT             ;file descriptor (stdout)
   mov  ecx,msg2                ;message to write, A pointer to the variable 'msg'
   mov  edx,len2                ;message #2 length

mov  eax, SYS_WRITE          ;system call number (sys_write)
   mov  ebx, STDOUT             ;file descriptor (stdout)
   mov  ecx,msg3                ;message to write, A pointer to the variable 'msg'
   mov  edx,len3                ;message #3 length
   int  0x80                    ;call kernel

   mov  eax, SYS_EXIT           ;system call number (sys_exit)
   int  0x80                    ;call kernel


section .data

                                ;Declare a label "msg" which has 
                                ;our string we want to print. 
                                ;for reference: 0xa = "\n" (line feed) 
                                ;db = define byte
                                ;length of the string
                                ;len" will calculate the current 
                                ;offset minus the "msg" offset.

msg1 db 'I came,', 0xa          ;string1 to be printed
len1 equ $ - msg1

msg2 db 'I saw', 0xa            ;string2 to be printed
len2 equ $ - msg2

msg3 db 'I conquered.', 0xa     ;string3 to be printed
len3 equ $ - msg3

```
