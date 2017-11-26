1.```chmod +x lab1C```获取运行的权限。  
2.```./lablC```运行程序。需要输入一个password。  
3.我的命令与void有点不同  
```gdb```  
```disas main```直接反汇编main函数部分，不汇编整个程序  
4. 
```
   0x080486ad <+0>:	push   ebp
   0x080486ae <+1>:	mov    ebp,esp
   0x080486b0 <+3>:	and    esp,0xfffffff0
   0x080486b3 <+6>:	sub    esp,0x20
   0x080486b6 <+9>:	mov    DWORD PTR [esp],0x80487d0
   0x080486bd <+16>:	call   0x8048560 <puts@plt>
   0x080486c2 <+21>:	mov    DWORD PTR [esp],0x80487ee
   0x080486c9 <+28>:	call   0x8048560 <puts@plt>
   0x080486ce <+33>:	mov    DWORD PTR [esp],0x80487d0
   0x080486d5 <+40>:	call   0x8048560 <puts@plt>
   0x080486da <+45>:	mov    DWORD PTR [esp],0x804880c
   0x080486e1 <+52>:	call   0x8048550 <printf@plt>
   0x080486e6 <+57>:	lea    eax,[esp+0x1c]
   0x080486ea <+61>:	mov    DWORD PTR [esp+0x4],eax
   0x080486ee <+65>:	mov    DWORD PTR [esp],0x8048818
   0x080486f5 <+72>:	call   0x80485a0 <__isoc99_scanf@plt>
   0x080486fa <+77>:	mov    eax,DWORD PTR [esp+0x1c]
   0x080486fe <+81>:	cmp    eax,0x149a
   0x08048703 <+86>:	jne    0x8048724 <main+119>
   0x08048705 <+88>:	mov    DWORD PTR [esp],0x804881b
   0x0804870c <+95>:	call   0x8048560 <puts@plt>
   0x08048711 <+100>:	mov    DWORD PTR [esp],0x804882b
   0x08048718 <+107>:	call   0x8048570 <system@plt>
   0x0804871d <+112>:	mov    eax,0x0
   0x08048722 <+117>:	jmp    0x8048735 <main+136>
   0x08048724 <+119>:	mov    DWORD PTR [esp],0x8048833
   0x0804872b <+126>:	call   0x8048560 <puts@plt>
   0x08048730 <+131>:	mov    eax,0x1
   0x08048735 <+136>:	leave  
   0x08048736 <+137>:	ret
   ```
5.```0x080486f5```处调用scanf函数，下面是cmp比较，不等跳转，查看0x8048833处的值```x/20c 0x8048833```
```
0x8048833:	10 '\n'	73 'I'	110 'n'	118 'v'	97 'a'	108 'l'	105 'i'	100 'd'
0x804883b:	32 ' '	80 'P'	97 'a'	115 's'	115 's'	119 'w'	111 'o'	114 'r'
0x8048843:	100 'd'	33 '!'	33 '!'	33 '!'
```
Invalid Password!!!好了此处凉凉，system那才是正确的路线

void的Python我看不懂，我的Python处于刚接触，只会写```print int(0x149a)```



