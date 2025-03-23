# 第5章 MATLAB绘图

## 5.1 二维绘图

**线型设置**

```matlab
plot(x,y)
plot(x,y,'s','linewidth',4)% s为线型参数
```

<img src="./Images/第5章 MATLAB绘图/图 5.1.png" alt="图 5.1" style="zoom:50%;" />

**坐标轴设置**

<img src="./Images/第5章 MATLAB绘图/图 5.2.png" alt="图 5.2" style="zoom:50%;" />

**单窗口绘制多图**

<img src="./Images/第5章 MATLAB绘图/图 5.3.png" alt="图 5.3" style="zoom:50%;" />

**子图绘制**

<img src="./Images/第5章 MATLAB绘图/图 5.4.png" alt="图 5.4" style="zoom:50%;" />

**fplot函数**

<img src="./Images/第5章 MATLAB绘图/图 5.5.png" alt="图 5.5" style="zoom:50%;" />

fplot有两种使用方式

```matlab
fplot(@func,[0,1])
fplot(@x f(x),[0,1])
```

**交互式绘图**

- **ginput**：通过鼠标直接读取二维平面图形上任意一点坐标值

  <img src="./Images/第5章 MATLAB绘图/图 5.6.png" alt="图 5.6" style="zoom:50%;" />

- **zoom**：对坐标轴进行缩放

  <img src="./Images/第5章 MATLAB绘图/图 5.7.png" alt="图 5.7" style="zoom:50%;" />

## 5.2 三维绘图

```matlab
plot3(x,y,z,LineSpec,'PropertyName',PropertyValue)
% 线绘图
```

**线面网格图mesh**

<img src="./Images/第5章 MATLAB绘图/图 5.8.png" alt="图 5.8" style="zoom:50%;" />

**滑面网格图surf**

**直方图bar**

<img src="./Images/第5章 MATLAB绘图/图 5.9.png" alt="图 5.9" style="zoom:50%;" />

**饼图pie**

<img src="./Images/第5章 MATLAB绘图/图 5.10.png" alt="图 5.10" style="zoom:50%;" />

**茎叶图**

<img src="./Images/第5章 MATLAB绘图/图 5.11.png" alt="图 5.11" style="zoom:50%;" />

**特殊命令**

<img src="./Images/第5章 MATLAB绘图/图 5.12.png" alt="图 5.12" style="zoom:50%;" />

<img src="./Images/第5章 MATLAB绘图/图 5.13.png" alt="图 5.13" style="zoom:50%;" />

## 5.4 三维图形高级设置

```matlab
% 视点控制
view(az,el)
% 设置查看三维图的三个角度，az是水平方位角，从y轴负方向开始逆时针旋转为正；el是垂直方位角，以向z轴方向的旋转为正
view([x,y,z])	% 设置视角忽略赋值
view(2)			% 默认二维视角，az=0，el=30
view(3)			% 默认三维视角，az=-37.5，el=30
view(T)			% 根据矩阵设置，T是由viewmtx产生的4*4矩阵
[az,el] = view	% 返回当前az，el值
T = view		% 返回转换矩阵T
%---------------------------------
%光照控制
camplight	% 设置并移动摄像头光源
lightangle	% 球坐标下定位或设置光源
light		% 设置光源
lightning	% 旋转光源模式
material	% 设置图像表面对光照的反应模式
```

