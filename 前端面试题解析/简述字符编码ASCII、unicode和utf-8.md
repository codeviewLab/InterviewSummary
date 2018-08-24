字符编码ASCII、unicode、utf-8
----

1、最早计算机采用8个bit作为一个字节，只有127个字符(大小写英文字母、数字、一些符号)编码到计算机中，为ASCII编码。  

2、一个字节表示各种语言肯定不够，比如中文需要三个字节。unicode可以把所有语言都统一到一套编码中，Unicode编码通常是2个字节。即使英文字母用unicode表示也是用多个字节。用Unicode编码比ASCII编码需要多一倍的存储空间，在存储和传输上就十分不划。  

3、本着节约的精神，出现了把Unicode编码转化为“可变长编码”的UTF-8编码。在utf-8编码中，常用的英文字母被编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节。  

4、现在可以把ASCII编码看成UTF-8的一部分

5、在计算机内存中，统一使用Unicode编码，当需要保存到硬盘或者需要传输的时候，就转换为UTF-8编码。
用记事本编辑的时候，从文件读取的UTF-8字符被转换为Unicode字符到内存里，编辑完成后，保存的时候再把Unicode转换为UTF-8保存到文件：
![](http://orvwtnort.bkt.clouddn.com/201721343/1535073665473.png)
浏览网页的时候，服务器会把动态生成的Unicode内容转换为UTF-8再传输到浏览器：
![](http://orvwtnort.bkt.clouddn.com/201721343/1535073700602.png)

参考文章
---
[字符串和编码](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001431664106267f12e9bef7ee14cf6a8776a479bdec9b9000)
[字符编码笔记：ASCII，Unicode 和 UTF-8](http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html)

