# Chapter 01
## 相关

- Canvas:绘制二维图形  ->  Echarts
- SVG:绘制矢量图  ->  d3.js
- WebGL:绘制三维图形  ->  three.js

## WebGL
- 基于OpenGL
- OpenGL ES着色器语言（GLSL ES）
- 缓存： 
  - 颜色缓存COLOR_BUFFER_BIT：在每次绘制结束后，将颜色缓存绘制到屏幕上，并清空颜色缓存
  - 深度缓存DEPTH_BUFFER_BIT
  - 模板缓存STENCIL_BUFFER_BIT(使用少)

## 着色器
- 顶点着色器：Vertex shader
  
  描述顶点特性（位置、颜色等）
- 片元着色器：Fragment shader

  进行逐片元处理过程，可以理解为像素（图像的单元）

- 内置变量：flot、vec4
### 绘制
- attribute：传输与顶点相关的数据
- uniform：对于所有顶点都相同（或与顶点无关）的数据

| 存储限定符 | 类型 |   变量名    |
| :--------- | ---: | :---------: |
| attribute  | vec4 | a_Position  |
| uniform    | vec4 | u_FragColor |

## 流程
>大部分WebGL程序都遵循如下的流程
```flow
op1=>operation: 获取Canvas元素
op2=>operation: 获取WebGL绘图上下文
op3=>operation: 初始化着色器 
op4=>operation: 设置canvas背景色 
op5=>operation: 清除canvas
op6=>operation: 绘图

op1->op2->op3->op4->op5->op6
```
---
> **齐次坐标：**
> - 提高三维数据的处理的效率
> - 它是四维的，但是当值为1时，就相当于是前三个点的坐标值
> - 齐次坐标（x,y,z,w）相对于三维坐标（x/w,y/w,z/w）  w必须大于等于0