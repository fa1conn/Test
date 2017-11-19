1.它是二进制文件，直接拖进IDA分析  
2.搜索字符串，发现correct![image](http://ww2.sinaimg.cn/large/0060lm7Tly1fln57z5ipgj311y0lcgo1.jpg)
3.F5后发现wrong...再看上面那个if语句，点进去发现correct![image](http://ww3.sinaimg.cn/large/0060lm7Tly1fln59vyx73j311y0lc40x.jpg)![image](http://ww3.sinaimg.cn/large/0060lm7Tly1fln5acmv03j311y0lcgnw.jpg)
4.点击进入if判断条件进行分析，发现非常简单。![image](http://ww3.sinaimg.cn/large/0060lm7Tly1fln5by6i4tj311y0lc40z.jpg)
5.写代码运算得flag
```
i=[120^0x34,49,124^0x32,0x88^0xDD,88]
flag=''
for a in i:
	flag+=chr(a)

print flag
```
