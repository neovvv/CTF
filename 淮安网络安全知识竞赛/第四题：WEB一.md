#第四题：WEB一

显示信息如下
|ID|Note|Author|
|-|-|-|
|1|Hello world|admin|

应该是sql注入

尝试访问http://101.37.25.214:8002/index.php?id=2，显示：

|ID|	Note	|Author|
|-|-|-|
|2	|SQL injection is a critical vulnerability	|admin|

确定是sql注入

###方法一：手动注入

###方法二：sqlmap注入
