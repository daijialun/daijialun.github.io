---
layout: post
title:  "getline和get使用区别"
date:   2015-11-21
categories: C++
---

# C++ getline与get使用区别

参考文章[C++中，get getline gets 用法 ](http://blog.sina.com.cn/s/blog_88feaf0b0100ynnn.html)，[get( )与getline( )区别](http://www.cnblogs.com/qlwy/archive/2011/11/03/2235126.html)

cin.get()遇到'\n'字符后便返回，即数组中存储了输入字符，但是不存储'\n'，'\n'还在输入缓冲区，下次读出的仍是'\n'；而cin.getline()遇到'\n'也返回，但是其会把'\n'从输入缓冲区里移除掉。所以大多数时候，用cin.getline更方便。

**cin.get()保留'\n'，留给下次输入；cin.getline()抛弃'\n'，下次则可正常输入**

## cin

最基本，最常用的方法，输入一个数字；接受一个字符串，遇“空格”，“TAB”与“回车”都结束

（>>符号 会滤掉不可见字符）

输入：jkljkl  jkljkl，输出：jkljkl，即遇空格结束

## cin.get()

1. cin.get( 字符变量名 )可以用来接收字符，`ch=cin.get()`或`cin.get(ch)`，输入：jkljkl，输出：j

2. cin.get( 字符数组名，接收字符数目 )来接收一行字符串，可接受空格

`char a[20]; cin.get(a, 20)` 输入：jkl jkl jkl，输出：jkl jkl jkl；输入：abcabc...abc（输入25个字符），输出：abcabc...abc（接收19个字符 + 1个'\0'）

3. cin.get() 没有参数，主要是用于舍弃输入流中的不需要的字符，或者舍弃回车

### cin.getline()

1. cin.getilne( 字符数组名，数目) 接受字符串，可接受空格并输出

`char m[20]; cin.getline(m, 5)` 接收5个字符到m中，为4个字符 + 一个'\0'

实际上cin.getline()有三个参数：字符数组名，接受个数，结束字符。如果第三个参数省略时，系统默认为'\0'

### getline()

getline() 接收一个字符串，可接收空格并输出，需包含"#include<string>"

`string str; getline(cin, str)` 输入：jkl jkl，输出：jkl jkl；其与cin.getline()类似，但是cin.getline()属于istream流，而getline()属于string流，是不一样的两个函数

### gets()

gets() 接收一个字符串，可接收空格并输出，需包含"#include<string>"

`char m[20]; gets(m)` （不能写成m=gets()）输入：jkl jkl，输出：jkl jkl

gets()与cin.getline()的用法比较相似

### getchar()

getchar() 接受一个字符，需包含"#include<string>"

`char ch; ch=getchar()`（不能写成getchar(ch)，且getchar()是C函数，C++尽量少用）