title: 小故事中使用模板布局

layout: examples

---

## 知识储备

​​&emsp;&emsp;在阅读本篇前，您需要了解什么小故事，如果您还不了解什么是小故事，可以查看[开发小故事前期准备](https://www.mipengine.org/doc/story/create1.html)、[小故事的组织结构](https://www.mipengine.org/doc/story/create2.html)、[创建小故事的封面](https://www.mipengine.org/doc/story/create3.html)了解基础信息；


## 使用小故事内置模板

​​&emsp;&emsp;在开发小故事时为了减少您的开发成本，我们为你封装好了一些常用的内置布局，你可以直接按照下面描述的方法直接使用，比如：

<div align=center>
    <img src="https://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/template.gif" width="276" height="494" />
</div>

### 小故事内置的布局

#### 基本用法

​​&emsp;&emsp;通过给页面元素添加 `template`和`flex-area` 属性来进行布局的设置，目前的布局分为两种，一种是杂志布局，一种是普通的内容布局。同时我们还提供了`background`属性为小故事和其段落设置不同的主题色。

#### 杂志布局	

​​&emsp;&emsp;首先介绍杂志布局，在杂志样式中，我们提供了两种杂志样式，第一种是只有主标题和杂志页面，第二种包含标题和内容，针对第一种杂志布局，具体的使用方式如下：

```html
<mip-story>
    <mip-story-view>
        <mip-story-layer template="magazine">
            <div flex-area="magazine-img">
                <mip-img  width="480" height="720"  src="https://www.mipengine.org/static/img/sample_02.jpg"></mip-img>
            </div>
            <div flex-area="magazine-content">
                <h1>用 MIP 来展示您的杂志封面</h1>
            </div>
        </mip-story-layer>
    </mip-story-view>
</mip-story>
```

​​&emsp;&emsp;首先在`mip-story-layer`上设置`template`设置为`magazine`，指定当前的此页为杂志页面，杂志页面是由图片和内容组成的，因此需要两个`div`来对图片和内容分层。在图片层中给相关的`div`设置`flex-area="magazine-img"`，在内容层中给相关的`div`设置`flex-area="magazine-content"`。

​​&emsp;&emsp;具体的展示如下：

<div align=center>
    <img src="https://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/25.png" width="276" height="494" />
</div>

​​&emsp;&emsp;针对第二种杂志布局，具体的使用方式如下：

```html
<mip-story>
    <mip-story-view>
        <mip-story-layer template="magazine">
            <div flex-area="magazine-img">
                <mip-img  width="480" height="720" layout="responsive" src="https://www.mipengine.org/static/img/sample_02.jpg"></mip-img>
            </div>
            <div flex-area="magazine-content">
                <h2>Title</h2>
                <p>小故事一种可交互的多媒体卡片，是由多元化内容组成的媒体形态，可带来沉浸式、多媒体、可交互的浏览体验。</p>
            </div>
        </mip-story-layer>
    </mip-story-view>
</mip-story>
```

​​&emsp;&emsp;具体的展示如下：

<div align=center>
    <img src="https://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/26.png" width="276" height="494" />
</div>


#### 普通的内容布局

​​&emsp;&emsp;除了杂志布局以外，还有普通的内容布局。在此主要提供了7中布局，

| template        | 说明       |
| --------------- | ---------- |
| ` center`       | 居中       |
| ` under-center` | 居中下对齐 |
| ` under-left`   | 居中左对齐 |
| ` under-right`  | 居中右对齐 |
| ` up-left`      | 居上左对齐 |
| ` up-center`    | 居中上对齐 |
| ` up-right`     | 居上右对齐 |

​​&emsp;&emsp;具体的使用方式如下：

```html
<mip-story>
	<mip-story-view>
        <mip-story-layer template="fill">
            <mip-img  width="480" height="720" layout="responsive" 
                     src="https://www.mipengine.org/static/img/sample_01.jpg"></mip-img>
        </mip-story-layer>
        <mip-story-layer template="under-center">
            <h4>小故事是什么？</h4>
            <p>居中</p>
        </mip-story-layer>
    </mip-story-view>
    <mip-story-view>
        <mip-story-layer template="fill">
            <mip-img  width="480" height="720" layout="responsive"
                     src="https://www.mipengine.org/static/img/sample_02.jpg"></mip-img>
        </mip-story-layer>
        <mip-story-layer template="under-left">
            <h4>小故事是什么？</h4>
            <p>居下左对齐</p>
            <a href="https://www.baidu.com">普通跳转链接</a>
        </mip-story-layer>
    </mip-story-view>
    <mip-story-view>
        <mip-story-layer template="fill">
            <mip-img  width="480" height="720" layout="responsive" 
                     src="https://www.mipengine.org/static/img/sample_01.jpg"></mip-img>
        </mip-story-layer>
        <mip-story-layer template="under-right">
            <h4>小故事是什么？</h4>
            <p>居下右对齐</p>
            <a href="https://www.baidu.com">普通跳转链接</a>
        </mip-story-layer>
    </mip-story-view>
    <mip-story-view>
        <mip-story-layer template="fill">
            <mip-img  width="480" height="720" layout="responsive" 
                     src="https://www.mipengine.org/static/img/sample_02.jpg"></mip-img>
        </mip-story-layer>
        <mip-story-layer template="up-left">
            <h4>小故事是什么？</h4>
            <p>居上左对齐</p>
            <a href="https://www.baidu.com">普通跳转链接</a>
        </mip-story-layer>
    </mip-story-view>
    <mip-story-view>
        <mip-story-layer template="fill">
            <mip-img  width="480" height="720" layout="responsive"
                     src="https://www.mipengine.org/static/img/sample_01.jpg"></mip-img>
        </mip-story-layer>
        <mip-story-layer template="up-center">
            <h4>小故事是什么？</h4>
            <p>居中上对齐</p>
            <a href="https://www.baidu.com">普通跳转链接</a>
        </mip-story-layer>
    </mip-story-view>
    <mip-story-view>
        <mip-story-layer template="fill">
            <mip-img  width="480" height="720" layout="responsive"
                     src="https://www.mipengine.org/static/img/sample_02.jpg"></mip-img>
        </mip-story-layer>
        <mip-story-layer template="up-right">
            <h4>小故事是什么</h4>
            <p>居上右对齐</p>
            <a href="https://www.baidu.com">普通跳转链接</a>
        </mip-story-layer>
        <mip-story-layer template="under-left">
            <h4>小故事是什么？</h4>
            <p>居下左对齐</p>
            <a href="https://www.baidu.com">普通跳转链接</a>
        </mip-story-layer>
    </mip-story-view>
</mip-story>
```

​​&emsp;&emsp;各种布局的示意如下图所示：

<div align=center>
    <img src="https://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/template2.gif" width="276" height="494" />
</div>

​​&emsp;&emsp;以上展示了如何通过设置不同的布局属性可以实现不同的位置布局。

#### 主题色的设置

​​&emsp;&emsp;我们还内置了选择不同的主题色，为小故事设置整体的主题色和不同段落的主题色。具体的使用方法如下：

```html
<mip-story standalone background="#787878">
    <mip-story-view background="#000000">
        <mip-story-layer template="magazine">
            <div flex-area="magazine-img">
                <mip-img  width="480" height="720"  src="https://www.mipengine.org/static/img/sample_02.jpg"></mip-img>
            </div>
            <div flex-area="magazine-content">
                <h1>用 MIP 来展示您的杂志封面</h1>
            </div>
        </mip-story-layer>
    </mip-story-view>
    <mip-story-view>
        <mip-story-layer template="magazine">
            <div flex-area="magazine-img">
                <mip-img  width="480" height="720" layout="responsive" src="https://www.mipengine.org/static/img/sample_02.jpg"></mip-img>
            </div>
            <div flex-area="magazine-content">
                <h2>Title</h2>
                <p>小故事一种可交互的多媒体卡片，是由多元化内容组成的媒体形态，可带来沉浸式、多媒体、可交互的浏览体验。</p>
            </div>
        </mip-story-layer>
    </mip-story-view>
</mip-story>
```

​​&emsp;&emsp;有上述代码可见，在`mip-story`设置`background`是整个小故事的主题色为灰色，在`mip-story-view`设置`background`是当前段落的主题色为黑色，具体展现形式如下：

<div align=center>
    <img src="https://mipstatic.baidu.com/static/mip-static/mip-story/demo/static/color.gif" width="276" height="494" />
</div>

