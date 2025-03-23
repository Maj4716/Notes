# 第3章 MATLAB程序设计

## 3.1 M文件

定义函数

```matlab
function [输出形参] = 函数名(输入形参)
% 紧接函数定义语句后的一行注释是H1帮助行，可以用lookup搜索出
% 紧接H1行的注释是帮助文本，可以用help搜索
function [da,a2,inva,traa] = comp4(x)
da = det(x);
a2 = x^2;
inva = inv(x);
traa = x';

[a,b,c,d] = comp4(A)
```

在函数M文件内部声明并使用的变量都是全局变量，和MATLAB工作区中同名变量存储位置不同，是完全不同的变量。除了返回值，被调用函数不改变工作区其他变量的值。

全局变量`global var1 var2`，一般使用大写字母定义全局变量。

永久变量`persistent var1 var2`，只有该变量从属的函数能够访问该变量，当函数运行结束时，永久变量保存在内存中，下次调用该函数时可以再次使用永久变量。

内联函数

```matlab
f = incline('sin(x)+sin(x)^2')
a = y(pi/4)
```

格式化输出`fprintf(format,data)`

<img src="./Images/第3章 MATLAB程序设计/图 3.2.png" alt="图 3.2" style="zoom:50%;" />

## 3.2 数据的输入和输出

```matlab
x = input(prompt)
x = input(prompt,'s')	%字符串
disp(a)
formatSpec = 'X is %3.2f meters or %8.3f mm\n';
fprintf(formatSpec,A1,A2)
pause					%暂停程序，单机任意键后继续
pause(n)				%n秒后继续执行
pause on				%显示并执行pause
pause off				%显示但不执行
```

## 3.3 程序控制结构

**分支结构**

```matlab
% 单分支if
if condition
	sentence
end
----------------------------------
% 双分支
if condition
	sentence_1
else
	sentence_2
end
----------------------------------
% 多分支
if condition_1
	sentence_1
elseif condition_2
	sentence_2
…………
elseif condition_n
	sentence_n
else
	sentence_n+1
end
---------------------------------
% switch语句
switch scalar or string
	case value_1
		sentence_1
	case value_2
		sentence_2
	…………
	case value_n
		sentence_n
	otherwise
		sentence_n+1
end
-------------------------------
% try语句
try
	sentence
catch
	sentence_if_error
end
% 错误信息储存在lasterr变量中
```

**循环结构**

```matlab 
% for循环
for i = start:step:end
	sentence
end
-------------------------------
% while循环
while condition
	sentence
end
------------------------------
% break结束本层循环执行end下面的语句
% continue结束当前循环进入下一个循环
```

## 3.4 程序调试

<img src="./Images/第3章 MATLAB程序设计/图 3.1.png" alt="图 3.1" style="zoom:50%;" />
