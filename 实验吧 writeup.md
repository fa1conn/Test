## 1000000
link: http://ctf5.shiyanbar.com/423/re/reverse3.exe  
1.PEID检查发现没壳。
2.搜索字符串发现good，点击进入该代码区。![image](http://ww3.sinaimg.cn/large/0060lm7Tly1flm0xnn8ruj311y0lcwhg.jpg)![image](http://ww2.sinaimg.cn/large/0060lm7Tly1flm0ydecs3j311y0lcdiw.jpg)
3.F5反汇编出代码
```
int __cdecl main(int argc, const char **argv, const char **envp)
{
  char v4; // [sp+14h] [bp-34h]@1
  unsigned __int8 v5; // [sp+15h] [bp-33h]@1
  unsigned __int8 v6; // [sp+16h] [bp-32h]@1
  unsigned __int8 v7; // [sp+17h] [bp-31h]@1
  unsigned __int8 v8; // [sp+18h] [bp-30h]@1
  unsigned __int8 v9; // [sp+19h] [bp-2Fh]@1
  unsigned __int8 v10; // [sp+1Ah] [bp-2Eh]@1
  unsigned __int8 v11; // [sp+1Bh] [bp-2Dh]@1
  unsigned __int8 v12; // [sp+1Ch] [bp-2Ch]@1
  unsigned __int8 v13; // [sp+1Dh] [bp-2Bh]@1
  unsigned __int8 v14; // [sp+1Eh] [bp-2Ah]@1
  unsigned __int8 v15; // [sp+1Fh] [bp-29h]@1
  unsigned __int8 v16; // [sp+20h] [bp-28h]@1
  char Str1[4]; // [sp+28h] [bp-20h]@1
  char v18; // [sp+2Ch] [bp-1Ch]@1
  int v19; // [sp+3Ch] [bp-Ch]@1

  __main();
  *Str1 = 0;
  memset(&v18, 0, 0x10u);
  memset(&v4, 0, 0x14u);
  v4 = 0xE6u;
  v5 = 0xECu;
  v6 = 0xE1u;
  v7 = 0xE7u;
  v8 = 0xBAu;
  v9 = 0xF4u;
  v10 = 0xE5u;
  v11 = 0xF3u;
  v12 = 0xF4u;
  v13 = 0xF4u;
  v14 = 0xE5u;
  v15 = 0xF3u;
  v16 = 0xF4u;
  v19 = 0;
  puts("喵?");
  scanf("%s", Str1);
  LOBYTE(v19) = 0;
  while ( Str1[v19] )
  {
    Str1[v19] |= 0x80u;
    ++v19;
  }
  if ( !strcmp(Str1, &v4) )
    printf("good");
  else
    printf("wrong");
  return 0;
}
```
你输入的str1与0x80异或得到的值与v4-v16相等即可因此写程序。
```
#include<stdio.h>
int main()
{
	int c[13]={0xE6,0xEC,0xE1,0xE7,0xBA,0xF4,0xE5,0xF3,0xF4,0xF4,0xE5,0xF3,0xF4};
	int i,y;
	for(i=0;i<13;i++){
		for(y=0;y<128;y++){
			if(c[i]==(y^0x80)) {
				printf("%c",y);
				break;
			}
		}
	}
}
```
值得一提的是异或那个等式又忘记加括号！！！
最近学了Python,写段python
```
a=[0xE6,0xEC,0xE1,0xE7,0xBA,0xF4,0xE5,0xF3,0xF4,0xF4,0xE5,0xF3,0xF4]
flag=''
for i in a:
    flag+=chr(i^0x80)
print flag
```
