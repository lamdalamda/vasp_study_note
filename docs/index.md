<a name="index">**Index**</a>
<a href="#0">DFT Theory</a>  
&emsp;<a href="#1">basic concepts 基本概念：如何计算</a>  
&emsp;&emsp;<a href="#2">Hohenberg-Kohn 1st Theorem :</a>  
&emsp;&emsp;<a href="#3">Hohenberg-Kohn 2nd Theorem :</a>  
&emsp;&emsp;<a href="#4">n(r), 或者基态电子密度</a>  
&emsp;&emsp;<a href="#5">泛函的具体形式 the energy functional=？</a>  
&emsp;&emsp;<a href="#6">Kohn-Sham equation</a>  
&emsp;&emsp;<a href="#7">递归求解</a>  
&emsp;&emsp;<a href="#8">结论：</a>  
&emsp;<a href="#9">寻找合适的$E_{XC}$泛函</a>  
&emsp;&emsp;<a href="#10">LDA近似：计算Exc的一种方式</a>  
&emsp;&emsp;<a href="#11">GGA</a>  
&emsp;<a href="#12">寻找合适的波函数-hartree fock</a>  
&emsp;&emsp;<a href="#13">单个电子与多电子的波函数</a>  
&emsp;&emsp;<a href="#14">Hartree product</a>  
&emsp;&emsp;<a href="#15">hartree fock calculation </a>  
&emsp;&emsp;<a href="#16">DFT计算过程总结</a>  
&emsp;&emsp;<a href="#17">Exc</a>  
&emsp;<a href="#18">一些补充</a>  
&emsp;<a href="#19">物质的性质： property of matters</a>  
&emsp;<a href="#20">bonding：</a>  
&emsp;<a href="#21">Hartree atomic units</a>  
<a href="#22">晶体学知识 crystallography</a>  
&emsp;<a href="#23">fourier transformation</a>  
&emsp;<a href="#24">reciprocal sapce 倒易空间</a>  
&emsp;&emsp;<a href="#25">一维理解</a>  
&emsp;&emsp;<a href="#26">倒空间的有意义的点q需要满足的条件</a>  
&emsp;&emsp;<a href="#27">一维小晶体的倒空间与布里渊区</a>  
&emsp;&emsp;<a href="#28">三维大晶体的倒空间与布里渊区</a>  
&emsp;&emsp;<a href="#29">推导Block theorem</a>  
&emsp;<a href="#30">k point取样</a>  
&emsp;&emsp;<a href="#31">trapezoidal method</a>  
&emsp;&emsp;<a href="#32">Gaussian quadrature</a>  
&emsp;<a href="#33">reference book 参考书</a>  
<a href="#34">Header 1</a>  
&emsp;<a href="#35">Header 2</a>  
&emsp;&emsp;<a href="#36">Header 3</a>  
&emsp;&emsp;<a href="#37">Jekyll Themes</a>  
&emsp;&emsp;<a href="#38">Support or Contact</a>  
**Attention注意**

每次渲染index.html之后，在<head>部分把原本的stylesheet部分换成以下代码

```markdown

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.css" integrity="sha384-yFRtMMDnQtDRO8rLpMIKrtPCD5jdktao2TV19YiZYWMDkUR5GQZR/NOVTdquEx1j" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.js" integrity="sha384-9Nhn55MVVN0/4OFx7EE5kpFBPsEMZxKTCnA+4fqDmg12eCTqGi6+BB2LjY8brQxJ" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
```

_https://katex.org/docs/autorender.html_

# <a name="0">DFT Theory</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
 latex test docs index


## <a name="1">basic concepts 基本概念：如何计算</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
摘自David S. Sholl, _Density functional Theory_

### <a name="2">Hohenberg-Kohn 1st Theorem :</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

The ground-state energy from Schroginger's equation is a unique functional of the electron density.

OR

ground state electron density uniquely determines all properties: energy/ wavefunction.

基态能量是电子密度分布函数(或者说，基态电子在空间中的密度分布)的泛函
一个基态电子密度对应了唯一的能量、波函数。

问题：泛函形式未知

### <a name="3">Hohenberg-Kohn 2nd Theorem :</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

The electron density that minimizes the energy of the overall functional is the true electron density corresponding to the full solution of the schrodinger equation.

使这个泛函结果（能量）最低的电子密度是薛定谔方程的解

->如果知道了泛函的形式，那么就可以计算出基态电子密度

### <a name="4">n(r), 或者基态电子密度</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

基态电子密度　$n_{(r)} = 2\Sigma \phi_i^*(r)\phi_i(r)$

更清楚一点

$$n_{(x,y,z)} = 2\phi_1^*(x,y,z)\phi_1(x,y,z)+2\phi_2^*(x,y,z)\phi_2(x,y,z)+2\phi_3^*(x,y,z)\phi_3(x,y,z)+.....$$

缩成一维：

$n_{(x)} = 2\phi_1^*(x)\phi_1(x)+2\phi_2^*(x)\phi_2(x)+2\phi_3^*(x)\phi_3(x)+.....$，对所有电子

是个期望值一样的东西

### <a name="5">泛函的具体形式 the energy functional=？</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

对于单个电子已知如下：

$E[\phi_i(r)]=E_{known}[\phi_i(r)]+E_{unknown}[\phi_i(r)]$

方括号是泛函的意思。类似于函数，把圆括号变成方括号
$ n(r) -- E[] --> E[n(r)] $


$E_{known}[]$是已知的能量泛函，包括电子动能，电子-核与电子-电子

$E_{unknown}[]$是未知的能量泛函：交换能


其中

$E_{known}[\phi_i(r)]=\frac{-\hbar}{m}\Sigma\int\phi_i^*(r)\nabla^2\phi_i(r)d^3r+\int V(r)n(r)d^3r+e^2/2\int \int \frac {n(r)n(r')}{|r-r'|}d^3rd^3r'+E_{ion} $

缩成一维，对于0号电子$\phi_0$

$E_{known}[\phi_0(x)]=\frac{-\hbar}{m}\Sigma\int\phi_0^*(x)\phi_i''(x)dx+\int V(x)n(x)dx+e^2/2\int \int \frac {n(x)n(x')}{|x-x'|}dxdx'+E_{ion} $

（不太清楚为什么会有一个求和）

由于前述$n_{(r)} = 2\Sigma \phi_i^*(r)\phi_i(r)$

所以虽然不知道是否合理，但是推导出来这个公式，即phi和n（r）有同样的泛函？？

$E[2\Sigma \phi_i^*(r)\phi_i(r)]=E_{known}[2\Sigma \phi_i^*(r)\phi_i(r)]+E_{unknown}[2\Sigma \phi_i^*(r)\phi_i(r)]$

也就是说泛函的形式是 
$E[]=E_{known}[]+E_{unknown}[]$

问题：解不出来电子密度n(r)因此需要kohn sham 方程解n(r)

### <a name="6">Kohn-Sham equation</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

Kohn-Sham equation是用来找电子密度，即n(r):

Kohn-Sham 方程是:

$[\frac{-\hbar^2}{2m}\nabla^2+V(r)+V_H(r)+V_{XC}(r)]\phi_i(r)=\epsilon_i\phi_i(r)$

其中

$V(r)$是薛定谔方程中已知的，是电子和所有原子核的相互作用

$V_H(r)$是hartree potential，是 coulomb repulsion  between "this electron" and "the total electron density", 或者说电子i和整个电子密度n(r)之间的coulomb repulsion

$V_H(r)=e^2\int \frac{n(r')}{|r-r'|}d^3r'$
理解为以r点的坐标向外积分？

$V_{XC}$是未知的，虽然有
$V_{XC}=\frac{\delta E_{XC}(r)}{\delta n(r)} $

用人能看懂的方法重新写

对于0号电子,其具有能量$\epsilon_0$，缩到一维，波函数满足

$[\frac{-\hbar^2}{2m}\phi_0''(x)+V(x)+e^2\int \frac{n(x')}{|x-x'|}dx'+V_{XC}(x)]\phi_0(x)=\epsilon_0\phi_0(x)$

### <a name="7">递归求解</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

1\猜测一个 初始电子密度

guess a initial trial electron density n(r)

2\ 解kohn sham 方程，得到每一个电子的波函数

solve the kohn-sham equation with n(r), get the $\phi(r)$

3\ 计算新的电子密度

通过$n_{(r)} = 2\Sigma \phi_i^*(r)\phi_i(r)$

4\ 调整电子密度递归运算

### <a name="8">结论：</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

通过 Hohenberg-Kohn定理和Kohn-Sham方程，距离比较精确地求解薛定谔方程目前只差一个合适的$E_{XC}$泛函

## <a name="9">寻找合适的$E_{XC}$泛函</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="10">LDA近似：计算Exc的一种方式</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

如前文所讲Exc泛函是很难知道形式的。

Exc只在一种情况下可以知道形式:当n(r)=常数，即uniform electron gas

$V_{XC}(r)=V^{electron gas}_{XC}[n(r)]$

*防止混淆,左边是函数$V_{XC}()$，右边是泛函$V^{electron gas}_{XC}[]$

使用LDA近似后，可以精确地解薛定谔方程，但是这个解不是真实解，因为薛定谔方程中的Exc是假的

### <a name="11">GGA</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

Use local electron density and the local gradient in the electron density calculation

局部电子密度，和局部电子密度的梯度

主流有：PW91 和 PBE

## <a name="12">寻找合适的波函数-hartree fock</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

泛函在前文已经基本找好了，这里介绍找波函数的过程

当不考虑Exc时候，可以对KohnSham方程进行比较好的计算：

### <a name="13">单个电子与多电子的波函数</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

对于单个电子，其波函数是localized的，可以用类似于$y=e^{-x^2}$描述，没有周期性，且在远离x=0的地方y约为0。但是对于晶体等多电子体系，应该使用周期性的波函数，比如$y=sin^2(x)$

### <a name="14">Hartree product</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
当总共只有一个电子时候，

$h\Chi=E\Chi$

会得到许多个解 $\Chi_j$
对于每个解$\Chi_1,\Chi_2,\Chi_3,....$
(假设$\Chi_1$对应了最低能量)
对应的能量分别是 $E_1,E_2,E_3,....$,

其中$E_1$是能量最低的基态

对于多个电子体系来说

当忽略了电子-电子相互作用时

Hamiltonian： $H=h_1+h_2+h_3+...$

$h_i$是第i个电子的动能和势能算符

可以得到
$\phi(x_1,x_2,....x_n)=\prod{\Chi_{ji}}$
其中j代表了能级（像上面j=1是基态）

对于基态来讲
$\phi(x_1,x_2,....x_n)=\Chi_{11}(x_1)\Chi_{12}(x_2)\Chi_{13}(x_3)...$

能量则是简单相加
$E=E_{11},E_{12},E_{13},....$,

以上方法求得的波函数由于忽略了电子-电子相互作用，所以存在以下问题：

_由于电子是费米子，所以当两个电子交换位置时候符号必须改变_

然而，当电子交换位置时候，按照上式，波函数的正负号没有变化

所以：引入Slater determinant

双电子的Slater determinant:

$$\phi(x_1,x_2)=\frac{1}{\sqrt2}det\left\{\begin{matrix}
\Chi_j(x_1)&\Chi_j(x_2)\\
\Chi_k(x_1)&\Chi_k(x_2)\\
\end{matrix}\right\}$$

$$\phi(x_1,x_2)=\frac{1}{\sqrt2}[\Chi_j(x_1)\Chi_k(x_2)-\Chi_k(x_1)\Chi_j(x_2)]$$

这个波函数满足pauli exclusiong principle：不区分电子， 当电子具有相同坐标时等于0

### <a name="15">hartree fock calculation </a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

hartree fock calculation 基于这个假设；原子核位置固定


Kohn sham 方程是
$[\frac{-\hbar^2}{2m}\nabla^2+V(r)+V_H(r)+V_{XC}(r)]\phi_i(r)=\epsilon_i\phi_i(r)$

而对于**单个**电子,HF calculation是： 
$[\frac{-\hbar^2}{2m}\nabla^2+V(r)+V_H(r)]\phi_i(x)=\E_j\Chi_j(x)$
相比于kohn sham减少了一个Exc项

由前面slater行列式可以看到，如果想要描述一个N个电子体系，那么需要知道$\Chi_1$到$\Chi_N$

对此，可以找到有限个（K个）函数，即$\phi_{1}(x)$到$\phi_{K}(x)$，使得这K个函数可以加权相加得到$\Chi_1$到$\Chi_N$
这K个函数被称为basis set
即：

$\Chi_j(x)=\sum^K_{i=1}\alpha_{j,i}\phi_{i}(x)$

写的清楚一点，对第一个$\Chi_1(x)$：

$\Chi_1(x)=\alpha_{1,1}\phi_{1}(x)+\alpha_{1,2}\phi_{2}(x)+...+\alpha_{1,K}\phi_{K}(x)$

现在已知$\phi_{1}(x)$到$\phi_{K}(x)$，问题变成了找到$\alpha_{j,i}$

找到$\alpha_{i,j}$的方式：继续进行递归运算：

1, 猜测一组初始的$\alpha_{j,i}$

2，通过这个初始的$\alpha_{j,i}$计算出来一组n(r)

3, n(r)代回$\Chi_j(x)=\sum^K_{i=1}\alpha_{j,i}\phi_{i}(x)$方程，求解$\alpha_{j,i}$

通过这个递归运算，可以得到一个精确的能量值，这个能量值是Hartree fock limit.

这个值虽然精确，但并不是实际的电子能量， 因为没有考虑到Exc，即Hartree fock方法实际上并没有解决电子-电子相互作用

### <a name="16">DFT计算过程总结</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

结合上文Kohn sham 方程计算，完整的DFT计算过程如下：

1, 猜测一组初始的$\alpha_{j,i}$

2，通过这个初始的$\alpha_{j,i}$计算出来一组n(r)

3，通过这个n(r) 解kohn sham方程 （或者不精确的Kohn sham方程，这个时候计算的是hartree fock limitx），得到每一个电子的波函数

4, 用每一个电子波函数计算n(r)

（通过$n_{(r)} = 2\Sigma \phi_i^*(r)\phi_i(r)$）

5，将n(r)代回$\Chi_j(x)=\sum^K_{i=1}\alpha_{j,i}\phi_{i}(x)$方程，求解$\alpha_{j,i}$

6，得到的$\alpha_{j,i}$代回第二步

### <a name="17">Exc</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

Electron correlation energy = True system energy - Hartree fock limit.

即Exc就是实际的能量减去Hartree fock limit


## <a name="18">一些补充</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
参考书：Richard M. Martin _Electronic structure: Basic theory and practical method_

## <a name="19">物质的性质： property of matters</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

物质属性一般会取决于两个种类：
1、electronic ground state 基态电子
2、electronic excited state 激发态电子

原因是；原子核质量远大于电子，因此相对于电子来说可以基本看作静止
这就是Born-Oppenheimer approximation

电子最低能量态决定了原子核的结构
the lowest energy state of the elctrons determines the spatial structure of nuclei:

## <a name="20">bonding：</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
一般认为分为5类：
closed shell system:稀有气体
ionic
metallic
covalent
hydrogen:比较特殊，因为氢原子是唯一没有core electron的 （往上面的氦的core electron是1s的两个电子）

实际材料的bonding一般是这五种的结合

## <a name="21">Hartree atomic units</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

$\hbar =m_e = e = 4\pi /\epsilon_0 = 1$

定义以上单位为1，用来简化计算

# <a name="22">晶体学知识 crystallography</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
参考书：Richard M. Martin _Electronic structure: Basic theory and practical method_

A crystal can be completely specified by the types and positions of the nuclei in **one repeat unit (primitive unit cell)** annd the rules that describe the **repetition (translation)**

primitive cell有很多种，wigner seitz cell是其中一种

Wigner Seitz cell: the most compact cell that is symmetric about the origin **注意 wigner seitz cell是在real space/实空间** 

wigner seitz cell在倒空间对应的是**first brillouin zone**

_fcc 的 wigner seitz cell是bcc的first brillouin zone_



## <a name="23">fourier transformation</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

![Image](./Fourier_series_and_transform.gif)
![Image](./40cf849e55ed95732a60b52d4019d609_720w.jpg)
_https://zhuanlan.zhihu.com/p/19763358_


## <a name="24">reciprocal sapce 倒易空间</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

考虑任何一个描述晶体性质的方程（比如说电子密度）

由于晶体的周期性，在实空间电子密度是周期性相同的,也就是说对于电子密度$n(r+T(r'))=n(r)$其中T是任何的translation操作

### <a name="25">一维理解</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

对于一个一维的，总共三个晶格的晶体，晶格常数为a

---《原子》---a---《原子》---a---《原子》---

那么电子密度n(x)必须满足：

    n(x)    =    n(x+a)       =n(x+2a)  
         
当0<x<a

因为n(x)有这样的周期性，所以一定可以对其进行傅里叶变化

傅里叶变化是从x空间变为q空间$n(x)->n(q)$

对于这个长度为3的一维晶体，其中含有3个cell，那么晶格个数N=3

从x空间到q空间的傅里叶变化是

$n(q)=\frac{1}{\Omega_{crystal}}\int_{\Omega_{crystal}} dxn(x)exp(iq·x)$

代入条件

$n(q)=\frac{1}{3a}\int_0^{3a} dxn(x)e^{(iq·x)}$

对于每一个晶格内部进行积分

$n(q)=\frac{1}{3a}(\int_0^adxn(x)e^{iq·x} +\int_a^{2a}dxn(x)e^{iq·x}+\int_{2a}^{3a}dxn(x)e^{iq·x})$

$n(q)=\frac{1}{3a}(\int_0^adxn(x)e^{iq·x} +\int_0^{a}dxn(x+a)e^{iq·(x+a)}+\int_{0}^{a}dxn(x+2a)e^{iq·x+2a})$

由于n(x)周期性n(x)=n(x+a)=n(x+2a)

$n(q)=\frac{1}{3a}(\int_0^adxn(x)e^{iq·x} +\int_0^{a}dxn(x)e^{iq·(x+a)}+\int_{0}^{a}dxn(x)e^{iq·x+2a})$

把exp拆开

$n(q)=\frac{1}{3a}(\int_0^adxn(x)e^{iq·x} +\int_0^{a}dxn(x)e^{iq·x}e^{iq·a}+\int_{0}^{a}dxn(x)e^{iq·x}e^{iq·2a})$

合并得到

$n(q)=\frac{1}{3a}(e^{iq·0a}+e^{iq·a}+e^{iq·2a})(\int_0^adxn(x)e^{iq·x})$

从而得到三维大晶体的一般形式：

$f(q)=\frac{1}{\Omega_{crystal}}\sum_0^{N_xa1}\sum_0^{N_ya2} \sum_0^{N_za3}  e^{iq·T(n1,n2,n3)} \int_0^{a1} \int_0^{a2} \int_0^{a3} dxdydzf(x,y,z) e^{iq·(x,y,z)}$

$f(q)=\frac{1}{\Omega_{crystal}}\sum e^{iq·T} \int drf(r) e^{iq·r}$

T是所有可能的平移（translation）操作

### <a name="26">倒空间的有意义的点q需要满足的条件</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

根据Born-Von Karmen条件，傅里叶变化后的每一个component都必须满足 $exp(i q·Na)=1$

为了满足$exp(iq·3a) =1$，则必须有：

$q·a=2\pi \frac{integer}{3}$

对于三维大晶体，$q·a=2\pi \frac{integer}{N}$

N是一个很大的值，所以大晶体的q点是连续的

### <a name="27">一维小晶体的倒空间与布里渊区</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

继续对于$q·a=2\pi \frac{integer}{3}$

尝试当interger=1

$q·a=\frac{2\pi}{3}$

$q=\frac{2\pi}{3a}$

$n(q)=\frac{1}{3a}(e^{0}+e^{\frac{i2\pi}{3}}+e^{\frac{i4\pi}{3}})(\int_0^adxn(x)e^{iq·x})$

然而

$e^{0}+e^{\frac{i2\pi}{3}}+e^{\frac{i4\pi}{3}}=0$

所以$n(\frac{2\pi}{3a})=0$

之后发现只有当$q·a=2\pi · integer$时（而非$q·a=2\pi \frac{integer}{3}$）

n(q)才有

$n(q)=\frac{1}{3a}(e^{2\pi}+e^{2\pi}+e^{2\pi})(\int_0^adxn(x)e^{2\pi})$

$n(q)=\frac{1}{3a}(1+1+1)(\int_0^adxn(x)*1)$

也就是说，是个非0的fourier component

从而定义单位倒易矢量$b=\frac{2\pi}{a}$


使n(r)的fourier component 非0的q的集
合记为G（倒易空间），

$G(m)=m * b$

其中m为任意正整数，且m=0 为基态

第一布里渊区是倒空间的wigner-seitz cell

同样用上面的3a大小的一维晶体距离

注意倒空间是无限长的一维空间,倒空间两个相邻格点之间距离为$b=\frac{2\pi}{a}$

第一布里渊区是

$-\frac{\pi}{a}<q<+\frac{\pi}{a}$

q=0对应了基态

**注意：这些是基态的条件**

### <a name="28">三维大晶体的倒空间与布里渊区</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>


$n(x+x',y+y',z+z')=n(x,y,z)$，其中x' y' z'是整数倍的$a_1 a_2 a_3$

$a_1 a_2 a_3$是三个晶格向量

傅里叶变化可以对所有有周期性性质的函数使用

因为n(r)有这样的周期性，所以一定可以对其进行傅里叶变化

傅里叶变化是$n(r)->n(q)$

对于一个体积为$\Omega$的三维晶体，其中含有$N_x \times N_y \times N_z = N_{cell}$个cell的体系 

根据Born-Von Karmen条件，傅里叶变化后的每一个component都要满足 $exp(iq· N_x a_1)=exp(iq· N_ya_2)=exp(iq· N_z a_3)=1$



为了满足$exp(iq· N_x a_1)=exp(iq· N_ya_2)=exp(iq· N_z a_3)=1$，则必须有：

$q·(a_1,a_2,a_3)=2\pi \frac{integer}{N_i}$

从r到q的傅里叶变化是

$f(q)=\frac{1}{N_{cell}\Omega_{cell}}\sum e^{iq·T} \int drf(r) e^{iq·r}$

通过计算，使f(q)非零需要满足的条件是

$q·(a_1,a_2,a_3)=2\pi · integer$

从而确立了倒空间的基矢，
$G(m_1,m_2,m_3)=m_1b_1,m_2b_2,m_3b_3$

其中$m_1,m_2,m_3$是任意整数，$b_1,b_2,b_3$是$a_1 a_2 a_3$的倒向量

### <a name="29">推导Block theorem</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

根据一通看不懂的证明（P87~P88, section 4.4 Richard M. Martin _Electronic structure: Basic theory and practical method_）

继续考虑一维情况，对于一个算符，比如说$\hat{H}$作用在电子波函数上，得到电子能量。$\hat{H}$是算符，$\epsilon$是本征态$\phi(x)$是本征方程
$\hat{H}\phi(x)=[-\frac{\hbar^2}{2m_e }\nabla^2+V(r)]\phi(x)=\epsilon\phi(x)$

类似得，可以定义translation算符$\hat{T_x}$,角标x代表一维的x轴上的translation

$\hat{T}_{x_0}\phi(x)=\phi(x+x_0)$

不知道为什么但是hamiltonian $\hat{H}$与$\hat{T_x}$是commute的

$\hat{H}\hat{T_x}=\hat{T_x}\hat{H}$

由于commute，$\hat{H}$的本征态也是$\hat{T_x}$的本征态

另外由于$\hat{T}_{x_0}\hat{T}_{x_1}=\hat{T}_{x_0+x_1}$

(显然分别挪了x0和x1的操作与一下子挪了x0+x1的操作结果是一样的)

则一定有$$\hat{T}_{x_0+x_1}\phi(x)=\hat{T}_{x_0}\hat{T}_{x_1}\phi(x)=t_{(x_0+x_1)}\phi(x)=(t_{x_0}+t_{x_1})\phi(x)$$

由于如下看不懂的原因：
**modules of t(x) must be unity 模必须为1？？**

**且本征方程必须满足周期性**

所以t(x)必须有$t(x)=e^{ik·T_x}$格式

其中$T_x$是x轴上移动的距离，$k=\frac{integer\times b}{cell总数}=\frac{2n\pi}{3a}$.其中n是任意整数integer，b是倒易空间单位矢量

由此

$\hat{T}_x\phi(x)=\phi(x+t_x)=e^{ik·T_x}\phi(x)$

具体来讲：
在之前的晶格常数为a总长度为3的一维晶体里面
考虑方程（简化掉了hbar）
$\hat{H}\phi(x)=[-\nabla^2+V(r)]\phi(x)=\epsilon\phi(x)$
假设基态是$\phi(x)=e^{\frac{i2\pi x}{a}}$



对于translation本身有如下性质

\hat{T_x}

即对于任意的translation操作**T**(即使长度不等于周期)

有$\phi(r+T)=e^{ik·T}\phi(r)$



激发态下晶体一般不再具有Born-Von Karmen所述的周期性



## <a name="30">k point取样</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

继续考虑一维情况，已知从x到q有傅里叶变换 
$n(q)=\frac{1}{\Omega_{crystal}}\int_{\Omega_{crystal}} dxn(x)exp(iq·x)$

那么从q到x也有傅里叶变换**注意：正负号很可能错了，需要以后勘误**

$n(x)=\frac{1}{\Omega_{k space}}\int_{\Omega_{k space}} dqn(q)exp(ix·q)$

虽然不知道n(q)是干什么的，但是n(x)是我们想要求的电子密度

$n(x)=\frac{1}{\Omega_{k space}}\int_{\Omega_{k space}} dqn(q)exp(ix·q)$这个公式中，可以看到想要求的是一个积分。显然积分是很难求的，所以考虑积分的定义

积分可以理解为：函数与x轴（在这个公式里面是与q轴）围出的面积

那么可以将积分用取样点离散化

### <a name="31">trapezoidal method</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
trepezoidal 方式拟合积分公式，对区域内进行均匀取样
$\int _{-1}^1f(x)dx \approx \frac{1}{n}[f(-1)+2\sum_{j=1}^{n-1}f(x_j)+f(1)]$

比如当n=4情况

$\int _{-1}^1f(x)dx \approx 0.25f(-1)+0.25f(-0.5)+0.25f(0)+0.25(0.5)+0.25(1)$

### <a name="32">Gaussian quadrature</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

$\int _{-1}^1f(x)dx \approx 0.25f(-1)+0.25f(-0.5)+0.25f(0)+0.25(0.5)+0.25(1)$可以转为如下公式，此时取样点是不均匀分布的

$\int _{-1}^1f(x)dx \approx \sum_{j=1}^n c_j f(x_j)$

不均匀分布的取样点是Gaussian quadrature，$c_j$是系数，由Gaussian quadrature来规定。
















## <a name="33">reference book 参考书</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

David S. Sholl, _Density functional Theory_

Kittel, _solid state physics_

Dehoff _Thermodynamics_






```markdown
Syntax highlighted code block

# <a name="34">Header 1</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
## <a name="35">Header 2</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
### <a name="36">Header 3</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### <a name="37">Jekyll Themes</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/lamdalamda/vasp_sudy_note/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### <a name="38">Support or Contact</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
