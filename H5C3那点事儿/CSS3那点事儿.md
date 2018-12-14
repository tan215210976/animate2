># CSS3简要札记

------

​	
$$
CSS3新增加的属性有很多，但常用的不多，以下介绍的时候会推荐常用的属性
$$

## 1, 选择器

### 	属性选择器


| 选择写法                 | 释义                  | note                     |
| -------------------- | ------------------- | ------------------------ |
| .list[attr=val]      | 获取属性为当前值的那个元素       | 如果是HTML5自定义属性，属性要加上data- |
| **.list[attr*=val]** | **获取属性值包含val的那个元素** | 多个，一般用来设置一些公共样式，常用       |
| .list[attr^=val]     | 获取属性值以val开头的那个元素    |                          |
| .list[attr$=val]     | 获取属性值以val结束的那个元素    |                          |
| .list[attr]          | 获取拥有该属性那个元素         |                          |

​	例：

```css
li[data-index="2"] {
	color: red;
	font-size: 20px
}
```



### 	伪类选择器


​	在做锚链接跳转的时候，当前跳转到的那个目标元素被选中

```css
li:target {
	color: red;
}
```



### 	结构伪类选择器 - ★★★★★


​	结构伪类的描述都是基于父盒子来说明的

| 选择方法                                     | 释义                | note |
| ---------------------------------------- | ----------------- | ---- |
| li:first-child  /  ul  :first-child      | 找到当前ul中的第一个子盒子    | 不常用  |
| li:first-of-type  /  ul  :first-of-type  | 找到父元素中第一个该类型的子盒子  | 常用   |
| li:last-child  /  ul  :last-child        | 找到当前ul中的最后一个子盒子   | 不常用  |
| li:last-of-type  /  ul  :last-of-type    | 找到父元素中最后一个该类型的子盒子 | 常用   |
| li:nth-child()    /  ul  :nth-child()    | 找到指定的第几个子盒子       | 不常用  |
| **li:nth-of-type()   /   ul   :nth-of-type()** | 找到指定的符合类型的第几个盒子   | 非常常用 |
| **li:nth-last-of-type()    /    ul    :nth-last-of-type()** | 从最后往前找第几个符合元素的    | 常用   |

​	这里括号里面的用法分别有以下几种

1. 传入number，代表指定的第几个，**不存在从0开始**，写几就是几

2. 传入奇偶的单词，even代表偶数，odd代表奇数

3. 传入倍数，例如2n

4. 传入倍数减值，能获取到元素的任意一列，

   ​	eg：比如一行7个元素，有6行，想选中第5列，就可以写成 7n-2

   ```css
   li:nth-of-type(7n-2) {
   	background-color: red;
   }
   ```

5. 传入-n减值获取头几个，或者最后的几个，**n的值从0开始**

   ​	eg，如果想获取到最后的几个，就可以使用 nth-last-of-type(-n +5)

   ```css
   li:nth-of-type(-n+7) {
     	background-color: red;
   }
   ```




---



   ## 2, 伪元素的使用 - ★★★★★

   > ::before
   >
   > ::after

   使用说明：

   - 普通元素都可以写伪元素，表现为当前盒子的**子元素**，除了表单元素
   - 伪元素**必须写入content属性**
   - 伪元素默认是**行内元素**，需要转换显示模式以设置大小，如果有浮动或者定位则自动转换
   - 使用场景： 清除浮动，设置字体图标，设置小装饰性的背景图

   ```css
   /* 清除浮动 */
   .clearfix::before,
   .clearfix::after {
     	content: "";
     	display: table;
     	visibility: hidden;
   }
   .clearfix::after {
     	clear: both;
   }
   ```

   ```css
   /* 设置字体图标 */
   .iconfont {
     	font-family: "iconfont";
   }
   .shopping-car::after {
     	content: "\e420";
   }
   ```

   ```css
   /* 设置小盒子的背景 */
   .box::after {
     	content: "";
     	position: absolute;
     	top: 0;
     	left: 0;
     	width: 20px;
     	height: 20px;
     	background: red;
   }
   ```



---



## 3, 颜色的表示方式 - ★★★★★

| 颜色表示方式                     | 常用值                                      |
| -------------------------- | ---------------------------------------- |
| 颜色名词                       | red / orange / yellow / green / blue / purple / pink / gray / navy / hotpink / yellowgreen |
| rgb(0, 0, 0)               | rgb(255, 0 , 0) -- 红色 / rgb(0, 255, 0) -- 绿色  /  rgb(0, 0, 255) -- 蓝色 |
| 十六进制                       | #e92322  /  #f40  /  #ccc  /  #fff  /  #000  -- 如果遇到aabbcc的模式，就可以写成 #abc |
| **rgba(0, 0, 0, .3)**      | 第4个值设置背景的透明，取值范围0-1， 一般把0.5写成 .5         |
| hsl(30deg, 100%, 50%)      | 参数1：颜色角度 0~360,单位是deg，参数2：饱和度，推荐100%，0%是灰色，参数3：明度，推荐是50%，100%是白色，0%是黑色 |
| hsla(45deg, 100%, 50%, .6) | 同上                                       |

![1001454N0_0](/images\1001454N0_0.jpg)

以下写法

```css
/* 颜色的表示方式 */
.box {
  	/* background-color: red; */
  	/* background-color: #f40; */
  	/* background-color: rgb(240, 12, 14); */
  	/* background-color: rgba(200, 0, 0, .6); */
  	/* background-color: hsl(30deg, 100%, 50%); */
  	/* background-color: hsla(120deg, 100%, 50%, .2); */
}
```

###	 	关于透明度设置的区别

```css
.box {
  	opacity: 0;
  	/* 这个属性会将盒子内容所有的元素变成透明 */
  	background-color: rgba(20, 20, 20, .4);
  	/* 这才是设置背景半透明 */
}
```



---



## 4, 文本阴影

```css
.box {
  	/* text-shadow: v h blur color;  x偏移 y偏移 模糊值 颜色 （前3个的单位都是px）*/
  	text-shadow: 2px 2px 2px rgba(0, 0, 0, .6);  /* 多个阴影使用逗号隔开 */
}
```

​	**文本阴影的使用场景较为少见，使用起来也比较简单**



---



## 5, 盒模型 - ★★★★

​	an: 	正常来讲，如果给一个元素添加padding内边距和边框，会使盒子变大，所以需要手动去减；

​		也就是说，盒子默认以content-box计算宽高，其他的值都是额外的，那么如果不想手动去减值怎么办？

​	使用这个属性：

```css
.box {
  	width: 200px;
  	height: 200px;
  	padding：20px;
  	border: 10px solid #ccc;
  	/* 让当前的盒子以边框计算单位，那么设置后，content内容将自动缩减 */
  	box-sizing: border-box;
}
```



---



## 6, 圆角 - ★★★

​	关于圆角的设置有几种常见的方式

```css
.box {
  	/* 在正方形的情况下，设置50%，会使当前盒子变成一个圆形 */
  	border-radius: 50%;
  	/* 如果写1个值的情况 -- 4个角都有10px的圆角 */
  	border-radius: 10px;
  	/* 如果写2个值的情况 -- 左上角和右下角 、 右上角和左下角 */
  	border-radius: 10px 20px;
  	/* 如果写3个值的情况 -- 左上角、 右上角和左下角、 右下角 */
  	border-radius: 10px 20px 30px;
  	/* 如果写4个值的情况 -- 左上角、 右上角、 右下角、 左下角 */
  	border-radius: 10px 20px 30px 40px;
}
```



---



## 7, 盒子阴影 - ★★

```css
.box {
  	/* box-shadow: v h blur size color inset; 
  				x轴偏移 y轴偏移 羽化值 扩展值 颜色 内阴影 */
  	box-shadow: 2px 2px 3px 12px rgba(0, 0, 0, .3) inset;
  	/*
  		1, 扩展值可以不写，如果是外阴影，也就是投影，不需要写值，内阴影需要加inset
  		2，如果需要添加多组阴影，通过逗号隔开
  		3，使用阴影的时候，颜色的值要尽可能的轻，太明显的投影显得太抢戏
  	*/
}
```

![shadow](images\shadow.jpg)



---



## 8, 渐变 

#### 	线性渐变 -  ★★  


```css
.box {
  	/* background-image: linear-gradient(to 方向名词[或者角度deg], 颜色 位置[百分比], ...); */
    background: #1bcdae;
  	/* 如果不支持渐变，就显示纯色 */
    background: -webkit-gradient(linear, left top, left bottom, from(#6dd27c),to(#1bcdae));
  	/* 兼容浏览器的写法 */
    background: linear-gradient(180deg, #6dd27c, #1bcdae);
  	/* 简洁的渐变使用方式 */
}
```

![gradient](images\gradient.jpg)

#### 	径向渐变


```css
.demo {
  	/* ackground-image: radial-gradient(形状 大小 位置, 颜色 状态, ...); 
  		形状：circle[圆形]  / ellipse[适应形状大小]
  		大小：closest-side | closest-corner | farthest-side | farthes-corner
  		位置：at 方向名词[top/left/bottom/right] 方向名词  |  at 数值px 数值px
  	*/
  
	width: 300px;
	height: 300px;
	border-radius: 50%;
	background-image: radial-gradient(circle farthest-corner at 75px 75px, #fff 0%, #666 100%);
}
```

![ball](images\ball.jpg)

#### 		重复渐变语法不变，在前面加上repeating-开头



---



## 9, 背景background - ★★★★★

​	关于背景的分支属性有如下

```css
.box {
  	/* 背景颜色 */
  	/* background-color: red; */
  	/* 背景平铺 */
  	/* background-repeat: no-repeatimage / repeat / repeat-x / repeat-y; */
  	/* 背景图片 */
  	/* background-image: url(../images/XXX.jpg); */
  	/* 背景位置 */
  	/* background-position: x y;  精灵图都是负值 */
  	/* 背景吸附 */
  	/* background-attachment: fixed;  当前盒子的背景去到浏览器的左上角 */
  	
  	/* 背景大小
  	/* background-size: 宽度 高度;
  						1，百分比， 也是两个值，也是代表两个方向，单位是百分号
  						2，两个值， 分别代表水平和垂直方向， 注意记得加px单位
  						3，contain （顾宽不顾高） cover（顾高不顾宽）
  	*/
  	
  	/* 背景显示 */
  	/* background-origin: content-box; 默认值是padding-box */
  	/* 背景裁切 */
  	/* background-clip: content-box; 默认值是padding-box */
  
  	/* 多张背景图片中间使用逗号隔开 */
  	/* 滤镜的效果需要一张图，逗号，一个颜色 */
  	/* background-blend-mode: lighten; 当前值是变亮，还有一些其他值 */
}
```

#### 	关于背景大小 background-size 的使用


1. 制作全屏背景的时候，比如全屏轮播，或者一些顶部广告图

   ```html
   问题：就是图片会很宽，因为要照顾到大多数的浏览器的宽度
   解决办法，	
   	1），使用 background-size: cover; 来解决盒子的适应
   		使用 background-position: center center; 来居中内容
   		因为主体的才是信息，两边的只是为了在宽屏的时候不会留白
   	2），当前的图片还是正常居中，或者是个没那么宽的图片，
   		两边通栏的盒子，使用背景颜色，这个颜色一定要和图片的边缘部分一样
   ```

   ```css
   .box {
     	width: 100%;
     	height: 450px;
     	background: url(../images/ctrip.jpg) no-repeat;
     
     	-webkit-background-size: cover;
     	background-size: cover;
     	background-position: center center;
   }
   ```

![img](file://psf/Home/Desktop/CSS3%E9%82%A3%E7%82%B9%E4%BA%8B%E5%84%BF/images/ctrip.jpg?lastModify=1541515376)

2.当制作移动端的2倍图或者3倍图的时候，并且使用的是精灵图

```html
问题：假如图片是1000 x 1000 设计稿中的盒子是50 x 50
解决办法，
	1），使用 background-size: 这里的值应该是当前宽度或者高度除以2或者3
		假如2倍图，当前图片是748*256, 这里设置的值，就应该是 374px auto
	2），由于使用精灵图用的是background-position，那么当前的位置也应该发生变化
		假如2倍图，当前精灵图的位置是 -248px -126px
		那么当前的位置就应该改成 -124px -63px
```


![2size](images\2size.jpg)

---



## 10, 过渡 transition - ★★★★★

#### 过渡的属性列表

| 属性分支                               | 取值                          | note                |
| ---------------------------------- | --------------------------- | ------------------- |
| transition-property  /  属性         | wdith / all                 | 必须要有具体值的属性，不能是显示状态  |
| transition-duration  /  耗时         | 2s /  .5s                   | 整数或者小数，单位是s（秒）      |
| transition-timing-function /  运动函数 | linear / 贝塞尔曲线  /  steps(3) | 三种取值方式，根据需求用一种，不能重复 |
| transition-delay  /  延迟            | 2s                          | 延迟一般用在多个盒子上按个走      |



#### 案例如下

```css
.box {
  	width: 200px;
  	height: 200px;
  	background-color: red;
  	position: absolute;
  	top: 0;
  	left: 0;
  
  	/* 设置过渡属性在盒子本身，而不是其他的状态 */
  	transition: left 2s ease-in 0s;
  	/* 			过渡属性可以直接写成all */
  	/*
  		1，平常在设置过渡的时候，不会按分支去写，而是按照连写的方式
  		2，当延迟为0s的时候，可以不写，
  		3，默认的运动方式是ease，匀速叫做linear
  	*/
}

.box:hover {
  	left: 200px;
}
```



---



## 11, 转换 transform

> ###   2d转换  |  3d转换

​	2d转换4个属性，3d转换3个属性和几个必须属性

#### 2d转换 - ★★★★★

​	1， 位移 translate(x, y)

```css
.box {
  	width: 200px;
  	height: 200px;
  	background: red;
  	/* 刚开始学习很多人会搞混这几个单词，以下这个叫过渡，跟转换没有关系 */
  	transition: transform 2s linear;
}
.box {
  	/* 默认是x轴位移200px */
	/* transform: translate(200px); */
  	/* 两个值代表x，y两个方向   向右，向下 */
  	transform: translate(200px, 200px); 
  	/* 单独写的话，方向要大写 */
  	/* translateX(200px) / translateY(200px) */
}
```

​	![translate](images\translate.jpg)

​	2，旋转 rotate(30deg)

```css
.box {
  	width: 200px;
  	height: 200px;
  	background: red;
  	transition: transform 2s linear;
}
.box {
  	/* 默认是Z轴旋转120deg */
  	transform: rotate(120deg); 
}
```

![rotate](images\rotate.jpg)

​	3，缩放 scale(1.05)

```css
.box {
  	width: 200px;
  	height: 200px;
  	background: red;
  	transition: transform 2s linear;
}
.box:hover {
  	/* 水平方向拉伸 */
  	/* transform: scaleX(1.05); */
  	/* 垂直方向拉伸 */
  	/* transform: scaleY(1.05); */
  	/* 默认是水平和垂直方向同时拉伸，但是不会太多 */
  	transform: scale(1.05);
}
```



​	4，斜切 - skew(45deg)

```css
.box {
  	width: 200px;
  	height: 200px;
  	background: red;
  	transition: transform 2s linear;
}
.box:hover {
  	/* 水平方向拉伸 */
  	/* transform: scaleX(1.05); */
  	/* 垂直方向拉伸 */
  	/* transform: scaleY(1.05); */
  	/* 默认是水平和垂直方向同时拉伸，但是不会太多 */
  	transform: scale(1.05);
}
```

![skew](images\skew.jpg)



#### 3d转换

​	1，位移3d translate3d(10px, 10px, 10px)

​	设置值的时候与2d没有区别，最后一个为z轴，正常看不出来效果

​	如果需要看出近大远小的效果，需要加入 ***视距***

##### **视距 perspective**

​	网页中，默认是二维空间，也就是说，所有的盒子都是在平面的网页上，所以设置z轴的位移，根本没有什么卵用，而当网页设置视距，则计算机会模拟景深的效果，设置z轴的位移就有近大远小的效果

```css
body {
  	/* 视距给父盒子设置，紧紧包着的父盒子 */
  	perspective: 500px;
  	/* 兼容写法 */
  	-webkit-perspective: 500;
}
.box {
  	width: 200px;
  	height: 200px;
  	background: red;
  	transition: transform 2s linear;
}
.box:hover {
  	/* 给父元素设置完视距后，改变元素的z轴方向，元素变大了 */
  	transform: translate3d(0, 0, 200px);
}
```



![translate3d](images\translate3d.jpg)



​	2，旋转 rotate3d(1, 2,1, -45deg)

​		与其他3d属性不同，设置它需要4个值，前三个都是向量不带单位，最后一个是角度

​	<u>**向量值： 当前轴的比例值，没有实际意义，就比如 1：1：1 和10：10：10一样**</u>

​	一般让拥有3d效果元素的父盒子旋转

```css
.box {
  	width: 200px;
  	height: 200px;
  	background: red;
  	transition: transform 2s linear;
}
.box:hover {
  	/* X轴旋转角度 */
  	/* transform: rotateX(30deg); */
  	/* Y轴旋转角度 */
  	/* transform: rotateY(30deg); */
  
  	/* 旋转的3d属性 */
  	transform: translate3d(0, 0, 200px);
}
```



![rotate3d](images\rotate3d.jpg)

​	在网页中，如果设置子元素旋转可以遵循左手法则

​	注意，在网页中x轴正值朝右，y轴正值朝下，z轴正值朝向自己

![lefthand](images\lefthand.jpg)

##### 保留元素的3d样式 transform-style

​	在网页元素中，无法看出元素旋转和位移的3d效果，此时需要给父元素设置属性

```css
ul {
  	width: 500px;
  	height: 500px;
  	
  	/* 让子盒子保留3d样式， 或者说将网页处于3d视角中 */
  	transform-style: preseve-3d;
}
li {
  	width: 200px;
  	height: 200px;
  	background: red;
  		
  	/* 设置元素向下位移，并且x轴旋转90deg */
  	transform: translateY(200px) rotateX(90deg);
}
...
```



![3dbox](images\3dbox.jpg)



​	3，缩放 scale3d(1, 1, 1.5)

​	3d的缩放难以展示和调试，表现形式难以调整成想象的样式，较为抽象，所以不怎么用



---



## 12, 动画  animation - ★★★★★ 

​	请问过渡和动画的区别是什么？

过渡：

 - 过渡只能实现一个状态到另外一个状态的变化
- 过渡的效果只能执行一次
- 过渡需要保持某个类名或者状态，否则会还原

动画：

- 动画能实现多个关键帧的连续变化
- 动画的播放次数能重复多次
- 动画能在播放的过程中停止
- 动画能主动停止在结束的那个关键帧



​	动画的声明 - @keyframes

```css
@keyframes donghua {
  	0% { 
      	/* 这里的0%可以替换为from， 或者没有变化的时候，不用写 */
      	/* 这里可以设置元素的初始状态 */
      	transform: translate(-50%, -50%);
      	opacity: 0;
  	}
  	100% {
      	/* 这里的100%可以替换为to */
      	/* 期间可以设置无限个关键帧，比如20% , 24.5%, 87.3% */
      	opacity: 1;
      	transform: translate(-50%, -50%) rotate(90deg);
  	}
}
```

​	相当于js中的函数，需要先声明，再引入

​	引入的属性名称为 animation

| 属性                        | 描述                                       |
| ------------------------- | ---------------------------------------- |
| @keyframes                | 定义动画，固定的语法，类似于函数声明                       |
| animation                 | 简写属性，除了 animation-play-state属性，这个最为常用    |
| animation-name            | 动画名称，每一个动画都有名称                           |
| animation-duration        | 规定动画完成的时间，单位是秒s                          |
| animation-timing-function | 规定动画的速度曲线，默认是“ease“   可以替换为贝塞尔曲线，或者steps() |
| animation-delay           | 规定动画的延时时间，单位是秒s                          |
| animation-iteration-count | 规定动画执行的次数，默认是一，无限循环是 ”infinite“          |
| animation-direction       | 规定动画是否逆向，默认不会，设置值为”alternate“            |
| animation-play-state      | 改变动画执行状态，默认是”running“， 暂停”paused“        |
| animation-fill-mode       | 规定动画起始或者结束的状态，forwords / backwords       |

​	

```css
.box {
  	/* animation: 动画名称  执行时间 速度曲线 延迟时间 播放次数 是否逆向 开始或结束的状态 */
  	animation: donghua .4s ease-in 0s infinite forwords;
}
```



​	关于动画的补充案例，《北极熊奔跑》、《阴阳师f4》、《beats按钮》...  都是线上写的比较多的一些用法，知识点都是死的，要学会灵活运用

​	** 动画可以多组，也可以采用给父盒子和子盒子分别设置动画的方式



---



## 13, web字体 和 字体图标

> web字体和字体图标是两回事。

#### web字体

​	使用web字体能够改变网页中部分文字显示的更加优雅，令主题突出留下深刻印象

[阿里字体]: http://iconfont.cn/webfont?spm=a313x.7781069.1998910419.d81ec59f2#!/webfont/index
[有字库]: https://www.youziku.com/

 - 正常来说，所有的字体文件，都是在电脑C盘windows文件夹fonts里面，所以为了保证所有的用户都能正常浏览网页，一般不会随意改变字体，


 - 前端任何一门技术，都不能帮用户的电脑设置字体，所以为了一致性，不会使用一些特殊的字体


 - 而移动端所谓的设置字体，都是更改手机设置内部的字体，而并非是网页


 - 在网页中，可以使一些量较少的文字，设置成其他的字体样式

使用流程：

​	在专门的网站上，编辑需要改变的文字，下载对应的文件或者生成链接

```css
/* 声明字体文件, 注意路径 */
@font-face {
	font-family: 'shuangyuan'; /* 这里的文字可以随意更改 */
	src: url('../fonts/webfont.eot'); /* IE9*/
	src: url('../fonts/webfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
 	url('../fonts/webfont.woff') format('woff'), /* chrome、firefox */
	url('../fonts/webfont.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
	url('../fonts/webfont.svg#webfont') format('svg'); /* iOS 4.1- */
}
/*定义一个样式，使用自定义的web字体*/
.myFont{
	font-family: shuangyuan; /* 这里使用的字体，一定要和上面声明的保持一致 */
}
```

在某段文字中，使用该类名

```html
<h1 class="myFont" id="hotPro">热门商品</h1>
```

![fonts](images\fonts.jpg)

或者使用在线的文件, 参考使用流程

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<link href='http://cdn.webfont.youziku.com/webfonts/nomal/106575/45836/5be13ba2f629d81b9c9d8c38.css' rel='stylesheet' type='text/css' />
</head>
<body>
	<h2 class="css158cfa3a2a1a04f">热门商品</h2>
</body>
</html>
```



#### 字体图标 - ★★★★★

​	网页元素中，一些小的装饰性的图标，都会采用精灵图或者字体图标来做，字体图标是矢量的，也就是说放大和缩小不会显示丢精度或者变模糊

[阿里图标库]: http://iconfont.cn/home/index?spm=a313x.7781069.1998910419.1.pCxKlU
[icomoon]: https://icomoon.io/
[awesome]: http://www.fontawesome.com.cn/

​	比较推荐的用法是使用阿里图标库，这里有成千上万的图标，单色多色可供使用，使用中文、英文、拼音检索都可以找到想要找到的图标；

使用流程：

​	1，根据设计师给出的图稿，挑选合适的图标，注意风格样式，要尽可能统一，边框就是边框，纯色就是纯色，不要因为视觉效果自己随意搭配；

​	2，点击加入到购物车，登录账号之后，加入到自己的项目中，没有项目就新建一个项目，

​	3，在项目中下载文件压缩包，

![icon](images\icon.jpg)



下载完之后，解压得到如下文件

![iconFile](images\iconFile.jpg)

```html
<!-- 在html中使用图标的方式很简单，按照使用文档说明 -->
<!-- <div class="声明字体的类名 图标本身的类名"></div> -->
<div class="iconfont shopping-cart"></div>
```



---



## 14, flex布局

> 要使用flex布局，一定要给父盒子加上 **<u>*display: flex;*</u>** 属性

在flex布局中，无非就是给父盒子和子盒子设置的属性，并且常用的属性并不多

- 父盒子加上了 display: flex; 子盒子就类似有了浮动，会到一行上来，并且不脱标
- 子盒子默认不会换行，一行排不下的时候，会自动缩减宽度
- flex布局可以嵌套，一般来说，如果只有单独的盒子，不建议使用
- 父盒子主要设置排列方向，子盒子主要设置分配空间



#### 父盒子的属性

| 属性                  | 描述                    | 常用值类型                   |
| ------------------- | --------------------- | ----------------------- |
| display             | 转换父盒子的显示模式            | flex                    |
| justify-content     | 设置主轴的排列方式，默认主轴就是横着的方向 | center / space-between  |
| flex-flow           | 综合属性，代表方向和排列轴两个       | flex-flow: wrap normal; |
| ---- flex-wrap      | 是上一个的分支属性, 代表是否换行     | wrap / nowrap           |
| ---- flex-direction | 设置主轴方向，默认横着向右，就是横轴    | row 行 / column 列        |
| align-items         | 设置侧轴方向，一般为居中          | center                  |



![flex](images\flex.jpg)

#### 给子盒子设置的属性

| 属性          | 描述         | 值        |
| ----------- | ---------- | -------- |
| flex-grow   | 分配父盒子剩余空间  | 常用       |
| flex-shrink | 缩减父盒子不够的空间 | 适合做响应式   |
| flex-basis  | 默认值是auto   | 不常用      |
| align-self  | 设置侧轴排列方式   | center常用 |



---



## 15, 扩展

> ​	关于CSS3，线上有很多的框架和插件来解决平时我们遇到的一些问题，不过学习不完，而且并不是所有的需求都能遇到；

- animate.css

  封装了元素运动的各种方式，下载文件后，引入文件，添加类名即可

- fullpage

  可以在github.io网站中找到星星数量最多的项目，并且官网提供了阅读文档，可以选择中文

  - 新版的需要收费，课程内另外发的是上一版的文件，不收费，方法都通用，
  - 使用fullpage可以解决全屏滚动的案例，基于jquery的插件
  - 使用fullpage的时候，注意要按照其格式来操作
  - fullpage提供了丰富的属性、事件和方法可供调用

- stealler.js

  - 这个插件可以使网页元素的背景或者元素，在页面滚动的时候缓慢行走，形成落差效果





