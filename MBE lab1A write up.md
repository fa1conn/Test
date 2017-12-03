1.和lab1B一个套路，修改sp后，F5出伪代码
2.
```
int __cdecl main(int argc, const char **argv, const char **envp)
{
  int v4; // [esp+1Ch] [ebp-24h]
  char s; // [esp+20h] [ebp-20h]
  unsigned int v6; // [esp+3Ch] [ebp-4h]

  v6 = __readgsdword(0x14u);
  puts(".---------------------------.");
  puts("|---------  RPISEC  --------|");
  puts("|+ SECURE LOGIN SYS v. 3.0 +|");
  puts("|---------------------------|");
  puts("|~- Enter your Username:  ~-|");
  puts("'---------------------------'");
  fgets(&s, 32, stdin);
  puts(".---------------------------.");
  puts("| !! NEW ACCOUNT DETECTED !!|");
  puts("|---------------------------|");
  puts("|~- Input your serial:    ~-|");
  puts("'---------------------------'");
  __isoc99_scanf(&unk_8048D00, &v4);
  if ( auth(&s, v4) )
    return 1;
  puts("Authenticated!");
  system("/bin/sh");
  return 0;
}
```
可以看出用户输入s，也就是username，auth(&s, v4)结果为0，才会执行puts，此时程序才会运行成功，进入auth函数
```
_BOOL4 __cdecl auth(char *username, int a2)
{
  _BOOL4 result; // eax
  int i; // [esp+14h] [ebp-14h]
  int v4; // [esp+18h] [ebp-10h]
  int len; // [esp+1Ch] [ebp-Ch]

  username[strcspn(username, "\n")] = 0;
  len = strnlen(username, 32);
  if ( len <= 5 )
    return 1;
  if ( ptrace(0, 0, 1, 0) == -1 )
  {
    puts("\x1B[32m.---------------------------.");
    puts("\x1B[31m| !! TAMPERING DETECTED !!  |");
    puts("\x1B[32m'---------------------------'");
    result = 1;
  }
  else
  {
    v4 = (username[3] ^ 0x1337) + 6221293;
    for ( i = 0; i < len; ++i )
    {
      if ( username[i] <= 31 )
        return 1;
      v4 += (v4 ^ username[i]) % 0x539;
    }
    result = a2 != v4;
  }
  return result;
}
```
改动了点数组名，变量名使代码清楚明了。要返回0，只能执行else部分，当a2=v4时（此时a2是用户输入的序列号），v4是程序验证的序列号。算法在伪代码中已经很清楚了，写个脚本
```
def foo(username):
	v4=(ord(username[3])^0x1337)+6221293
	len1=len(username)
	for i in range(len1):
		v4 += (v4^ord(username[i])) % 0x539
	return v4

serial=foo("fa1con")
print serial
```