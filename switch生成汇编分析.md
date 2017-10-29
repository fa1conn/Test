```
#include<stdio.h>
int main()
{
	int a=10;
	switch(a){
		case 20:
			a=10;
		case 30:
			a=10;
		case 10:
			a=20;
	}
	printf("%d",a);
}
```
```
.file	"016.c"
	.intel_syntax
	.def	___main;	.scl	2;	.type	32;	.endef
	.section .rdata,"dr"
LC0:
	.ascii "%d\0"
	.text
	.align 2
.globl _main
	.def	_main;	.scl	2;	.type	32;	.endef
_main:
	push	ebp
	mov	ebp, esp
	sub	esp, 24
	and	esp, -16
	mov	eax, 0
	add	eax, 15
	add	eax, 15
	shr	eax, 4
	sal	eax, 4
	mov	DWORD PTR [ebp-12], eax
	mov	eax, DWORD PTR [ebp-12]
	call	__alloca
	call	___main
	mov	DWORD PTR [ebp-4], 10           ;将10传入[ebp-4]
	mov	eax, DWORD PTR [ebp-4]          ；将[ebp-4]传入eax
	mov	DWORD PTR [ebp-8], eax          ；将eax=10传入[ebp-8]
	cmp	DWORD PTR [ebp-8], 20           ；将[ebp-8]与20比较
	je	L3                              ；相等则跳转至L3
	cmp	DWORD PTR [ebp-8], 20           ；将[ebp-8]与20比较
	jg	L6                              ；大于则跳转至L6
	cmp	DWORD PTR [ebp-8], 10           ；将[ebp-8]与10相比
	je	L5                              ；相等则跳转至L5
	jmp	L2                              ；跳转至L2
L6:
	cmp	DWORD PTR [ebp-8], 30           ；将[ebp-8]与30比较
	je	L4                              ；等于则跳转至L4
	jmp	L2                              ；跳转至L2
L3:
	mov	DWORD PTR [ebp-4], 10           ；将10传给[ebp-4]
L4:
	mov	DWORD PTR [ebp-4], 10           ;将10传给[ebp-4]
L5:
	mov	DWORD PTR [ebp-4], 20           ；将20传给[ebp-4]
L2:
	mov	eax, DWORD PTR [ebp-4]          ；将[ebp-4]传给eax
	mov	DWORD PTR [esp+4], eax
	mov	DWORD PTR [esp], OFFSET FLAT:LC0
	call	_printf                     ；打印eax
	mov	eax, 0
	leave
	ret
	.def	_printf;	.scl	2;	.type	32;	.endef
```