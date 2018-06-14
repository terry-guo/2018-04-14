# 一，常用单位

**1、px：**绝对单位，页面按精确像素展示

**2、em：**相对单位，基准点为父节点字体的大小，如果自身定义了font-size按自身来计算（浏览器默认字体是16px），整个页面内1em不是一个固定的值。

**3、rem：**相对单位，可理解为”root em”, 相对根节点html的字体大小来计算，CSS3新加属性，chrome/firefox/IE9+支持。//（ 是截止目前用的最多也是最流行的）

  	在移动端中利用rem的相对于根HTML进行改变，通过一段JS实现了移动端自适应，本文则使用纯CSS视口单位来自行自适应，虽然现在的兼容性还没法完全能够接受，但不妨碍你认识这个vw和vh的强大。

​	响应式布局的实现依靠媒体查询（ Media Queries ）来实现，选取主流设备宽度尺寸作为断点针对性写额外的样式进行适配，但这样做会比较麻烦，只能在选取的几个主流设备尺寸下呈现完美适配。

​	即使是通过 rem 单位来实现适配，也是需要内嵌一段脚本去动态计算根元素大小。

近年来，随着移动端对视口单位的支持越来越成熟、广泛，使得我们可以尝试一种新的办法去真正地适配所有设备尺寸。

4、百分比（%）

**5、vw、vh、vmin、vmax** 主要用于页面视口大小布局，相对于rem;v*在页面布局上更加方便简单

​	vw：viewpoint width，视窗宽度，1vw等于视窗宽度的1%。
	vh：viewpoint height，视窗高度，1vh等于视窗高度的1%。
	vmin：vw和vh中较小的那个。
	vmax：vw和vh中较大的那个。

兼容性：**vw, vh, vmin, vmax：IE9+局部支持，chrome/firefox/safari/opera支持，ios safari 8+支持，android browser4.4+支持，chrome for android39支持**

![0](.\images\a1.png)



# 二、认识视口单位（ Viewport units )

​	在桌面端，视口指的是在桌面端，指的是浏览器的可视区域；

  	而在移动端较为复杂，它涉及到三个视口：分别是 Layout Viewport（布局视口）、 Visual Viewport（视觉视口）、Ideal Viewport。

​	而视口单位中的“视口”，在桌面端，毫无疑问指的就是浏览器的可视区域；但是在移动端，它指的则是三个 Viewport 中的 Layout Viewport 。

![0](.\images\a2.jpg)



根据CSS3规范，视口单位主要包括以下4个：[·](http://caibaojian.com/vw-vh.html)

- vw : 1vw 等于视口宽度的1%
- vh : 1vh 等于视口高度的1%
- vmin : 选取 vw 和 vh 中最小的那个
- vmax : 选取 vw 和 vh 中最大的那个

**视口单位区别于%单位，视口单位是依赖于视口的尺寸，根据视口尺寸的百分比来定义的；而%单位则是依赖于元素的祖先元素。**

![0](.\images\a3.jpg)

用视口单位度量，视口宽度为100vw，高度为100vh（左侧为竖屏情况，右侧为横屏情况）