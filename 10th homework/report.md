# Report: Some Potentials
### Author: Cathaya.Liu 2015301020026
***
![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/V-TIME.gif)
***
## 摘要
本次报告的主要内容是使用弛豫法，通过给定的初始条件和边界条件，计算电势的分布情况。通过把电场分割成均匀网格，逐步演化，经过足够多次的迭代后，就能得到比较精确的解。
## 理论与算法
* #### 1、基本思想
电势遵循Laplace方程：

![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/1.gif)

我们把计算区域划分成长、宽、高分别为Δx、Δy、Δz的小方格，在此基础上改写方程，可以得到：

![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/2.gif)

![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/3.gif)

然后有：

![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/4.gif)

对于二维情形，上式应改写为：

![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/5.gif)

* #### 2、算法描述
设定初始条件和边界条件；

创建ΔV变量，使之初值为0；

执行循环：

![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/6.gif)

![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/7.gif)

返回V[n+1]的值和ΔV的值；

判断。当ΔV足够小时，便可以认为我们得到了足够精确的解。
* #### 3、算法的Python实现
```
---------------------------------------------------------------------------------------------------------------------------------------
#引入初始需要的包。
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
---------------------------------------------------------------------------------------------------------------------------------------
#设定初值条件和边界条件，以课本内容为例。
the_origin_V=[[0 for col in range(7)] for row in range(7)]       
the_origin_V[0][1]=0.67
the_origin_V[6][1]=0.67
the_origin_V[0][5]=0.67
the_origin_V[6][5]=0.67
the_origin_V[0][2]=0.33
the_origin_V[6][2]=0.33
the_origin_V[0][4]=0.33
the_origin_V[6][4]=0.33
---------------------------------------------------------------------------------------------------------------------------------------
#进行循环运算；
V=[the_origin_V]

for i in range(0,30):
    VO=V[i]
    K=[[0 for col in range(7)] for row in range(7)]
    Delta_V=0
    for i in range(1,6):
        for j in range(1,6):
                K[i][j]=round((VO[i-1][j]+VO[i+1][j]+VO[i][j-1]+VO[i][j+1])/4,2)  
                Delta_V+=abs(VO[i][j]-K[i][j])
    for i in range(0,7):
        for j in range(0,7):
            K[i][j]=K[i][j]+V[0][i][j]
    V.append(K)
---------------------------------------------------------------------------------------------------------------------------------------
```
* #### 4、一些注意事项
使用二维列表储存网格的电势值；

运算时要注意对边界条件的保护；
## 结果陈列
* #### FIGURE 5.4 form N=1 to N=15

![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/Figure_1.png)
![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/Figure_1-1.png)
![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/Figure_1-2.png)
![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/Figure_1-3.png)

* #### FIGURE 5.6 form N=1 to N=15

![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/Figure_1-4.png)
![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/Figure_1-5.png)
![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/Figure_1-6.png)
![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/Figure_1-7.png)
![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/Figure_1-8.png)

* #### FIGURE 5.3 GIF
![](https://github.com/Cathayaliu/computationalphysics_N2015301020026/blob/master/10th%20homework/233.gif)

## 结论
弛豫法可以较好的完成对电场的计算任务，但是这种算法的时间复杂度似乎为O（n^2），这就意味着为了得到足够精确的解，需要付出很多计算资源。这种算法应该还可以进一步优化。
