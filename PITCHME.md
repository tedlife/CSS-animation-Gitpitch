# CSS 动画实例

---

## Transition

transition 顾名思义“过渡”，动画的形成，过渡显然是必须的。它的使用语法：

```css
transition: <property> <duration> <timing-funciton> <delay>;
```

---

其中：

* <property> 默认值：all
* <timing-funciton> 默认值：ease
* <delay> 默认值：0
* 可以同时写多组 transition，它们之间用英文逗号隔开

---

另外，注意不是所有的 CSS 属性都支持 Transition，比如 `display: none;` 与 `display: block` 之间没有中间状态的，是不支持Transition 的。

---

加上前缀是考虑浏览器兼容性问题，也可以使用网站 CanIUse，后面类似问题不再赘述：

```css
-webkit-transition: all .4s; // Safari, Chrome
-moz-transition: all .4s; // Firefox
-ms-transition: all .4s; // IE
-o-transition: all .4s; // Opera
transitian: all .4s;
```

---

### transition 实例之背景颜色

---

HTML 部分：

```html
<a href="#" class="btn"></a>
```

---

CSS 部分：

```css
.btn {
	background-color: #00a0d6;
	color: #fff;
	transition: background-color .4s;
}

.btn:hover {
	background-color: #007da7;
	color; #ad7eb6;
}
```

---

### transition 实例之隐藏的按钮内容

---

HTML 部分：

```html
<section>
	<a href="#" class="btn buy-button">
		Buy Now!
	</a>
<section>
```

---

第一步，写两个 span 内联元素，来分别表示现在展示的和隐藏的按钮文字

```html
<section>
	<a href="#" class="btn buy-button">
		<span class="top content">Buy Now!</span>
		<span class="bottom content">On Sale $59</span>
	</a>
<section>
```

---

第二步，给按钮正常状态和 hover 状态加个样式

```css
.btn { position: relative; }
.content { position: absolute; }

.top { top: 0; }
.btn:hover .top { top: -100px; }

bottom { top: 100px; }
.btn:hover .bottom { top: 0; }
```

---

第三步，在正常状态和 hover 状态之间加个 transition

```css
.content {
	position: absolute;
	transition: top .3s;
}
```

---

[CSS 动画 Transition 练习](https://codepen.io/ista/pen/jwOQKO)

在上面例子的基础上，还有很多可以应用的地方，可以发挥想象力，课后小练习：应用 Transition 和 `visibility: hidden; opacity: 0;` 写一个 Modal（弹出框） 组件。

---

## Transform

transform 顾名思义“变换”，可以用来旋转（rotate），移动（translate），放大（scale）,扭曲（skew）页面元素等等。

---

### transform 实例之旋转小图标

---

HTML 部分：

```html
<a href="#" class="modal-close"><i class="fa fa-times"></i></a>
```
---

CSS 部分：

```css
.modal-close {
	transition: transform 1s;
}

.modal-close:hover {
	transform: rotate(360deg);
}
```

---

### transform 实例之移动并缩小输入框标签

---

HTML 部分：

```html
<form action="#">
  <input type="text" name="name" id="name" class="form-input" />
  <label for="name" class="form-label">姓名</label>
</form>
```

---

第一步，输入框标签文字颜色的过渡

```css
.form-input + .form-label {
	position: relative;
	color: #6a7989;
	transition: color 0.3s;
}
.form-input:focus + .form-label {
	color: #333;
}
```

---

第二步，把输入框标签文字缩小 80%，并加上过渡效果

```css
.form-input + .form-label {
	position: relative;
	color: #6a7989;
	transform-origin: center left;
	transition: color 0.3s, transform 0.3s;
}
.form-input:focus + .form-label {
	color: #333;
	transform: scale(0.8);
}
```

---

第三步，把输入框标签文字上衣到输入框上面

```css
.form-input + .form-label {
	position: relative;
	color: #6a7989;
	transform-origin: center left;
	transition: color 0.3s, transform 0.3s;
}
.form-input:focus + .form-label {
	color: #333;
	transform: scale(0.8) translateY(-40px);
}
```

[CSS 动画 Transform 练习](https://codepen.io/ista/pen/awbQQw)

---

## Keyframe

Keyframe 允许你自定义这个动画过程中的具体变化。比如说，在 25% 这个时候，改变颜色，在 50% 的这个时候，旋转 360 度。这样可以组合出，更加复杂的动画效果。

使用 Keyframe 有两个步骤：

---

第一步，创建动画过程

```css
// 语法一
@keyframes <name-animation> {
	<step 1> {<property>: <value>;}
	<step 2> {<property>: <value>;}
	...
	<step n> {<property>: <value>;}
}
// 语法二
@keyframes <name-animation> {
	from {<property>: <value>;}
	to {<property>: <value>;}
}
// 具体写法，创建一个叫 swing 的动画
@keyframes swing {
	0% {transform: rotate(0deg);}
	100% {transform: rotate(-10deg);}
}
```

---

第二步，给元素指定你创建的动画

```css
// 语法
animation: <name> <duration> <delay> <iteration> <timing-funciton>;
// 具体写法，给 arm 这个元素添加 swing 动画
#arm {
	transform-origin: top center; // 基点位置不一样，有着不同的动画效果
	animation: swing 2s 0s infinite ease;
}
```

---

### Keyframe 实例之弹出框

作为课后小挑战，对 CSS 动画感兴趣的，去做这个小挑战。

---
 
## SVG 动画

SVG 动画可以综合上面所学的 Transition、Transform 和 Keyframe 来做出很多有趣的动画，当然对 SVG 相关知识也要学习。课后有兴趣的可以 Google 探索下。

---

## 相关资源

* [自定义一个 timing-function](http://cubic-bezier.com/)
* [在 Codepen 尝试 Timing functions](http://codepen.io/alyssamichelle/pen/GJmpPb?editors=110)
* [Can I Use](http://caniuse.com/)
* [Animate.css 动画库](https://daneden.github.io/animate.css/)


