## Flowchart
![Arithmetic](https://github.com/suddy00/CISC_211_Assembly/assets/17439019/fa7a2c3e-e852-487c-9cde-469f1dd73973)

## Challenges
- The size of the registry used for values can cause the program to skip program steps.

```assembly
section .text

	;Declaring constants
	SYS_EXIT  equ 1

	global _start


_start:
;1
	mov eax, -var1			;eax = -var1 (2)
	mov dl,10			;move 10 into dl
	imul dl				;multipy eax(-2) by dl(10)
	mov [result],eax

;2
	add ebx, var1			;adding all variables to eax
	add ebx, var2
	add ebx, var3
	add ebx, var4
	mov [result], ebx		;storing added variables to result

;3
	mov eax, -var1			;eax = -var1 (2)
	mov dl, var2			;move var2(5) to dl
	imul dl				;multipy eax(-2) by dl (5)
	add eax, var3			;add var3(7) to eax(-10)
	mov [result], eax
;4
	mov eax, var1			;mov var1(2) to eax
	mov dl,2			;move 2 to dl
	mul dl				;divide eax(2) by dl(2)

	mov cl, var2			;move var2(5) to edx
	sub cl, 3			;subtract 3 from edx(5)
	mov bl, cl			;move edx(2) to bl
;	idiv ebx			;divide eax(4) by bl (2)
	mov [result], eax

  	mov  eax, SYS_EXIT		;system call number (sys_exit)
   	int  0x80                   	;call kernel

section .bss
		;using this space for uninitialized variable (result)
	result resw 1

section .data
		;using this space for initiallized variables (var)
	var1 equ 2
	var2 equ 5
	var3 equ 7
	var4 equ 10


```
