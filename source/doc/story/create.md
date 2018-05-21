title: 创建小故事
layout: doc
---

## 小故事的概念

### 小故事是什么

​	小故事是一种可交互的多媒体卡片，是由多元化内容组成的媒体形态，可带来沉浸式、多媒体、可交互的浏览体验，如图，是一个小故事的示例；

- 示例

<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/oscar5.gif" width="276" height="494" />

### 小故事产品构成

​	每个小故事（Story）下有多个段落（View），每个段落（View）可自由组合音频、视频、图片、GIF、文字等富媒体元素(Element)。

<!-- - 示例 -->

<!-- ![intro-view-layer-element (1)](http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/intro-view-layer-element.jpg) -->

### 小故事面向人群

​	小故事采用开放的[MIP技术](https://www.mipengine.org/)，能让站长、自媒体、开发者、商家等各种可以提供优质有创意内容的人群使用工具或MIP技术进行小故事创作。

​	在百度搜索结果页的呈现形式如图：

![搜索结果页展示](http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/%E6%90%9C%E7%B4%A2%E7%BB%93%E6%9E%9C%E9%A1%B5%E5%B1%95%E7%A4%BA.png)

## 起步教程

### 1. 技术储备

开发一个小故事的技术储备：

1. HTML，CSS和JavaScript的基本知识；
2. 对MIP的基础原理和规范，请参考[MIP 的开发文档](https://www.mipengine.org/doc/00-mip-101.html) ；

### 2、开发环境准备，Run起示例Demo

1、下载代码；

- 下载本教程的代码，下载地址如下：[oscar-demo](http://mipstatic.baidu.com/static/mip-static/mip-story/demo/story-demo.zip)；
- 提取zip文件的内容，减压后在story-demo目录下的oscar-story.html是完整小故事demo的入口。

2、运行示例页面

​	运行示例代码的方法如同启动MIP页面的服务，MIP 页文件可以直接运行，你可以选择如下方式，像预览普通 HTML 站点一样预览 MIP-HTML 页面：

- 直接在浏览器中打开（由于 XML HTTP Requests 失败可能会导致某些元素预览失败）。
- 在本地部署一个服务，如 Apache，Nginx 等。
	 使用 MIP-CLI 辅助预览，使用方法见 MIP 博客：[开发教程一](http://www.cnblogs.com/mipengine/p/mip_cli_1_install.html)。	

设置完本地的web服务，通过访问一下URL，可查看小故事的Demo示例：

```
http://localhost:8000/oscar-story.html
```

完成了以上准备工作，那么接下来，让我们开始开发属于你自己的小故事。

## 小故事的组织结构介绍

​	小故事主要由 [mip-story 组件](/examples/mip-extensions/mip-story.html) 承载，充当小故事中所有段落的容器，按照段落个数自动生成段落导航，返回链接，段落播放完的重播和分享功能。

小故事具有三个基本概念：段落（view），层（layer）和元素（element）.

- 每个小故事可以包含多个段落（view），每个段落充满屏幕。用户操作翻页后，会看到下一个段落。
- 每个段落又可以包含多个层（layer），单个层可以设置布局模式，如多行布局，左右布局，图片拉伸布局等。
- 元素（element）是资源素材，如背景图，主标题，详细描述等。在 `<h1>`、`<p>`、`<mip-img>` 等标签中声明。

![intro-view-layer-element (1)](http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/intro-view-layer-element.jpg)

​	这里的每一个组件都是一个mip组件，其中故事组件为`mip-story`，段落为`mip-story-view`，层为`mip-story-layer`，元素为资源素材，如背景图，主标题，详细描述等。在 `<h1>`、`<p>`、`<mip-img>` 等标签中声明。

![mip-story-tag-hierarchy](http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/demo-story1.png)

## 开发小故事

开发一个小故事，只需要简单的三部：

1. 创建封面以及段落；
2. 为段落添加丰富内容；
3. 为小故事添加封底；

下面请跟随详细步骤教程开始制作你的第一个小故事吧！

​	小故事由`mip-story`组件表示，它作为故事中所有页面的容器。该`mip-story`组件还负责创建UI外壳，包括处理手势和导航。

​	`mip-story`组件是一个自定义的MIP组件，与所有自定义组件一样，您必须要将该组件的关联脚本添加到MIP文档；在一个标准的 [MIP HTML 页面](https://www.mipengine.org/doc/01-mip-demo.html)的`<script>`标签中添加依赖脚本：

```html
<!DOCTYPE html>
<html mip>
<head>
    ....
</head>
<body>
    <!-- MIP 运行环境 -->
    <script src="https://c.mipcdn.com/static/v1/mip.js"></script>
    <!-- 小故事依赖脚本 -->
    <script src="https://c.mipcdn.com/static/v1/mip-share/mip-share.js"></script>
    <script src="https://c.mipcdn.com/static/v1/mip-story/mip-story.js"></script>
    <script src="https://c.mipcdn.com/static/v1/mip-stats-baidu/mip-stats-baidu.js"></script>
    <script src="https://c.mipcdn.com/static/v1/mip-scrollbox/mip-scrollbox.js"></script>
</body>
</html>
```

​	添加好依赖后，需要把`mip-story`元素添加到`<body>`文档中，如下所示：

```html
<!DOCTYPE html>
<html mip>
<head>
    ....
</head>
<body>
    <!-- 组件使用 -->
    <mip-story id="story-demo">
       ...
    </mip-story>
    <!-- MIP 运行环境 -->
    <script src="https://c.mipcdn.com/static/v1/mip.js"></script>
    <!-- 小故事依赖脚本 -->
    <script src="https://c.mipcdn.com/static/v1/mip-share/mip-share.js"></script>
    <script src="https://c.mipcdn.com/static/v1/mip-story/mip-story.js"></script>
    <script src="https://c.mipcdn.com/static/v1/mip-stats-baidu/mip-stats-baidu.js"></script>
    <script src="https://c.mipcdn.com/static/v1/mip-scrollbox/mip-scrollbox.js"></script>
</body>
</html>
```

​	在此需要重点注意的是，要想获得有效的MIP故事，在`<body>`元素中必须只有一个`<mip-story>`组件，所有其他元素（除`<script>`中添加的依赖）都要包含在`<mip-story>`组件中。

​	在完成以上工作，我们拥有了一个小故事的外壳，但是此时的故事是无效，因为它需要有一个段落，那么接下来让我们创建该段落。



## 小故事的封面的开发介绍

###1、在`mip-story`中添加一个封面

​	MIP小故事中的页面由`<mip-story-view>`组件表示。在一个`<mip-story>`，你可以有一个或多个`<mip-story-view>`组件，包含故事的每个单独的屏幕。您在开发一个小故事时候，第一页是显示在故事的第一页。要创建该页面，请将`<mip-story-view>`组件**添加**到`<mip-story>`。为页面**分配**一个唯一的ID。对于封面，分配唯一的ID `cover`：

```html
<mip-story id="story-demo">
    <mip-story-view>
        ...
    </mip-story-view>
</mip-story>
```

​	现在我们有了我们封面的外壳。但是，我们的故事仍然无效。在我们的页面中，我们需要指定至少一个**图层**。

### 2、在封面中添加一个图层

​	像下图中的图层一样，您可以在MIP故事页面中使用图层来创建视觉效果。层层叠在一起，因此，第一层是底层，下一层在顶层，依此类推。

我们的封面实际上由两层组成：

- **第1层**：用作背景的图像
	 **第2层**：故事的标题和副标题	

<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/story-layer.png" width="350" height="494" />

##### 2.1 创建第一层

​	我们将第一层添加到封面上。该图层包含填充屏幕的图像。

​	通过将`<mip-story-view>`元素添加为子元素来创建图层`<mip-story-layer>`。由于是封面，我们希望图像填充屏幕，可以设置`<mip-story-layer>`中的`template`属性为`fill`，指定该`template="fill"`。在图层内部，`<mip-img>`为`cover.jpg`文件添加一个元素，并确保它对`layout="responsive"`图像尺寸为720 x 1280像素的响应（即）。以下是我们的图层：

```html
<mip-story>
    <mip-story-view>
        <mip-story-layer template="fill">
            <mip-img src="cover.jpg"></mip-img>
        </mip-story-layer>
    </mip-story-view>
</mip-story>
```

​	通过以上代码，可以实现封面的显示，它的图形化界面如下：


<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/cover-0.png" width="276" height="494" />

##### 2.2 创建第二层

​	在完成第一层的情况下，我们开始完成第二层，它在背景之上，包含主标题和副标题。要添加第二层，首先需要完成与第一层相同的任务，但是此处的`template`不使用`fill`模板，此处我们使用`vertical`模板。

​	大家肯定会对`template`属性很迷惑，这个属性到底是干啥的，都有什么取值，为什么封面需要使用`fill`模板，那么接下来，我们了解下`template`属性的简单用法；`template`属性是`<mip-story-layer>`组件的一个属性，用来设置该层的整体布局结构；

- `template`属性

  - `template="fill"`：填充布局，该布局方式会将当前 `<mip-story-layer>` 中的第一个元素进行填充布局，其他元素均隐藏。适合于将图片、视频作为背景展示的场景。如图：

    ```html
    <mip-story-layer template="fill">
        <mip-img src="cover.jpg)"></mip-img>
    </mip-story-layer>
    ```

	<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/cover-2.png" width="276" height="494" />

  - `template="vertical"`：`<mip-story-layer>` 中的元素沿 `y` 轴排列，`x` 轴方向填充布局。

    ```html
    <mip-story-layer template="vertical">
      <p>element 1</p>
      <p>element 2</p>
      <p>element 3</p>
    </mip-story-layer>
    ```
	<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/cover-3.png" width="276" height="494" />

  - `template="horizontal"`：`<mip-story-layer>` 中的元素沿 `x` 轴排列，`y` 轴方向填充。

    ```html
    <mip-story-layer template="horizontal">
      <p>element 1</p>
      <p>element 2</p>
      <p>element 3</p>
    </mip-story-layer>
    ```

	<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/cover-4.png" width="276" height="494" />

  - `template="thirds"`：支持上中下三列布局，在使用该布局时，内部的元素需要同时加入对应的属性，包括：

    - `flex-area='upper-third'`: 元素位于三等分布局的上部；

    - `flex-area='middle-third'`: 元素位于三等分布局的中部；

    - `flex-area='lower-third'`: 元素位于三等分布局的下部；

      ```html
      <mip-story-layer template="thirds">
        <h1 flex-area="upper-third">element 1</h1>
        <p flex-area="middle-third"></p>
        <p flex-area="lower-third">element 2</p>
      </mip-story-layer>
      ```

	  <img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/cover-5.png" width="276" height="494" />

现在您已经了解一个层中的模板布局，现在让我们完成封面的第二层。

对于第二层，我们需要添加主标题和副标题，我们希望这些元素依次排列，所以使用`vertical`模板。如下：

```html
<mip-story>
    <mip-story-view>
        <mip-story-layer template="fill">
            <mip-img  layout="responsive" width="480" class="fade-in-scale" height="720" src="https://www.mipengine.org/static/img/mip-story/p1.png" layout="responsive"></mip-img>
        </mip-story-layer>
        <mip-story-layer>
            <div class="page1-wrap">
                <span>第90届奥斯卡</span>
                <span>The 90th Oscar</span>
                <span class="line"></span>
                <span>颁奖典礼回顾</span>
            </div>
        </mip-story-layer>
    </mip-story-view>
</mip-story>
```

​	刷新浏览器我们发现，我们已经开发完完整的封面。

<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/cover-6.png" width="276" height="494" />

​	在完成了小故事封面的基础上，我们需要更多的段落来丰富我们的小故事内容，以达到好的用户体验，那么接下来我们讲介绍如何[开发更丰富的段落内容]()。


## 小故事段落的开发介绍

​	现在您已经熟悉了如何在MIP故事中添加一个段落，如我们在创建小故事封面中所提到的一样。接下来将讲解如何创建剩余的页面。

- 使用单层

   添加新的一个段落，在单个图层中显示图片和文字。

   包含一层，布局为`vertical`，包含三个元素：标题、图片、副标题。

	```html
	<mip-story>
		<mip-story-view>
			<mip-story-layer template="vertical">
				<!-- 主标题 -->
				<div class="common-wrap">山姆·洛克威尔</div>
				<mip-img layout="responsive" width="1242" height="1665" src="./static/p5.png"></mip-img>
				<!-- 副标题 -->
				<div class="common-wrap-1">
					<span></span>
					<span>最佳男配角</span>
					<span>主演：三块广告牌</span>
				</div>
			</mip-story-layer>
		</mip-story-view>
	</mip-story>
	```

	<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/vertical-0.png" width="276" height="494" />

- 使用双层

  添加两层，文本并联排列。

  ```html
  <mip-story>
      <mip-story-view>
          <mip-story-layer template="fill">
              <mip-img layout="responsive" width="480" height="720" src="https://www.mipengine.org/static/img/mip-story/p6.png"></mip-img>
          </mip-story-layer>
          <mip-story-layer template="thirds" class="common-wrap-2">
              <div flex-area="upper-third">艾莉森·珍妮</div>
              <div flex-area="middle-third"></div>
              <div flex-area="lower-third">
                  <span></span>
                  <div>最佳女配角</div>
                  <div>主演: 我，花样女王</div>
              </div>
          </mip-story-layer>
      </mip-story-view>
  </mip-story>
  ```
  <img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/fill-0.png" width="276" height="494" />


  以上是我们在添加页面的时候几种方式，那么接下来就是我的小故事的分享页了。

## 小故事内置动画的使用介绍 

### 小故事内置动画属性

在小故事中，我们提供了一些列的内置动画，您在开发使用时您可以通过将动画入口应用于小故事的层（layer）中的元素来增强MIP的故事。例如，您可以让标题从左侧飞入，或者放入页面或淡入等等。MIP提供了以下预设的动画，通过给元素添加 `animate-in` 属性来完成指定的动画效果。

- 基本用法：

```html
<style mip-custom>
    mip-story-view {
        color: #fff;
    }
    h1 {
        text-align: center;
    }
    .box {
        width: 100px;
        height: 100px;
        background-color: #09f;
        margin-top: 30px;
        margin-left: auto;
        margin-right: auto;
    }
    </style>
<mip-story>
    <mip-story-view>
        <mip-story-layer template="vertical">
            <h1>fade-in</h1>
            <!-- 内置动画的使用方式如下 -->
            <div animate-in="fade-in" class="box"></div>
        </mip-story-layer>
	</mip-story-view>
</mip-story>
```

小故事提供以下预设动画：

| animate-in        | 默认动画时间（ms） | 说明         |
| ----------------- | ------------------ | ------------ |
| `fade-in`         | 500                | 淡入         |
| `fly-in-top`      | 500                | 上侧滑入     |
| `fly-in-bottom`   | 500                | 下侧滑入     |
| `fly-in-left`     | 500                | 左侧滑入     |
| `fly-in-right`    | 500                | 右侧滑入     |
| `twirl-in`        | 1000               | 旋转进入     |
| `whoosh-in-left`  | 500                | 左侧飞入     |
| `whoosh-in-right` | 500                | 右侧飞入     |
| `rotate-in-left`  | 700                | 左侧旋转飞入 |
| `rotate-in-right` | 700                | 右侧旋转飞入 |

- 实际动画示意图如下：

<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/%E5%B0%8F%E6%95%85%E4%BA%8B%E5%86%85%E7%BD%AE%E5%8A%A8%E7%94%BB.gif" width="276" height="494" />


在设置了上述`animate-in` 属性的配置后，可以完成对应的动画，但是我们还支持其他属性，配合`animate-in`属性使得动画更加饱满生动，目前每个动画都设有一个内置的默认时间，用于：

- **`animate-in-delay`：延迟**
  - 这是延迟启动动画的时间量。例如，.3s的延迟表示动画在.3秒后进入页面。延迟0s立即开始动画。
  - 是否必填：否
  - 取值：ms/s
- **`animate-in-duration`：持续时间**
  - 这是动画发生的时间量。例如，从开始到结束的淡入动画需要500毫秒。
  - 是否必填：否
  - 取值：ms/s
- **`animate-in-after` ：开始时间**
  - 这是动画发生的开始时间。例如，上述示例中，每个动画都是相对于上一个动画结束开始。
  - 是否必填：否
  - 取值：带有动画元素的id

您可以通过更改`animate-in-delay`、`animate-in-duration`和`animate-in-after` 属性的延迟或持续时间来自定义动画的时间。

- 示例

```html
<mip-story-layer>
      <!-- 以fade-in的形式入场，动画时间持续1000ms, 动画开始前延迟1000ms-->
    <h1 animate-in="fade-in" animate-in-duration="1000" animate-in-delay="1000"  id="first-animate">最佳影片</h1>
      <!--在id为 first-animate 的元素动画动画结束之后开始执行-->
    <p animate-in="fly-in-left" animate-in-after="first-animate">钢铁侠是一部非常好的科幻片。</p>
</mip-story-layer>
```

### 如何设计一个更加生动的MIP页面

​	我们可以通过以下代码实现一个静态页面。

```html
<mip-story-view>
    <mip-story-layer template="fill">
        <mip-img  layout="responsive" width="480" height="720" src="https://www.mipengine.org/static/img/mip-story/p7.png"></mip-img>
    </mip-story-layer>
    <mip-story-layer>
        <div class="common-wrap1">
            <span></span>
            <span>最佳动画短片</span>
            <span>亲爱的篮球</span>
            <span></span>
            <span>最佳动画长片</span>
            <span>寻梦环游记</span>
        </div>
    </mip-story-layer>
    <mip-story-layer>
        <div class="mask"></div>
    </mip-story-layer>
</mip-story-view>
```

在浏览器中可以看到如下页面：


<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/animation-0.png" width="276" height="494" />

如果在此基础上添加动画，那么将使得页面更加生动。

​	我们将首先制作文本的入口动画，并在页面右侧显示“fade-in”。像这样添加`animate-in="fade-in"`到`<span>`元素：

```html
<mip-story-view>
    <mip-story-layer template="fill">
        <mip-img  layout="responsive" width="480" height="720" class="fade-in-scale" src="https://www.mipengine.org/static/img/mip-story/p7.png"></mip-img>
    </mip-story-layer>
    <mip-story-layer>
        <div class="common-wrap1">
            <span></span>
            <span animate-in="fade-in" id="sixth-animation">最佳动画短片</span>
            <span>亲爱的篮球</span>
            <span></span>
            <span>最佳动画长片</span>
            <span>寻梦环游记</span>
        </div>
    </mip-story-layer>
    <mip-story-layer>
        <div class="mask"></div>
    </mip-story-layer>
</mip-story-view>
```

​	接下来，我们给每个图片添加动画。

```html
<mip-story-view>
    <mip-story-layer template="fill">
        <mip-img  layout="responsive" width="480" height="720" class="fade-in-scale" src="https://www.mipengine.org/static/img/mip-story/p7.png"></mip-img>
    </mip-story-layer>
    <mip-story-layer>
        <div class="common-wrap1">
            <span></span>
            <span animate-in="fade-in" id="sixth-animation">最佳动画短片</span>
            <span animate-in="fly-in-left" animate-in-duration=400 animate-in-after="sixth-animation">亲爱的篮球</span>
            <span></span>
            <span animate-in="fade-in" id="sixth-animation">最佳动画长片</span>
            <span animate-in="fly-in-right" animate-in-duration=400 animate-in-after="sixth-animation">寻梦环游记</span>
        </div>
    </mip-story-layer>
    <mip-story-layer>
        <div class="mask"></div>
    </mip-story-layer>
</mip-story-view>
```


<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/animation3.gif" width="276" height="494" />

​	MIP故事中的动画有很多可能性（例如，结合动画，链接动画），本教程中只显示了部分的功能，详细的API请参考[MIP组件的介绍]()。当然您在开发小故事的过程中也可以使用CSS3中的animation来完成小故事的动画，但是在ios11.3系统中，使用animation去实现动画会出现丢失动画效果的问题，这是由于浏览器在解析页面的时，自定义标签元素由于没有默认的display属性的，因此在animation动画间隙时会出现找不到该DOM元素的从而无animation动画，我们推荐您在开发小故事时，可以优先选择已封装好的内置动画。但是如果想要自己写animation动画是需要您在小故事的`mip-story`里添加`display="none"`。您有任何问题欢迎在[issue](https://github.com/mipengine/mip-extensions/issues)中提出意见。

代码示例：

```html
<!DOCTYPE html>
<html mip>
<head>
    <meta charset="utf-8">
    <title>小故事内置动画效果示意图</title>
    <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1,user-scalable=no">
    <link rel="stylesheet" type="text/css" href="https://mipcache.bdstatic.com/static/v1/mip.css">
    <link rel="canonical" href="http://www.1905.com/mip/oscar">
    <style mip-custom>
        mip-story {
            display: none;
        }
    </style>
</head>
<body>
    <mip-story>
        ...
	</mip-story>
    <!-- MIP 运行环境 -->
    <script src="https://c.mipcdn.com/static/v1/mip.js"></script>
    <!-- 小故事依赖脚本 -->
    <script src="https://c.mipcdn.com/static/v1/mip-share/mip-share.js"></script>
    <script src="https://c.mipcdn.com/static/v1/mip-story/mip-story.js"></script>
    <script src="https://c.mipcdn.com/static/v1/mip-stats-baidu/mip-stats-baidu.js"></script>
    <script src="https://c.mipcdn.com/static/v1/mip-scrollbox/mip-scrollbox.js"></script>
</body>
</html>
```

## 小故事分享页面的介绍

​	到目前，您已经添加了所有的页面，那么当我们需要对一个小故事进行分享的时候，我们则需要创建一个分享页面。

​	在分享页中，在 `<mip-story>` 段落最后提供了专门用于展示分享及小故事更多相关信息的页面。当用户在最后一个段落继续向后点击时候，即会出现。其中该页面内容需要通过开发者进行配置，具体使用范式和配置参数如下：



```html
<mip-story>
    <script type="application/json">
    {
         "share": {
                "thumbnail": "https://www.mipengine.org/static/img/mip-story/cover.jpg",
                "background": "https://www.mipengine.org/static/img/mip-story/p8.png",
                "title": "第90届奥斯卡颁奖典礼回顾",
                "from": "小故事",
                "desc": "一分钟带你了解第九十届奥斯卡颁奖典礼",
                "readings": "10000"
            }
     }
	</script>
    <mip-story-view>
        <mip-story-layer template="fill">
        </mip-story-layer>
    </mip-story-view>
</mip-story>
```

如图所示：

<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/share.png" width="276" height="494" />


除了share字段，我们还提供了别的字段，以丰富小故事的分享页面，具体使用方式如下：

```html
<mip-story>
    <script type="application/json">
    {
        "share": {
            "thumbnail": "img/share.jpg",
            "background": "img/sharebg.png",
            "title": "相约一起看樱花",
            "from": " "
        },
        "recommend": {
        "url": "",
        "items": [
            {
                "cover": "https://img6.bdstatic.com/img/image/public/ribenshangying3.jpg",
                "url": "http://shxingtuan.com/jp_sakura/index.html",
                "title": "日本赏樱推荐",
                "from": " ",
                "fromUrl": " "
            },
            {
                "cover": "https://img6.bdstatic.com/img/image/public/shangyingmeitu.jpg",
                "url": "https://m.baidu.com/sf/vsearch?pd=image_content&word=%E8%B5%8F%E6%A8%B1&tn=vsearch&sa=vs_tab&lid=9813145669733695291&ms=1&atn=page&fr=tab&ssid=2e3d6e69757a696e616e6e616ece0f",
                "title": "往年樱花美图欣赏",
                "from": " ",
                "fromUrl": " "
            }
        ]
        }
     }
	</script>
    <mip-story-view>
        <mip-story-layer template="fill">
        </mip-story-layer>
    </mip-story-view>
</mip-story>
```

- share: share 字段下包含的是分享相关的数据。
- share.thumbnail: 预览小故事的缩略图地址。
- share.background: 结尾页背景图片地址。
- share.title: 小故事标题。
- share.from: 资源的来源信息。
- recommend: 小故事推荐相关的信息。
- recommend.items: 推荐小故事列表，它是一个数组，包含了所有推荐的小故事数据。
  - cover: 推荐的小故事背景图片。
  - url: 推荐的小故事跳转地址。
  - title: 推荐的小故事标题。
  - from: 推荐的小故事来源信息。
  - fromUrl: 推荐的小故事来源跳转地址。

<img src="http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/share.jpeg" width="276" height="494" />

在完成以上步骤，我们的小故事已经基本开发完成，但是在发布之前，我们需要对其进行校验，看是否属于MIP HTML的标准。

## 添加统计

​	在完成一个小故事的开发以后，有时候我们需要对整个小故事的用户行为进行监控，因此需要使用统计组件，来进行统计，我们这里提供了两个组件便于用户使用。

- PV 使用 mip-pix 组件统计

  `mip-pix`组件本身在页面不可见，但本元素只有滚动到屏幕可见范围内才触发初始化;

  - 示例

    ```html
    <mip-pix src="https://www.mipengine.org/a.gif"></mip-pix>
    ```

  详细的使用介绍可点击查看[mip-pix 组件](https://www.mipengine.org/examples/mip/mip-pix.html)

- 交互行为日志使用 [mip-stats-baidu 组件统计](https://github.com/mipengine/mip-extensions/tree/master/src/mip-stats-baidu)

  - 示例

    ```html
    <mip-stats-baidu>
        <script type="application/json">
            {
                "token": "02890d4a309827eb62bc3335b2b28f7f",
                "_setCustomVar": [1, "login", "1", 2],
                "_setAutoPageview": [true]
            }
        </script>
    </mip-stats-baidu>
    ```

完成了统计添加，我们已经完成了一个小故事的整个开发，但是鉴于小故事是属于特殊的MIP页，因此小故事也要经过MIP页面校验，只有符合MIP页面规范的小故事才可以最终在搜索结果页展现。

## 小故事的MIP规范校验

​	当我们完成一个小故事页面的开发后，我们需要对小故事进行MIP规范的校验，原因是小故事页是属于MIP页的，因此为了可以试您的小故事在搜索结果页可以生效展示，需要对小故事进行MIP规范校验，目前MIP规范的校验有两种方式：

-  [MIP 校验工具](https://www.mipengine.org/validator/validate) 

  首先打开 [MIP 校验工具](https://www.mipengine.org/validator/validate) 的校验网页，把您开发的小故事页面代码复制粘贴到MIP代码校验工具的可视化区域，在网页的底部就会显示出您开发的小故事页面是否符合MIP规范。

  如果校验通过，则会显示绿色的**`SUCCESS → 验证成功，完全符合MIP规范`**提示您页面校验成功。

  ![success](http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/success.png)

  如果校验不通过，则会显示红色的**`ERROR → line x,col x:xxxxxxxx`** 提示您页面校验不成功，并且定位校验错的行号和列号。

  ![fail](http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/fail.png)

  ​

- 使用[MIP-CLI](http://www.cnblogs.com/mipengine/p/mip_cli_1_install.html)工具中的`mip validate`命令

  MIP-CLI：mip 开发工具，用于 MIP 页面和组件的开发和校验。
  依赖环境: **Node.js (>=4.x)**
  输入`node -v` 查看 node 版本，如果版本为 5.x，6.x，[ 请点击这里 ](http://www.cnblogs.com/mipengine/p/mip_cli_1_install.html#question1)。

  示例:

  ![img](http://mip-doc.bj.bcebos.com/mip-blog-11/11_node_v.png)

  将安装好的 node 打开 输入以下指令（mac系统需要sudo）：

  ```
  $ npm install -g mip-cli
  ```

  mac系统需要使用以下指令：

  ```
  $ sudo npm install -g mip-cli
  ```

  出现以下界面显示正在安装：

  ![img](http://mip-doc.bj.bcebos.com/mip-blog-11/11_install.png)

  如果安装过程中有报错，[ 请点击这里查看解决办法 ](http://www.cnblogs.com/mipengine/p/mip_cli_1_install.html#question2)。

  检验是否安装成功可以输入`mip -V`，如果出现 mip 版本号，则表示安装成功。

  ![img](http://mip-doc.bj.bcebos.com/mip-blog-11/11_mip_V.png)

  此时您已经成功安装好MIP-CLI，在控制台直接输入`mip validate xxx.html`，其中xxx.html文件为您自己开发的mip页面。您可以查看是否通过校验。

  可以看到如果成功，控制台将显示以下提示：

  ![success1](http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/success1.png)

  如果失败，控制台会显示失败原因，并且定位错误信息的出处：

  ![fail1](http://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/fail1.png)

​	在校验的同时，可能会有各种报错，那么您可以通过查看[MIP校验错误列表](https://www.mipengine.org/doc/2-tech/2-validate-mip.html)来定位出错的位置和原因，修改并且重新校验，校验通过就可以提交部署MIP小故事页面了。
