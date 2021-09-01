# 计算最低能量
## INCAR

### 必须

定义初始电荷密度ICHARG=2

ISMEAR：
对于未知体系ISMEAR=0
对于半导体绝缘体可以 ISMEAR=-5

### 可选：

Sigma
SIGMA=0.1左右
ENCUT=240 需参考POTCAR

## KPOINTS
示例

```
k-points
 0
Monkhorst Pack
 11 11 11
 0  0  0
```
## POSCAR

对于寻找晶格常数这种弛豫任务，不需要给精确的晶格常数

# DOS 计算density of States
ISMEAR：
对于未知体系ISMEAR=0
对于半导体绝缘体可以 ISMEAR=-5更精确

LORBIT=11输出DOS

# band Structure

ICHARG=11 读取已有的CHGCAR，因为band structure计算时候k point是固定的几个点，不利于计算

# volume relaxation寻找晶格常数

## INCAR
**必须**
ISMEAR 需要指定

IBRION>0 进行relaxation
例如IBRION=2
另外一般有ISIF=3，NSW=15或者其他比较大的数字

EDIFF 和 EDIFFG也需要指定
https://www.vasp.at/wiki/index.php/Cd_Si_volume_relaxation