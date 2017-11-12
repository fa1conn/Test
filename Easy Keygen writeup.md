1.运行程序发现要输入name和serial.  
2.打开IDA生成idb文件，找到字符串input name![image](F:\piccture\001.png)
3.F5后代码如下
```
int __cdecl main(int argc, const char **argv, const char **envp)
{
  signed int v3; // ebp@1
  signed int i; // esi@1
  int result; // eax@6
  int v6; // [sp+0h] [bp-13Ch]@0
  int v7; // [sp+0h] [bp-13Ch]@1
  char v8; // [sp+Ch] [bp-130h]@1
  char v9; // [sp+Dh] [bp-12Fh]@1
  char v10; // [sp+Eh] [bp-12Eh]@1
  char v11; // [sp+10h] [bp-12Ch]@1
  char v12; // [sp+11h] [bp-12Bh]@1
  __int16 v13; // [sp+71h] [bp-CBh]@1
  char v14; // [sp+73h] [bp-C9h]@1
  char v15; // [sp+74h] [bp-C8h]@1
  char v16; // [sp+75h] [bp-C7h]@1
  __int16 v17; // [sp+139h] [bp-3h]@1
  char v18; // [sp+13Bh] [bp-1h]@1

  v11 = 0;
  v15 = 0;
  memset(&v12, 0, 0x60u);
  v13 = 0;
  v14 = 0;
  memset(&v16, 0, 0xC4u);
  v17 = 0;
  v18 = 0;
  v8 = 16;
  v9 = 32;
  v10 = 48;
  sub_4011B9(aInputName, v6);
  scanf(aS, &v11);
  v3 = 0;
  for ( i = 0; v3 < strlen(&v11); ++i )
  {
    if ( i >= 3 )
      i = 0;
    sprintf(&v15, aS02x, &v15, *(&v11 + v3++) ^ *(&v8 + i));
  }
  memset(&v11, 0, 'd');
  sub_4011B9(aInputSerial, v7);
  scanf(aS, &v11);
  if ( !strcmp(&v11, &v15) )
  {
    sub_4011B9(aCorrect, *&v8);
    result = 0;
  }
  else
  {
    sub_4011B9(aWrong, *&v8);
    result = 0;
  }
  return result;
}
```
4.*(&v11 + v3++)其实是一个数组，每次递增1，而 *(&v8 + i) 则是将每次的v8的地址加1后取该地址的值。![image](F:\piccture\002.png)![image](F:\piccture\003.png)发现v8，v9，v10是连续的，因此取值依次取16，32，48  
5.程序大概如下：先键入v11，然后依次与16，32，48异或，依次循环，之后再与v15比较，结果为0则表示正确。v15应该就是题目给出的serial
6.写c程序
```
#include<stdio.h>
int main()
{
	int i=0;
	int v8;
	int v15[8];
	int a=0,b=0;
	
	for(;a<8;a++){
		scanf("%x",&v15[a]);
	}
	for(;b<8;b++){
		i=i%3;
		if(i==0){
			v8=16;
		}
		else if(i==1){
			v8=32;
		}
		else {
			v8=48;
		}

		for(int flag=0;flag<127;flag++){
			if((flag^v8)==v15[b]){
				printf("%c",flag);
			}
		
		}
		i++;
	}
return 0;

}
```
结果为K3yg3nm3