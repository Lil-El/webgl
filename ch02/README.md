# 绘制和变换三角形

## Content
- 绘制三角形
- 绘制其他基本图形
- 变换：移动、旋转、缩放等
- 矩阵简化变换

## 绘制多个点
三维模型的基本单位就是三角形，游戏模型这种复制的模型都包含了上万个三角形和顶点

#### 缓冲区对象buffer object
一次性向着色器传入多个顶点数据

#### 流程
- 获取webgl上下文
- 初始化着色器
- 设置点的坐标 （新）
  - 创建buffer对象
  - 创建类型化数组，所有顶点的坐标数据
  - 绑定buffer
  - 向buffer添加数据
  - 将buffer的数据分配给attribute变量
  - 开启attibute变量
- 设置背景色
- 清空canvas
- 绘制
  - 删除顶点的size属性
  - drawArrays使用gl.TRIANGLES而不是gl.POINTS
    - POINTS：点
    - TRIANGLES：三角形，(v0,v1,v2) (v3,v4,v5) (v5,v6,v7)
    - LINES：线段，(v0,v1) (v2,v3) (v3,v4)
    - LINE_STRIP：线条，(v0,v1) (v1,v2) (v2,v3)
    - LINE_LOOP：连接的线条，(v0,v1) (v1,v2) (v2,v3) (v3,v0)
    - TRIANGLE_STRIP：带状三角形，(v0,v1,v2) (v2,v1,v3) (v2,v3,v4)
    - TRIANGLE_FAN：三角形组成的类似扇形的图形，(v0,v1,v2) (v0,v2,v3) (v0,v3,v4)

### 平移
定义uniform变量，与VERTEX_SOURCE的gl_position相加
>平移公式  x' = x + Tx(常量)
### 旋转
- 旋转轴
- 方向
- 角度

一个图形以z轴旋转了b度，如果b度为正，即逆时针旋转
默认遵守右手法则，右手握拳，大拇指指向旋转轴的正方向，其余手指的方向就是旋转方向，也就是`正旋转`；

>旋转公式  x' = x * cosB - y * sinB
>         y' = x * sinB + y * cosB
### 变换矩阵：旋转
> **矩阵相乘：**
> 
>     [ x' ]   [ a b c ]   [ x ]
>     [ y' ] = [ d e f ] * [ y ]
>     [ z' ]   [ g h i ]   [ z ]
> x' = ax + by + cz
> 
> y' = dx + ey + fz

将旋转公式和矩阵比较，可以得出旋转矩阵

x' = ax + by + cz 与 x' = x * cosB - y * sinB

a = cosB , b = -sinB , z = 0

其他同理，得出`旋转矩阵（变换矩阵）`：

    [ x' ]   [ cosB -sinB 0 ]   [ x ]
    [ y' ] = [ sinB cosB  0 ] * [ y ]
    [ z' ]   [ 0    0     1 ]   [ z ]
### 变换矩阵：平移
x' = x + Tx(Tx是一个常量，不是相乘)

y' = y + Ty

x' = x + Tx 和 x' = ax + by + cz
因为有常量，所以使用4个分量来表示矩阵(4 x 4)

    [ x' ]   [ a b c d ]   [ x ]
    [ y' ] = [ e f g h ] * [ y ]
    [ z' ]   [ i j k l ]   [ z ]
    [ 1  ]   [ m n o p ]   [ 1 ]

x' = ax + by + cz + d 和 x' = x + Tx;

    [ x' ]   [ 1 0 0 Tx ]   [ x ]
    [ y' ] = [ 0 1 0 Ty ] * [ y ]
    [ z' ]   [ 0 0 1 Tz ]   [ z ]
    [ 1  ]   [ 0 0 0  1 ]   [ 1 ]

这就是`平移矩阵`
#### 4x4的旋转矩阵
上面创建了旋转和平移矩阵，而我们要创建一个矩阵去实现 **旋转平移** ，而 3 x 3 和 4 x 4 的矩阵无法相乘，所以我们要将 3 x 3 的矩阵转换为 4 x 4 的矩阵。

x' = x * cosB - y * sinB

y' = x * sinB + y * cosB

和

x' = ax + by + cz + d

y' = ex + fy + gz + h

得出 **4x4旋转矩阵** ：

    [ x' ]   [ cosB -sinB 0 0 ]   [ x ]
    [ y' ] = [ sinB cosB  0 0 ] * [ y ]
    [ z' ]   [ 0    0     1 0 ]   [ z ]
    [ 1  ]   [ 0    0     0 1 ]   [ 1 ]

### 变换矩阵：缩放
x' = x * Sx(常量) 和 x' = ax + by + cz + d

得出变换矩阵：

    [ x' ]   [ Sx 0  0  0 ]   [ x ]
    [ y' ] = [ 0  Sy 0  0 ] * [ y ]
    [ z' ]   [ 0  0  Sz 0 ]   [ z ]
    [ 1  ]   [ 0  0  0  1 ]   [ 1 ]