# 第4章 MATLAB数据分析与处理

## 4.1 数据插值与拟合

**拉格朗日插值法**
$$
y(x)=\sum_{k=1}^{n}y_{k}\left(\prod_{j=1}^{n}\frac{x-x_{j}}{x_{k}-x_{j}}\right)
$$

```matlab
function y = lagrange(x0,y0,x)
% x0,y0是原始函数值，x是拟合函数的区间
% 拉格朗日插值法的思路是通过拟合一个不超过n次的多项式，使得每一组xy值都在这一函数上
ii = 1:length(x0)
y = zeros(size(x))
for i = ii
	ij = find(ii~=i);
	y1 = 1;
	for j = 1:length(ij)
		y1 = y1.*(x-x0(ij(j)));
	end
	y = y+y1*y0(i)/prod(x0(i)-x0(ij));
end
```

**埃米尔特插值**

对于给定的$n$个插值节点$x_1,x_2,\cdots,x_n$和对应的函数值$y_z,y_2,\cdots,y_n$以及一阶导数$y_z',y_2',\cdots,y_n'$
$$
y(x) = \sum_{i = 1}^{n}h_{i}[ ( x_{i} - x ) ( 2a_{i}y_{i} - y_{i} ' ) + y_{i} ]
$$
其中
$$
h_{i}=\prod_{j\neq i}^{n}\left(\frac{x-x_{j}}{x_{i}-x_{j}}\right)^{2},a_{i}=\sum_{i\neq j}^{n}\frac{1}{x_{i}-x_{j}}
$$
**分段线性插值**

```matlab
yi = interpl(x,Y,xi,method,'extrap')
%{
对一组节点(x,Y)进行插值，计算xi的函数值，x为节点向量值，Y为节点函数值；如果Y为矩阵，则对每一列进行插值
method是插值使用的算法，默认为线性算法，有以下几种
nearest：线性最近项插值
linear：线性插值
spline：三次样条插值
pchip、cubic：分段三次埃尔米特插值

当最后参数为'extrap'时，用指定方法对超出范围的值进行外推计算，当参数为extrapval时，返回标量extrapval为超出变量值。
}%
```

**数据拟合**

```matlab
p = polyfit(x,y,n)			% 返回n阶多项式
[p,S] = polyfit(x,y,n)		% 返回多项式系数p和结构S用于误差估计或预测
[p,S,mu] = polyfit(x,y,n)	% 更高级的参数，用的时候自己查
```

## 4.2 数值微积分

```matlab
Y = diff(X)		% 计算X的向前差分
Y = diff(X,n)	% 计算n阶向前差分
quad()			% 一元函数数值积分，采用自适应辛普森方法
quadl()			% 自适应Lobatto方法
quadv()			% 一元函数向量数值积分
dbquad()		%二重积分
triplequad()	%三重积分
trapz()			%梯形数值积分
```

```matlab
% 一元函数积分
Z = trapz(Y)
% 通过梯形法计算Y的近似积分
Z = trapz(X,Y)
% 根据X指定的坐标或向量间距对Y进行积分
Z = trapz(X,Y,dim)
% 通过梯形法计算Y跨维积分，维度由dim决定
q = quad(fun,a,b)
% 使用递归自适应辛普森积分法求取函数fun从a到b的近似积分，误差小于1e-6
q = quad(fun,a,b,tol)
% tol可指定大于1e-6的允许误差
q = quad(fun,a,b,tol,trace)
% 递归期间显示[fcnt a b-a Q]的值，fcnt为计算函数数值次数，a为积分左边界，b-a为区间长度，Q为区间内积分值，trace=1显示迭代信息，trace=0不显示
%-------------------------------------
% 二重积分
q = dblquad(fun,xmin,xmax,ymin,ymax)
% 通过调用quad函数计算fun(x,y)在矩形区域的双重积分
q = dblquad(fun,xmin,xmax,ymin,ymax,tol)
q = dblquad(fun,xmin,xmax,ymin,ymax,tol,trace)
% 同上
```

## 4.3 零极点问题

```matlab
% 求零点
x = fzero(fun,x0)
% 寻找x0内函数fun的零点，返回x坐标
x = fzero(fun,[x1,x2])
% 寻找区间内零点
x = fzero(fun,x0,tol,trace)
% tol代表精度，缺省时tol=0.001.trace=1迭代信息在运算中显示，trace=0不显示。
[x,fval] = fzero()
% 返回零点的x坐标同时返回该点函数值
%-----------------------------------
% 一元函数极小值
x = fminbnd(fun,x1,x2)
% 返回一个值x，该值是fun中描述的标量值函数在区间内的局部最小值
x = fminbnd(fun,x1,x2,options)
% 可选项如下
[x,fval] = fminbnd()
% fval为目标函数最小值
[x,fval,exitflag] = fminbnd()
% exitflag>0表示函数收敛于0，=0表示达到最大迭代次数，<0表示不收敛于x
[x,fval,exitflag,output] = fminbnd()
% outpu=iterations表示迭代次数，=funccount表示函数赋值次数，=algorithm表示所使用的算法
%----------------------------------
% 多元函数极小值
x = fminsearch(fun,x0)
x = fminsearch(fun,x0,options)
[x,fval] = fminsearch()
[x,fval,exitflag] = fminsearch()
[x,fval,exitflag,output] = fminsearch()
% 同上
```

<img src="./Images/第4章 MATLAB数据分析与处理/图 4.1.png" alt="图 4.1" style="zoom:50%;" />

## 4.4 常微分方程求解

```matlab
% 解析解
S = dsolve(eqn)
S = dsolve(eqn,cond)
```

**龙格库塔法**

<img src="./Images/第4章 MATLAB数据分析与处理/图 4.2.png" alt="图 4.2" style="zoom:50%;" />

**调用方式**

```matlab
[T,Y] = solver(odefun,tspan,y0)
[T,Y] = solver(odefun,tspan,y0,options)
[T,Y,TE,YE,IE] = solver(odefun,tspan,y0,options)

%{
其中，solver可以是任意命令
odefun定义了微分方程形式
tspan是微分方程积分区间
y0是初始条件
options介绍如下
}%
```

<img src="./Images/第4章 MATLAB数据分析与处理/图 4.3.png" alt="图 4.3" style="zoom:50%;" />
