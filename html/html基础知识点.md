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


# <span id = "basic">基础知识点</span>
1. html中块级元素不会被嵌套进内联元素中，但是可以被嵌套在其他块级元素中
2. keywords已经被废弃，因为作弊者填充了大量的Keywords，导致错误的引导了搜索引擎的搜索结果
3. 给网站设置主语言
```
<html lang="zh">
```
4. 文档锚点，在要跳转的元素上增加一个id属性，在```<a>```的```href```属性中使用#ID。给```<a>```元素增加```download```属性，代表下载资源，href属性中放要下载的资源路径
5. 电子邮件链接
```
<a href="mailto:邮箱号?cc=抄送&bcc=密件抄送&subject=主题&body=主体">
```
6. 定义列表
```
<dl>
  <dt></dt>
  <dd></dd>
</dl>
```
7. 引用：如果一个块级元素是被引用的内容，应该使用
```
<blockquote cite="https://www.baidu.com">
	<p>这一段话来自于我</p>
</blockquote>
```
其cite属性指向引用的url，浏览器在渲染块引用时，会默认缩进

如果是行内元素，则需要用
```
<p>后面这句话是被<q cite="https://www.baidu.com">引用的内容</q></p>
```
同样的，在其上使用cite属性指向引用的url
8. 缩略语
```
<abbr title="Hypetext Markup Language">HTML</abbr>
```
9. 上标和下标
```
<sup>  上标superscript
<sub>  下标subscript
```
# <span id="icon">给网站增加自定义图标</span>
```
<link rel="icon" type="image/x-icon" href="路径">
```
给网站的自定义图片最好选用.icon格式，16*16像素的图片
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
如果图片的内容对网站有意义，应该使用html的方式，这样可以设置该元素的```title```和```alt```属性，如果对网站无意义，则应该使用css去设置
2. 图片元素的语义容器，让图片和标题具有联系应该使用```<figure>```元素，将图片和内容具有联系，当然```<figure>```中不仅仅可以包含图片
```
<figure>
  <img>
  <figcaption></figcaption>
</figure>
```
3. 可以使用```<video>```元素来在网页上显示一段视频，可以设置其属性```controls```，让用户可以控制视频
```
<video src="测试小视频.mp4" controls>
  <p>备选文字</p>
</video>
```
在```<video>```元素中的```<p>```元素是当浏览器不支持```<video>```标签时，将显示后备文本。

由于各个浏览器对视频格式的兼容性不同，所以你应该设置多个后备选项
```
<video controls>
  <source src="测试小视频.mp4" type="video/mp4">
  <source src="测试小视频.webm" type="video/webm">
</video>
```
给```<source>```元素设置type属性的意义是为了浏览器在加载时去读取type属性，从而跳过不支持的格式，如果不设置type属性，那么浏览器就会一个一个加载视频来判断，将耗费大量的时间。
4. ```<video>```的新属性： 
autoplay：自动播放，即使其他内容还没有完全加载
loop：循环播放，默认为1
muted：播放时自动静音
poster：指向一个图片的url，用来在视频还没有播放时去显示图片，用于粗略的预览
preload：用来缓冲较大的文件，none不缓冲，auto页面加载后去缓存媒体文件 metadata仅缓冲文件的元数据

5. 插入音频使用
```
<audio>
```
因为音频文件只有控制条，没有像视频那样的视觉组件，所以除了```poster```、```width```、```height```以外其余属性和```<video>```相同
6. WEBVTT
webVTT格式，简单来说字幕文件，使用时用```<track>```标签，将其放在```<source>```元素的最后，kind属性说明是哪种类型的，```srclang```属性用来告诉是什么语言编写的
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
1. 基本属性：
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

优点：svg矢量中的文本仍然可以访问，有利于seo。

缺点：非常容易变复杂，会在浏览器处理中占用很长的处理时间，兼容性差（ie9开始支持），比位图更难创建。

svg在html页面中的使用可以使用两种方式：
1. 使用```<img>```标签
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
2. 使用内联的```<svg>```标签
```
<svg width="300" height="200">
    <rect width="100%" height="100%" fill="green" />
</svg>
```
优点：减少了http请求，可以为svg分配class和id，并使用css来控制样式，内联的svg是唯一可以使用css进行交互，包括伪类和动画，同样也可以作为链接。
缺点：只适合在一个地方使用svg，多次使用将导致资源密集型维护，会额外增加html文件的大小，浏览器不能像缓存普通图片一样缓存svg，svg中可以增加回退，但是对于支持svg的浏览器来说，仍然会加载后备图片或文本，为了兼容旧浏览器而极大的增大了开销
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
3. ```<thead>```和```<tfoot>```不论写在代码中的什么位置，都会出现在表格第一行和表格最后一行
# <span id="form">表单基础</span>
1. 写法
```
<form>
  <fieldset>
    <legend>表单的描述</legend>
  </fieldset>
</form>
```
2. 下拉列表，使用```<optgroup>```造成视觉包裹效果，使用```multiple```属性进行多选
3. 自动补全
```
  <input type="text" list="datalist的ID">
  <datalist id="与文本框list属性相对应">
    <option></option>
  </datalist>
```
4. 上传文件时使用```accept```属性来限制用户上传文件的类型，必须使用post方法提交表单，将```ecctype```设置为```multipart/form-data```
5. ```css:valid```控制通过验证样式，```css:invalid```控制不通过样式，```pattern```设置正则表达式验证
# <span id="safe">网站安全问题</span>
1. XSS
	XSS是指跨站脚本攻击，通过在网站的输入框写入```script```脚本或文件，如果网站未进行过滤，将会解析该脚本，如果该脚本获取的是网站的cookie，就会导致很严重的问题。
	
	1.1 在html中注入
	```
	<div>${content}</div>
	```
	当content为
	```
	<script>alert("XSS")</script>
	```
	代码会变为
	```
	<div><script>alert("XSS")</script></div>
	```
	页面将会执行```alert("XSS")```。
	防御手段：  可以通过转义等手段来进行简单的防御，把```<```和```>```分别转义为```&lt;```和 ```&gt;```。
	
	1.2 通过html属性注入
	```
	<img src=${src}>
	当${src}为
	2"onerror="alert("XSS")"
	```
	代码变为
	```
	<img src="2" onerror="alert("XSS")">
	```
	防御手段：将```"```转义为```&quto;```
	1.3 通过Javascript代码来注入
	```
	var mydata = "${data}";
	当data为hello";alert("XSS")时，代码变为：
	var mydata = "hello";alert(3);"";
	``` 
	防御手段：将```"```转义为```\```
	XSS利用的是用户对网站的信任
2. CSRF
	CSRF是指跨站请求访问，在用户不知情的情况下，冒充其身份发起一次请求
	防御：1.Get请求不对数据进行修改 2. 不让第三方网站访问到用户的cookie 3.阻止第三方网站的请求接口 4. 请求时附带验证信息

3. iframe的安全隐患：攻击向量

单点劫持：将隐藏的iframe嵌入到文档中，并使用被隐藏的iframe来捕获用户交互，误导用户操作并获取敏感信息

措施：在必要的时候才使用iframe、使用https减少远程内容在传输过程中被篡改的可能性，https防止嵌入式内容访问父文档的内容，反之亦然，在使用了https后，各大知名公司都会检测src路径、始终使用sandbox来进行沙盒化，默认情况下，应该使用没有参数的sandbox属性来强制执行所有可用的权限，如果真的需要，单独添加参数放开权限，但是不能同时使用allow-script和allow-same-origin属性，在这种情况下，嵌入式内容可以绕过阻止站点执行脚本的同源安全策略，并使用Javascript来关闭沙盒、配置SCP指令，提供一组HTTP标头，可以防止其他网站在其网页中嵌入您的内容
# <span id="seo">seo概念及相关优化</span>
在代码层面进行seo优化：
1. ```h1~h6```这6个标题，一个页面最好不要超过三个，对于```h1```大标题，一个页面最好只出现一次，但是对于```html5```来说，每个具有结构大纲的元素都可以有自己独立的```h1```标题
2. 使用```html5语义化标签```
3. ```img```必须设置```alt```属性，如果宽度和高度固定，则同时写固定值
```
<img src="logo.png" alt="logo" width="100" height="100">
```
4. 对于不需要追踪爬行的链接，设置```nofollow```属性，一般可用于博客评论、论坛帖子、留言板，也可以用于广告链接和隐私政策、用户登录条款等方面
5. URL：越短越好，避免过多参数，目录层次尽量少。文件和目录名具有描述性，字母全部小写

# <span id="DOCTYPE">!DOCTYPE html的作用</span>
```!DOCTYPE html```用来告诉Web浏览器页面使用了哪种HTML版本，浏览器能够了解预期的文档类型

# <span id="model">标准模式和怪异模式</span>
标准的显示方式：标准模式
不标准的显示方式：页面没有定义```!DOCTYPE html```或```DOC```内容出错的情况下都会进入怪异模式。
既可以显示标准的，也能够显示不标准的，属于过渡类型：准标准模式

											一枚小菜鸡~~~~~如有错误，感谢指正
