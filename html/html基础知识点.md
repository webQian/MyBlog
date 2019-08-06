[基础知识点](#basic)

[站点自定义图标](#icon)

[语义化](#Semanticization)

[多媒体](#media)

[iframe相关](#iframe)

[svg相关](#svg)

[表格](#table)

[表单](#form)

[网站安全相关](#safe)

[seo相关知识及优化](#seo)

[!DOCTYPE html的作用](#DOCTYPE)

[标准模式和怪异模式](#model)

[ie浏览器](#ie)

[同源策略](#source)


# <span id = "basic">基础知识点</span>
1. html中块级元素不会被嵌套进内联元素中，但是可以被嵌套在其他块级元素中
2. keywords已经被废弃，因为作弊者填充了大量的Keywords，导致错误的引导了搜索引擎的搜索结果
3. 给网站设置主语言
```
<html lang="zh">
```
4. 在6个可用标题h1~h6中，每个页面的使用最好不要超过三个，h1一个页面应该只使用一次
5. URL：统一资源定位符
6. 文档锚点，在要跳转的元素上增加一个id属性，在a链接的href属性中使用#ID。给a元素增加download属性，代表下载资源，href属性中放要下载的资源路径
7. 电子邮件链接
```
<a href="mailto:邮箱号?cc=抄送&bcc=密件抄送&subject=主题&body=主体">
```
8. 定义列表
```
<dl>
  <dt></dt>
  <dd></dd>
</dl>
```
9. 引用：如果一个块级元素是被引用的内容，应该使用
```
<blockquote>
```
元素将其包裹起来，然后其cite属性指向引用的url，浏览器在渲染块引用时，会默认缩进

如果是行内元素，则需要用
```
<q>
```
元素将引用的内容包裹起来，同样的，在其上使用cite属性指向引用的url
10. 缩略语
```
<abbr title="Hypetext Markup Language">HTML</abbr>
```
11. 上标和下标
```
<sup>  上标superscript
<sub>  下标subscript
```
# <span id="icon">给网站增加自定义图标</span>
```
<link rel="icon" type="image/x-icon" href="路径">
```
给网站的自定义图片最好选用.icon 16像素的图片
# <span id="Semanticization">语义化标签</span>
文档的基本组成部分：页眉、导航栏、主内容、侧边栏、页脚
```
<header>：页眉，如果直接放在<body>元素下，则认为是整个网站的页眉，如果在一个区块中，则认为是该区块的标题

<nav>：导航栏

<main>：页面的主内容区域，整个页面应该只能有一个<main>元素，每个页面的独有的内容，不要嵌套在其他元素中

<article>：存放与页面其他部分无关的一个独立内容

<section>：适合用来组织页面的各部分，使其按功能分开

<aside>：侧边栏

<footer>：页脚
  
<address>：联系方式

<time datetime="2018-09-12">：时间
```
# <span id="media">多媒体相关</span>
1. 背景图片的使用方式
如果图片的内容对网站有意义，应该使用html的方式，这样可以设置该元素的title和alt属性，如果对网站无意义，则应该使用css去设置
2. 图片元素的语义容器，让图片和标题具有联系应该使用<figure>元素，将图片和内容具有联系，当然<figure>不仅仅可以包含图片
```
<figure>
  <img>
  <figcaption></figcaption>
</figure>
```
3. 可以使用<vedio>元素来在网页上显示一段视频，可以设置其属性controls，让用户可以控制视频
```
<video src="测试小视频.mp4" controls>
  <p>备选文字</p>
</video>
```
<video>元素中的<p>元素是当浏览器不支持<video>标签时，将显示后备文本。

由于各个浏览器对视频格式的兼容性不同，所以你应该设置多个后备选项
```
<video controls>
  <source src="测试小视频.mp4" type="video/mp4">
  <source src="测试小视频.webm" type="video/webm">
</video>
```
给<source>元素设置type属性的意义是为了浏览器在加载时去读取type属性，从而跳过不支持的格式，如果不设置type属性，那么浏览器就会一个一个加载视频来判断，将耗费
大量的时间。
4. <video>的新属性： 
autoplay自动播放，即使其他内容还没有完全加载
loop循环播放，默认为1
muted播放时自动静音
poster指向一个图片的url，用来在视频还没有播放时去显示图片，用于粗略的预览
preload用来缓冲较大的文件，none不缓冲，auto页面加载后去缓存媒体文件 metadata仅缓冲文件的元数据
5. 插入音频
```
<audio>
```
因为音频文件只有控制条，没有像视频那样的视觉组件，所以除了poster、width、height以外其余属性和<video>相同
6. WEBVTT
webVTT格式，简单来说字幕文件，使用时用<track>标签，将其放在<source>元素的最后，kind属性说明是哪种类型的，srclang属性用来告诉是什么语言编写的
```
<video controls autoplay loop>
      <source src="测试小视频.mp4" type="video/mp4">
      <source src="测试小视频.webm" type="video/webm">
      <track kind="subtitle" src="字幕.vtt" srclang="zh">
</video>
```
7. 最大宽度
```
  max-width:1200px
```
在高于此宽度情况下，元素会内部会保持1200px，并处于可用空间的正中间，在小于此宽度的情况下，元素会占有视口宽度的100%

# <span id="iframe">iframe相关</span>
iframe将一个完整的html页面插入到页面中。
1. 基本属性
allowfullscreen：允许全屏模式

frameborder：边框，应该在css中使用

src：路径

sandbox：该属性在已经支持了其他属性并且更现代的浏览器中使用，可以提高安全性，沙盒化
2. 为了提高网页加载速度，在网页加载后使用javascript来设置iframe元素的src属性，可以使页面更快的使用，减少页面的加载时间
3. 嵌入多种类型外部内容，像java applet、flash、svg、pdf、视频、图片，使用
```
<embed>和<object>
```

# <span id="svg">svg</span>
svg是描述矢量图形的xml语言
优点：svg矢量中的文本仍然可以访问，有利于seo

缺点：非常容易变复杂，会在浏览器处理中占用很长的处理时间，兼容性差（ie9开始支持），比位图更难创建
1. svg在html页面中的使用
第一种方式：使用<img>标签

优点：熟悉语法，内置文本仍然有效，可以在a链接中嵌套，让其变为超链接

缺点：无法使用javascript操作图像，而且必须要使用内联样式控制，并且不能使用伪类

在兼容处理上，可以使用合并方式
```
<img src="png" alt="文本" srcset="svg">
```
旧浏览器将加载png，新式浏览器将使用svg

还可以使用css来设置为背景图片
```
background-image:url('svg')
background-image:url('png') no-repeat center;
```
第二种方式：使用内联的svg标签
```
<svg width="300" height="200">
    <rect width="100%" height="100%" fill="green" />
</svg>
```
优点：减少了http请求，可以为svg分配class和id，并使用css来控制样式，内联的svg是唯一可以使用css进行交互，包括伪类和动画，同样也可以作为链接。

缺点：只适合在一个地方使用svg，多次使用将导致资源密集型维护，会额外增加html文件的大小，浏览器不能像缓存普通图片一样缓存svg，svg中可以增加回退，但是对于支持svg的浏览器来说，仍然会加载后备图片或文本，为了兼容旧浏览器而极大的增大了开销
元数据meta标签和标准模式、怪异模式

# <span id="table">表格</span>
1. 要给表格每一列设置样式，使用
```
<colgroup>
  <col>
  <col>
<colgroup>
```
2. 表格标题
```
<caption>
```
3. thead和tfoot不论写在代码中的什么位置，都会出现在表格第一行和表格最后一行

# <span id="form">表单基础</span>
1. 写法
```
<form>
  <fieldset>
    <legend>表单的描述</legend>
  </fieldset>
</form>
```
2. 下拉列表，使用<optgroup>造成视觉包裹效果，使用multiple进行多选
3. 自动补全，使用
```
  <input type="text" list="datalist的ID">
  <datalist id="与文本框list属性相对应">
    <option></option>
  </datalist>
```
4. 上传文件时使用accept属性来限制用户上传文件的类型，必须使用post方法提交表单，将ecctype设置为multipart/form-data
5. css:valid控制通过验证样式，css:invalid控制不通过样式，pattern设置正则表达式验证

# <span id="safe">网站安全问题</span>
1. XSS
2. CSRF
3. SQL注入
4. http数据头注入
5. 电子邮件注入
6. iframe的安全隐患：攻击向量

单点劫持：将隐藏的iframe嵌入到文档中，并使用被隐藏的iframe来捕获用户交互，误导用户操作并获取敏感信息

措施：在必要的时候才使用iframe、使用https减少远程内容在传输过程中被篡改的可能性，https防止嵌入式内容访问父文档的内容，反之亦然，在使用了https后，各大知名公司都会检测src路径、始终使用sandbox来进行沙盒化，默认情况下，应该使用没有参数的sandbox属性来强制执行所有可用的权限，如果真的需要，单独添加参数放开权限，但是不能同时使用allow-script和allow-same-origin属性，在这种情况下，嵌入式内容可以绕过阻止站点执行脚本的同源安全策略，并使用Javascript来关闭沙盒、配置SCP指令，提供一组HTTP标头，可以防止其他网站在其网页中嵌入您的内容

# <span id="seo">seo概念及相关优化</span>

# <span id="DOCTYPE">!DOCTYPE html的作用</span>

# <span id="model">标准模式和怪异模式</span>

# <span id="ie">ie浏览器下的不同之处</span>

# <span id="source">同源策略</span>

