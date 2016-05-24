# 作业13 电磁场分布的数值求解  
姓名：吴雨桥  
班级：13级弘毅班  
日期：2016年5月23日  
## 背景介绍  
![](https://raw.githubusercontent.com/wuyuqiao/computationalphysics_N2013301020142/master/Ex13/electric.jpg)  
上图表示空间中电磁场的一种可能分布。  
在不存在电荷的空间中，电势的分布遵循拉普拉斯方程:  
![](https://raw.githubusercontent.com/wuyuqiao/computationalphysics_N2013301020142/master/Ex13/Laplace.png)  
如果加上边界条件，理论上我们就可以解出电势V。但是除了一些特殊的边界条件以外，对于这类问题我们难以得到解析解。所以我们必须使用数值计算的方法，得到电势的数值解。理论分析表明，对于本文中所讨论的情况，二维网格化离散的情况下，非边界上的点的电势相等于其周围最近的四个点的电势的平均值。  
在本文中我们使用的方法是relaxation method，这种方法可以用来数值求解以拉普拉斯方程为代表的一类所谓的“椭圆偏微分方程”。  
这种方法也是有不同的版本，最简单的一种是Jacobi方法。Jacobi方法的精髓是从一个符合边界条件的猜测解开始，通过迭代，使得数值解收敛于真实的解。  
Jacobi方法的改进版是Gauss-Seidel方法。在计算中，我们总是算完一个点再算另一个点，也就是逐点更新计算结果。该方法主要的改进是在计算某一点的电势时，使用之前的点已经更新后的数据。  
Gauss-Seidel方法的改进版是simultaneous over-relaxation （SOR）方法。在这种方法中引入了参数alpha，从而增大了收敛速度。  
## 电容器周围电势场的求解（5.3）  
![](https://raw.githubusercontent.com/wuyuqiao/computationalphysics_N2013301020142/master/Ex13/IMG_20160523_232921.jpg)  
我们接下来尝试求解如图所示的电容器问题。图中两块有限导体平板横坐标为±0.3，纵坐标范围是-0.3~+0.3。边界条件为左侧平板上电势为+1，右侧平板上电势为-1，周围x=±1和y=±1的地方电势为0.  
我们首先使用Gauss-Seidel方法，对电容器附近的电势进行求解，求得的电势分布如图所示：  
[![](https://raw.githubusercontent.com/wuyuqiao/computationalphysics_N2013301020142/master/Ex13/capacitor1.png)  
![](https://raw.githubusercontent.com/wuyuqiao/computationalphysics_N2013301020142/master/Ex13/capacitor%202.png)](https://github.com/wuyuqiao/computationalphysics_N2013301020142/blob/master/Ex13/capacitor.py)  
点击图片可以获得绘图代码。由图可知，空间中的电势场在左侧平板上呈现一个峰，在右侧平板上呈现一个谷。整体的分布情况与我们的直觉相符。下图为由电势分布推导出的电场分布：  
[![](https://raw.githubusercontent.com/wuyuqiao/computationalphysics_N2013301020142/master/Ex13/capacitor%203.png)](https://github.com/wuyuqiao/computationalphysics_N2013301020142/blob/master/Ex13/capacitor%202.py)  
点击图片可以获得绘图代码。由图可知，电场线主要从左侧板流向右侧板，板间的电场是均匀的。这与电磁学的结论相符。