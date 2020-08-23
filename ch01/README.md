# Chapter 01
## 相关

- Canvas:绘制二维图形  ->  Echarts
- SVG:使用XML描述2D图形  ->  d3.js
- WebGL:绘制三维图形  ->  three.js
> **Canvas**
> - 依赖分辨率
> - 不支持事件处理器
> - 弱的文本渲染能力
> - 能够以 .png 或 .jpg 格式保存结果图像
> - 最适合图像密集型的游戏，其中的许多对象会被频繁重绘
> 
> **SVG**
> - 不依赖分辨率
> - 支持事件处理器
> - 最适合带有大型渲染区域的应用程序（比如谷歌地图）
> - 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
> - 不适合游戏应用
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
- attribute：传输与顶点相关的数据（实时变化的）
- uniform：对于所有顶点都相同（或与顶点无关）的数据（一致的，“不变”的）

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