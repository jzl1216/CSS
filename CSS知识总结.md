setInterval()存在bug,解决方法就是，给它赋予一个id，在需要结束的时候将其清理掉即可（clearInterval(id))。    

# 浏览器渲染原理
## 浏览器渲染过程
* 步骤
  1. 根据HTML构建HTML树（DOM）
  2. 根据CSS构建CSS树（CSSOM）
  3. 将两棵树合并成一颗渲染树（render tree）
  4. Layout布局（文档流、盒模型、计算大小和位置）
  5. Paint绘制（把边框颜色、文字颜色、阴影等画出来）
  6. Compose合成（根据层叠关系展示画面）  
注：更新样式加class类不要加style样式（class类中可以包含多个样式）
## 浏览器更新样式的三种更新方式
1. JS/CSS> 样式 > 布局（Layout） > 绘制（Paint） > 合成（Compose）
2. JS/CSS> 样式 > 绘制（Paint） > 合成（Compose）  
3. JS/CSS> 样式 > 合成（Compose）  

# CSS动画的两种做法（transition和animation）
## transform
* 四个常用功能
  1. 位移 translate
  2. 缩放 scale
  3. 旋转 rotate
  4. 倾斜 skew
* 经验
一般都需要配合transition过渡  
## transition 过渡
* 作用
补充中间帧
* 语法
transition: 属性名 时长 过渡方式 延迟  
transition: left 200ms linear  
可以用逗号分隔两个不同属性  
transition：left 200ms, top 400ms  
可以用all代表所有属性
transition: all 200ms  
过渡方式有：linear(线性匀速)|ease(缓动)|ease-in（淡入）|ease-out（淡出）|ease-in-out（淡入淡出）|cublic-bezier|step-start|step-end|steps  
* 并不是所有属性都能过渡
display:none => block无法过渡  
一般改成visibility:hidden =>visible(没有为什么 )  
## animation(动画)
* 缩写语法
animation: 时长| 过渡方式 | 延迟 | 次数 | 方向 | 填充模式 | 是否暂停 | 动画名  
时长：1s或者1000ms  
过渡方式：跟transition取值一样  
次数：3或者2.4或者infinite（无限次）  
方向： reverse（反过来） | alternate（交替的） | alternate-reverse  
填充模式： none | forwards | backwards | both  
是否暂停： paused | running  
以上属性都有对应的单独属性
* keyframes完整写法(标准写法：一种是百分数另一种是from to)
```
@keyframes xxx {
 0% { top: 0; left: 0; }
 30% { top: 50px; }
 68%,72%% { left: 50px; }
 100% { top: 100px; left: 100%}
}
```
```
@keyframes yyy {
  from {
    transform: translateX(0%)
  }
  to {
    transform: translateX(100%)
  }
}
```
绝对居中代码
```
  position: absolute;
  left:50%;
  top:50%;
  transform: translate(-50%,-50%)
```
inline元素不支持transform，需要先变成block
