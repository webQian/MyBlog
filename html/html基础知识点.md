# 基础知识点
1. html中块级元素不会被嵌套进内联元素中，但是可以被嵌套在其他块级元素中
2. 在<meta>标签中，keywords已经被废弃，因为作弊者填充了大量的Keywords，导致错误的引导了搜索引擎的搜索结果
3. 给网站设置主语言
```
<html lang="zh">
```
4. 在6个可用标题h1~h6中，每个页面的使用最好不要超过三个，h1一个页面应该只使用一次
5. URL：统一资源定位符
6. 文档锚点，在要跳转的元素上增加一个id属性，在a链接的href属性中使用#ID，给a元素增加download属性，代表下载资源，href属性中放要下载的资源路径
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
9. 引用：如果一个块级元素是被引用的内容，应该使用<blockquote>元素将其包裹起来，然后<blockquote>的cite属性指向引用的url，浏览器在渲染块引用时，会默认缩进
如果是行内元素，则需要用<q>元素将引用的内容包裹起来，同样的，在<q>元素上使用cite属性指向引用的url
10. 缩略语
```
<abbr title="Hypetext Markup Language">HTML</abbr>
```
11. 语义化的联系方式标签和时间标签
```
<address>
<time datetime="2018-09-12">
```
12. 上标和下标
```
<sup>  上标superscript
```
```
<sub>  下标subscript
```
# 给网站增加自定义图标
```
<link rel="icon" type="image/x-icon" href="路径">
```
给网站的自定义图片最好选用.icon 16*16像素的图片
# 语义化标签
文档的基本组成部分：页眉、导航栏、主内容、侧边栏、页脚

<header>：页眉，如果直接放在<body>元素下，则认为是整个网站的页眉，如果在一个区块中，则认为是该区块的标题

<nav>：导航栏

<main>：页面的主内容区域，整个页面应该只能有一个<main>元素，每个页面的独有的内容，不要嵌套在其他元素中

<article>：存放与页面其他部分无关的一个独立内容

<section>：适合用来组织页面的各部分，使其按功能分开

<aside>：侧边栏

<footer>：页脚
# 多媒体相关
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
6. WEBVTT
webVTT格式，简单来说字幕文件，使用时用<track>标签，将其放在<source>元素的最后，kind属性说明是哪种类型的，srclang属性用来告诉是什么语言编写的
```
<video controls autoplay loop>
      <source src="测试小视频.mp4" type="video/mp4">
      <source src="测试小视频.webm" type="video/webm">
      <track kind="subtitle" src="字幕.vtt" srclang="zh">
</video>
```
# iframe相关
iframe将一个完整的html页面插入到页面中。
1. 基本属性
allowfullscreen：允许全屏模式

frameborder：边框，应该在css中使用

src：路径

sandbox：该属性在已经支持了其他属性并且更现代的浏览器中使用，可以提高安全性，沙盒化
2. 


因为音频文件只有控制条，没有像视频那样的视觉组件，所以除了poster、width、height以外其余属性和<video>相同
元数据meta标签和标准模式、怪异模式
seo
html语义化有助于seo以及屏幕阅读器
<!DOCTYPE html>的作用




iframe元素的基本属性：allowfullscreen，如果设置了则允许iframe可通过全屏API设置为全屏模式
frameborder：边框，应该通过css来实现，不推荐在Html中使用
src:路径
iframe元素中的文本是一种备选属性
sandbox:该属性需要在已经支持了其他属性并且更现代的浏览器中使用，可以提高安全性
！！！！！为了提高速度，在页面加载后使用javascript来设置iframe元素的src属性，可以使页面更快的被使用，减少页面的加载时间！！！重要的seo指标
iframe的安全隐患：攻击向量
单击劫持：将隐藏的iframe嵌入到文档中，并使用它来捕获用户交互，误导用户并得到敏感信息

措施：只要在必要的时候使用iframe 2.使用https,https减少了远程内容在传输过程中被篡改的可能性 https防止嵌入式内容访问您父文档中的内容，反之亦然。
所有有声望的公司，当您嵌入内容时，iframe将通过https来查看iframe中src的属性
3.始终使用sandbox属性，给嵌入的内容仅能完成自己工作的权限，一个允许包含在其里面的代码以适当的方式执行或用于测试，但不能对其他代码块造成损害的容器称为沙盒
默认情况下，应该使用没有参数的sandbox属性来强制执行所有可用的限制，如果真的需要，请逐个添加需要的权限，但是请注意永远不应该同时添加allow-script和allow-
same-origin到sandbox属性中，这种情况下，嵌入式的内容可以绕过 阻止站点执行脚本的同源安全策略，并且使用javascript来关闭沙盒
4.配置CSP指令：内容安全策略。提供一组HTTP标头，可以防止其他网站在其网页中嵌入您的内容


<embed>和<object>元素不同于iframe元素，它们可以用来嵌套多种类型的外部内容的 像java applet、flash、svg、pdf、视频、图片，但是基本已经废弃

矢量图：较小的文件体积，高度可缩放，不会像素化，即不会破坏分辨率
位图：bmp、png、jpg、gif，由像素网格来定义
矢量图用算法来定义
svg是描述矢量图形的xml语言，svg矢量中的文本仍然可以访问，有利于seo，很好的适应样本和脚本，每个组件都可以用css和javascript来控制
缺点：svg非常容易变复杂，会在浏览器中占用很长的处理时间，
兼容性，ie9才开始支持
比位图更难创建
svg在html页面中的使用
1.使用img标签 
优点:熟悉语法，alt属性中提供的内置文本仍然有效，可以在a链接中嵌套img，使其成为超链接 
缺点：无法使用javascript操作图像，如果要用CSS属性控制svg，必须写内联样式，外部样式不对svg起作用，不能对svg使用伪类

对于不支持svg的浏览器，可以在src中引入png等图像，而在srcset属性中引入svg，srcset只有在新式浏览器中才支持
<img src="png" alt="test" srcset="svg">，旧浏览器将加载Png,新浏览器将加载svg
还可以使用css来设置为背景图片，而旧浏览器将继续读取png图像
background-image:url('png') no-repeat center;
background-image:url('svg')
2.使用内联的svg:<svg width="300" height="200">
    <rect width="100%" height="100%" fill="green" />
</svg>
优点：减少http请求，可以减少加载时间，可以为svg分配id和class，并使用css来控制样式，内联的svg是唯一可以在css使用交互，包括伪类和动画方法，同样可以将其包裹
在a标签中，使其成为链接

缺点：只适合在一个地方使用svg，多次使用将导致资源密集型维护
会额外增加html文件的大小
浏览器不能像缓存普通图片那样缓存内联的svg
在svg中增加回退，但是支持svg的浏览器仍然会下载后备图像，增加了开销

3.使用iframe
<iframe src="svg">
  <img src="png">
</iframe>
缺点：如果浏览器不支持iframe，将会回退


响应式图片：可以在不同屏幕和分辨率的设备上都能良好工作以及其他特性的图片
正文内容被设置的最大宽度是1200像素：在高于此宽度的情况下，正文内容会保持在1200像素，并处于可用空间的正中间，在低于此宽度的情况下，会保持可视宽度的100%

colspan rowspan
表格中如果要给每一列设置样式：
使用<colgroup>
      <col>
      <col>
    </colgroup>代表表格的每一列
<caption>表格的标题
tfoot包含的一行永远都回出现在表格的最后，不管你把它的代码放在哪里，thead也一样
<form>
  <fieldset>
    <legend>表单的描述</legend>
  </fieldset>
</form>
readonly：用户不能修改输入的值
下拉列表：可以用multiple来进行多选，也可以<optgroup>造成视觉包裹效果
自动补全：使用<datalist id="文本框list属性的值">
                <option>可能的值</option>
             </datalist>
    <input type="text" id="username" list="id">
    accept来限制用户上传文件的类型
    html发送文件：1.post方法，因为文件内容不能放在url参数中2.将enctype设置multipart/form-data
    
    安全问题:XSS：跨站脚本攻击，发生在当您将用户发送的数据显示给这个用户或者另外一个用户时 CSRF、SQL注入、http数据头注入和电子邮件注入
    
    
    html5验证，在表单元素通过验证后，可以使用css :valid来进行样式控制，没有通过验证的，可以使用:invalid来进行样式控制
    pattern:正则表达式验证
    
    如果想自定义错误提示信息，可以使用Html5使用的setCustomValidity
    
    在form元素上使用Novalidate来禁止浏览器的自动验证
