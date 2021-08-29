**Attention注意**

每次渲染index.html之后，在<head>部分把原本的stylesheet部分换成以下代码

```markdown

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.css" integrity="sha384-yFRtMMDnQtDRO8rLpMIKrtPCD5jdktao2TV19YiZYWMDkUR5GQZR/NOVTdquEx1j" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.js" integrity="sha384-9Nhn55MVVN0/4OFx7EE5kpFBPsEMZxKTCnA+4fqDmg12eCTqGi6+BB2LjY8brQxJ" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
```

_https://katex.org/docs/autorender.html_

# DFT Theory
 latex test docs index


## basic concepts 基本概念：如何计算
摘自David S. Sholl, _Density functional Theory_

### Hohenberg-Kohn 1st Theorem :

The ground-state energy from Schroginger's equation is a unique functional of the electron density.

OR

ground state electron density uniquely determines all properties: energy/ wavefunction.

基态能量是电子密度分布函数(或者说，基态电子在空间中的密度分布)的泛函
一个基态电子密度对应了唯一的能量、波函数。

问题：泛函形式未知

### Hohenberg-Kohn 2nd Theorem :

The electron density that minimizes the energy of the overall functional is the true electron density corresponding to the full solution of the schrodinger equation.

使这个泛函结果（能量）最低的电子密度是薛定谔方程的解

->如果知道了泛函的形式，那么就可以计算出基态电子密度

### n(r), 或者基态电子密度

基态电子密度　$n_{(r)} = 2\Sigma \phi_i^*(r)\phi_i(r)$

更清楚一点

$$n_{(x,y,z)} = 2\phi_1^*(x,y,z)\phi_1(x,y,z)+2\phi_2^*(x,y,z)\phi_2(x,y,z)+2\phi_3^*(x,y,z)\phi_3(x,y,z)+.....$$

缩成一维：

$n_{(x)} = 2\phi_1^*(x)\phi_1(x)+2\phi_2^*(x)\phi_2(x)+2\phi_3^*(x)\phi_3(x)+.....$，对所有电子

是个期望值一样的东西

### 泛函的具体形式 the energy functional=？

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

### Kohn-Sham equation

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

### 递归求解

1\猜测一个 初始电子密度

guess a initial trial electron density n(r)

2\ 解kohn sham 方程，得到每一个电子的波函数

solve the kohn-sham equation with n(r), get the $\phi(r)$

3\ 计算新的电子密度

通过$n_{(r)} = 2\Sigma \phi_i^*(r)\phi_i(r)$

4\ 调整电子密度递归运算

### 结论：

通过 Hohenberg-Kohn定理和Kohn-Sham方程，距离比较精确地求解薛定谔方程目前只差一个合适的$E_{XC}$泛函

## 寻找合适的$E_{XC}$泛函

### LDA近似：计算Exc的一种方式

如前文所讲Exc泛函是很难知道形式的。

Exc只在一种情况下可以知道形式:当n(r)=常数，即uniform electron gas

$V_{XC}(r)=V^{electron gas}_{XC}[n(r)]$

*防止混淆,左边是函数$V_{XC}()$，右边是泛函$V^{electron gas}_{XC}[]$

使用LDA近似后，可以精确地解薛定谔方程，但是这个解不是真实解，因为薛定谔方程中的Exc是假的

### GGA

Use local electron density and the local gradient in the electron density calculation

局部电子密度，和局部电子密度的梯度

主流有：PW91 和 PBE

## 寻找合适的波函数-hartree fock

泛函在前文已经基本找好了，这里介绍找波函数的过程

当不考虑Exc时候，可以对KohnSham方程进行比较好的计算：

### 单个电子与多电子的波函数

对于单个电子，其波函数是localized的，可以用类似于$y=e^{-x^2}$描述，没有周期性，且在远离x=0的地方y约为0。但是对于晶体等多电子体系，应该使用周期性的波函数，比如$y=sin^2(x)$

### Hartree product
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

### hartree fock calculation 

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

### DFT计算过程总结

结合上文Kohn sham 方程计算，完整的DFT计算过程如下：

1, 猜测一组初始的$\alpha_{j,i}$

2，通过这个初始的$\alpha_{j,i}$计算出来一组n(r)

3，通过这个n(r) 解kohn sham方程 （或者不精确的Kohn sham方程，这个时候计算的是hartree fock limitx），得到每一个电子的波函数

4, 用每一个电子波函数计算n(r)

（通过$n_{(r)} = 2\Sigma \phi_i^*(r)\phi_i(r)$）

5，将n(r)代回$\Chi_j(x)=\sum^K_{i=1}\alpha_{j,i}\phi_{i}(x)$方程，求解$\alpha_{j,i}$

6，得到的$\alpha_{j,i}$代回第二步

### Exc

Electron correlation energy = True system energy - Hartree fock limit.

即Exc就是实际的能量减去Hartree fock limit



## reference book 参考书

David S. Sholl, _Density functional Theory_

Kittel, _solid state physics_

Dehoff _Thermodynamics_






```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/lamdalamda/vasp_sudy_note/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
