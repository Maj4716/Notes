# 第2章 MATLAB基本运算

```matlab
inf			% 无穷大
nan			% 不等量
nargin		% 函数输入变量数目
nargout		% 函数输出变量数目
```



## 2.1 矩阵运算

**创建矩阵**

```matlab
a = [1 2 3;4 5 6;7 8 9]
b = [1:3;4:6;7:9]
c = [1:2:10]
```

**生成命令**

```matlab
[] 					% 空矩阵
linspace(a,b,c)		% 在ab之间生成c个等差元素
eye(n) 				% n阶单位矩阵
ones(m,n) 			% m×n阶全1矩阵
zeros(m,n) 			% m×n阶全0矩阵
rand(m,n) 			% m×n阶[0,1]随机矩阵
randn(m,n) 			% m×n阶正态分布随机矩阵
magic(n) 			% 创建魔方矩阵
```

**外部读取**

```matlab
load matrix.dat
```

**访问元素**

```matlab
A(i,j) 				% i行j列元素
A(i,:) 				% i行元素
A(:,j) 				% j行元素
A(i,:) = [1,2,……]	%覆写第i行
A(i,:) = []			%删除第i行
A(a:b,c:d) 			% a~b行，c~d列矩阵块
A(:) 				% 所有元素
A(L) 				% 按列遍历第L个元素
sub2ind 			% 全下标计算单下标
ind2sub 			% 单下标计算全下标
```

**矩阵运算**

```matlab
a\b 	% 左除，a^-1b
a/b 	% 右除，ab^-1
a.*b 	% ab对应元素相乘
a.^3 	% 矩阵a的三次方
3.^a 	% 3的a次方
a.^b 	% a的b次方
```

**矩阵函数**

```matlab
[n,m] = size(a) 	% 返回行数和列数
n = length(a) 		% 返回元素个数或行列最大值
[i,j] = find(a==5) 	% 返回满足条件的索引
cat(dim,a,b)		% 在dim维度上拼接，1为行，2为列
					% 如拼接[1]和[2]
					% 参数为1结果为	参数为2结果为
					%[1				[1 2]
					% 2]
vertcat(a,b)		% 纵向拼接，对应cat1
horzcat(a,b)		% 横向拼接，对应cat2
[a;b]				% 对应cat1
[a,b]				% 对应cat2
inv(a) 				% 矩阵求逆
pinv(a) 			% 矩阵伪逆
compan(a)			% 伴随矩阵 
det(a) 				% 行列式
d = eig(a) 			% 特征值
[V,D] = eig(a) 		% 特征值与特征向量
rank(a) 			% 秩
trace(a) 			% 迹
a' 					% 转置
sqrt(a) 			% 开方
orth(a) 			% 正交化
reshape(a,m,n)		% 变为m×n维
flipud(a)			% 上下翻转
pliplr(a)			% 左右翻转
rot90(a,k)			% 逆时针翻转k×90°
diag(a)				% 提取对角元素返回列向量
diag(v)				% 以列向量v作对角元素创建对角矩阵
X = diag(v,k)		% 将向量v写入矩阵X的主对角线
					% 其他元素都为0，k表示上移行数
v = diag(X,k)		% 从矩阵X提取对角线元素到v
					% k表示上移行数
triu/tril(a)		% 提取上/下三角矩阵
```

## 2.2 数值运算

<img src="./Images/第2章 MATLAB基本运算/图 2.1.png" alt="图 2.1" style="zoom:45%;" />

<img src="./Images/第2章 MATLAB基本运算/图 2.2.png" alt="图 2.2" style="zoom:50%;" />

<img src="./Images/第2章 MATLAB基本运算/图 2.3.png" alt="图 2.3" style="zoom:50%;" />

<img src="./Images/第2章 MATLAB基本运算/图 2.4.png" alt="图 2.4" style="zoom:50%;" />

<img src="./Images/第2章 MATLAB基本运算/图 2.5.png" alt="图 2.5" style="zoom:50%;" />

```matlab
k = polyder(p)			% 求多项式p的微分
k = polyder(a,b)		% 求多项式ab乘积的微分
[q,d] = polyder(a,b)	% 求多项式ab商的导数
						% 分子存入q，分母存入d
q = polyint(p,k)		% 返回多项式p的积分，常数项为k
q = polyint(p)			% 返回多项式p的积分，常数项为0
y = polyval(p,x)		% 将x的值带入多项式p
y = polyval(p,A)		% 将矩阵A的值分别代入p
y = polyvalm(p,A)		% 要求X为方阵，以方阵为自变量求多项式值，a*A*A+b*A+c*eye(size(A))
r = roots(p)			% 求多项式系数向量p对应的根
p = poly(r)				% 求根向量为r的多项式p
```

**线性方程组求解**

对于线性方程组$\bold{A*X=B}$，$\bold{A}$为$m\times n$矩阵，当$m=n,n>n,m<n$时方程分别为“恰定”“超定”“欠定”方程。当$\bold{A}$为非奇异矩阵时，$\bold{X}=\mathrm{inv}(\bold{A})*\bold{B}$；当$\bold{A}$为奇异矩阵或非方阵时，$\bold{X}=\mathrm{pinv}(\bold{A})*\bold{B}$。一般采用左除。

## 2.3 符号运算

```matlab
sym('x')			% 创建符号变量x
sym('a',[n1,……,nM])	% 创建一个由自动生成的n1×n2×……×nM的符号数组
sym('A',n)			% 创建一个自动生成元素填充的n×n符号矩阵
syms x y z			% 创建多个符号变量
sym2poly(P)			% 符号和多项式互转
poly2sym(P)
collect(a)			% 合并同类项
expand(a)			% 符号多项式展开
factor(a)			% 因式分解
simplify(a)			% 简化符号表达式
symsum(a)			% 级数求和
solve(a)			% 符号方程求解
limit(f)			% 计算符号函数f0处极限
limit(f,x,z)		% 计算f(x)在a处的极限
limit(f,x,inf)		% 计算无穷极限
limit(f,x,z,'right')% 计算右趋a处极限
diff(f)				% 默认以x为自变量求一阶导数
diff(f,'z')			% 以z为自变量求一阶导
diff(f,x,n)			% 默认x为自变量求n阶导
diff(diff(f,x,m),y,n)%多元函数求偏导
int(f)				% 对默认变量求不定积分
int(f,v)			% 以v为自变量求不定积分
int(f,v,a,b)		% 求(a,b)上v的定积分

```

