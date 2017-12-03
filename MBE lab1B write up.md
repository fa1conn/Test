1.调整堆栈平衡，参考 https://bbs.pediy.com/thread-158896.htm  
2.接着F5大法就可以使用了
```
int __cdecl main(int argc, const char **argv, const char **envp)
{
  unsigned int v3; // eax@1
  int savedregs; // [sp+20h] [bp+0h]@1

  v3 = time(0);
  srand(v3);
  puts(".---------------------------.");
  puts("|-- RPISEC - CrackMe v2.0 --|");
  puts("'---------------------------'");
  printf("\nPassword: ");
  __isoc99_scanf("%d", &savedregs);
  test(savedregs, 322424845);
  return 0;
}
```
看到有个测试函数test，点进去  
3.
```
int __cdecl test(int a1, int a2)
{
  int result; // eax@2
  char v3; // al@23
  char v4; // [sp+1Ch] [bp-Ch]@1

  v4 = a2 - a1;
  switch ( a2 - a1 )
  {
    case 1:
      result = decrypt(v4);
      break;
    case 2:
      result = decrypt(v4);
      break;
    case 3:
      result = decrypt(v4);
      break;
    case 4:
      result = decrypt(v4);
      break;
    case 5:
      result = decrypt(v4);
      break;
    case 6:
      result = decrypt(v4);
      break;
    case 7:
      result = decrypt(v4);
      break;
    case 8:
      result = decrypt(v4);
      break;
    case 9:
      result = decrypt(v4);
      break;
    case 10:
      result = decrypt(v4);
      break;
    case 11:
      result = decrypt(v4);
      break;
    case 12:
      result = decrypt(v4);
      break;
    case 13:
      result = decrypt(v4);
      break;
    case 14:
      result = decrypt(v4);
      break;
    case 15:
      result = decrypt(v4);
      break;
    case 16:
      result = decrypt(v4);
      break;
    case 17:
      result = decrypt(v4);
      break;
    case 18:
      result = decrypt(v4);
      break;
    case 19:
      result = decrypt(v4);
      break;
    case 20:
      result = decrypt(v4);
      break;
    case 21:
      result = decrypt(v4);
      break;
    default:
      v3 = rand();
      result = decrypt(v3);
      break;
  }
  return result;
}
```
发现是322424845-savedregs并赋值给v4并进行选择跳转
4.进入decrypt函数
```
int __cdecl decrypt(char a1)
{
  size_t i; // [sp+10h] [bp-28h]@1
  size_t v3; // [sp+14h] [bp-24h]@1
  char s[4]; // [sp+1Bh] [bp-1Dh]@1
  int v5; // [sp+2Ch] [bp-Ch]@1

  v5 = *MK_FP(__GS__, 20);
  strcpy(s, "Q}|u`sfg~sf{}|a3");
  v3 = strlen(s);
  for ( i = 0; i < v3; ++i )
    s[i] ^= a1;
  if ( !strcmp(s, "Congratulations!") )
    system("/bin/sh");
  else
    puts("\nInvalid Password!");
  return *MK_FP(__GS__, 20) ^ v5;
}
```
s与v4异或结果为Congratulations!就成功了。
异或Q与C可得18，所以最终结果是322424845-18=322424827
