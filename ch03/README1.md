# 高级变换与动画基础

> 使用`矩阵变换库 - cuon-matrix.js`

### 使用库

// 将 matrix 实例设置为 xx 变换矩阵，以（x,y,x）为旋转轴

Matrix.setRotate(angle,x,y,z)

Matrix.setTranslate(x,y,z)

Matrix.setScale(x,y,z)

// 将 matrix 乘以一个 xx 变换矩阵

Matrix.Rotate(angle,x,y,z)

Matrix.Translate(x,y,z)

Matrix.Scale(x,y,z)

### 平移+旋转

平移后的坐标 = 平移矩阵 \* 原始坐标

平移+旋转后的坐标 = 旋转矩阵 _ 平移后的坐标= 旋转 _ (平移 _ 原始) = (旋转 _ 平移) \* 原始

(旋转 \* 平移)这个矩阵 matrix 经过了多次`模型变换(model transformation)`，得出了`模型矩阵(model matrix)`

可以发现，矩阵相乘的顺序和操作顺序相反

### 旋转+平移

这个结果和上面的不同

### 动画
