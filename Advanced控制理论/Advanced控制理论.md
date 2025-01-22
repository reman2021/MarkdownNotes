## 状态空间表达（State-Space Representation）

### 传递函数

有一个质量-弹簧-阻尼（Mass-Spring-Damping）系统，输入为 $u(t)=f(t)$，输出为 $x$：

![image-20241122002954854](Advanced控制理论.assets/image-20241122002954854.png)

根据牛顿第二定律，可以得到如下平衡方程：
$$
m\ddot{x}=f(t)-kx-c\dot{x}\Rightarrow m\ddot{x}+kx+c\dot{x}=f(t)
$$
经拉普拉斯变换得
$$
ms^{2} X(s)+kX(s)+csX(s) = F(s)
$$
故该系统的传递函数为
$$
G(s)=\frac{Output}{Input}=\frac{X(s)}{F(s)} =\frac{1}{ms^2+cs+k}
$$

### 状态空间

包含输入、输出和状态变量的一阶微分方程的集合。

首先选择状态变量消除高阶项。取系统的状态变量为 $z_1,z_2$，令 $z_1=x，z_2=\dot{x}$，即 $\dot{z_1}=\dot{x}=z_2,\dot{z_2}=\ddot{x}$ ，可得
$$
\dot{z_1}=\dot{x}=z_2,\\
\dot{z_2}=\ddot{x}=\frac{f(t)-c\dot{x}-kx}{m}=\frac{1}{m}u(t)-\frac{c}{m}z_{2}-\frac{k}{m}z_{1}
$$
写成状态空间方程的形式：
$$
\begin{aligned}
\dot{z} & =Az+Bu \\
y & =Cz+Du
\end{aligned}
\Rightarrow
\begin{aligned}
&
\begin{bmatrix}
\dot{z_{1}} \\ \dot{z_{2}}
\end{bmatrix}
\begin{bmatrix}
0 & 1 \\
-\frac{k}{m} & -\frac{B}{m}
\end{bmatrix}
\begin{bmatrix}
z_{1} \\ z_{2}
\end{bmatrix}+
\begin{bmatrix}
0 \\
\frac{1}{m}
\end{bmatrix}
\begin{bmatrix}
u_{t}
\end{bmatrix}\\
& y=\begin{bmatrix}
1&0\end{bmatrix}
\begin{bmatrix}
{z_{1}}\\{z_{2}}\end{bmatrix}+[0]
\begin{bmatrix}
u_{t}
\end{bmatrix} \\
\end{aligned}
$$
对上式做拉普拉斯变换（Laplace Transform）得：
$$
sZ(s)=AZ(s)+BU(s) \Rightarrow Z(s)=(sI-A)^{-1}U(s)
\\
Y(s)=CZ(s)+DU(s) \Rightarrow Y(s)=C(sI-A)^{-1}U(s)+DU(s)
$$
故传递函数$G(s)$：
$$
G(s)=\frac{Y(s)}{U(s)}=C(sI-A)^{-1}+D=\frac{1}{ms^2+cs+k}
$$

### 状态空间方程的解

对状态空间方程 $\dot{x}=Ax+Bu$ ，两边同乘以 $e^{-At}$ 得
$$
e^{-At}\frac{dx(t)}{dt}=e^{-At}(Ax(t)+Bu(t))=Ae^{-At}x+Be^{-At}u(t)
$$
即
$$
e^{-At}\frac{dx(t)}{dt}-Ae^{-At}x=\frac{d(e^{-At}x(t))}{dt}=Be^{-At}u(t)
$$
对两边积分得
$$
e^{-At}x(t)=e^{-At_0}x(t_0)+\int_{t_0}^{t}Be^{-A\tau}u(\tau)
$$
即可得到状态空间方程的解为
$$
\begin{align*}
x(t) &= e^{A(t-t_0)}x(t_0)+\int_{t_0}^{t}e^{A(t-\tau)}Bu(\tau) \\
&= \Phi(t-t_0)x(t_0)+\int_{t_0}^{t}\Phi(t-\tau)Bu(\tau)
\end{align*}
$$
其中，$e^{A(t-t_0)}x(t_0)$ 为系统的状态转移矩阵，记为 $\Phi(t-t_0)$，表明了系统的状态从初始状态 $x(t_0)$ 转移到 $x(t)$ 的变化规律，而其变化**由矩阵A的特征值决定**。$\int_{t_0}^{t}e^{A(t-\tau)}Bu(\tau)$ 为卷积，表明了系统输入与输出的关系。



