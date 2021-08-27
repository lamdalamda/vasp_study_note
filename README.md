# vasp study note

# DFT

## basic concepts

### Hohenberg-Kohn 2nd 1st Theorem :

The ground-state energy from Schroginger's equation is a unique functional of the electron density.

OR

ground state electron density uniquely determines all properties: energy/ wavefunction.

基态能量是电子密度的泛函
基态电子密度唯一地决定能量、波函数。

问题：泛函形式未知

David S. Sholl, _Density functional Theory_

### Hohenberg-Kohn 2nd Theorem :

The electron density that minimizes the energy of the overall functional is the true electron density corresponding to the full solution of the schrodinger equation.

使这个泛函结果（能量）最低的电子密度是薛定谔方程的解

->如果知道了泛函的形式，那么就可以计算出基态电子密度

### n(r), 或者基态电子密度

基态电子密度　$n_{(r)} = 2\Sigma \phi_i^*(r)\phi_i(r)$

更清楚一点

$n_{(x,y,z)} = 2\phi_1^*(x,y,z)\phi_1(x,y,z)+2\phi_2^*(x,y,z)\phi_2(x,y,z)+2\phi_3^*(x,y,z)\phi_3(x,y,z)+.....$

缩成一维：

$n_{(x)} = 2\phi_1^*(x)\phi_1(x)+2\phi_2^*(x)\phi_2(x)+2\phi_3^*(x)\phi_3(x)+.....$

是个期望值一样的东西

### 泛函的具体形式 the energy functional=？

对于单个电子已知如下：

$E[\phi_i(r)]=E_{known}[\phi_i(r)]+E_{unknown}[\phi_i(r)]$

方括号是泛函的意思,类似于函数，把圆括号变成方括号
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

## 递归求解

1\猜测一个 初始电子密度

guess a initial trial electron density n(r)

2\ 解kohn sham 方程，得到每一个电子的波函数

solve the kohn-sham equation with n(r), get the $\phi(r)$

3\ 计算新的电子密度

通过$n_{(r)} = 2\Sigma \phi_i^*(r)\phi_i(r)$

4\ 调整电子密度递归运算

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
