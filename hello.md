# Hi. 这里是兔子

年前为这个域名续了费，就想着怎么也得更新一下子，毕竟已经荒废两年多了。忙了一个多月的工作，又发生了许多的事情，到 3 月底终于鼓起勇气，恩，开更吧。其实吧，原由还有很多，认识了 mogu 大爷，然后掉进了 julia 的坑，然后不知怎么的就聊起了 elm。哦哦，那个我知道，其实我很早就在关注了，那时才刚刚出来，貌似是 0.10 的版本？不过由于工作忙，初次见面之后就那样了，第一影响是 wtf……第二次见面是因为 redux。在 redux 的官网上看到了他的实现受到 elm 的影响，我才突然想起来，哦，我的天，他貌似比想象的要强大的多，同时版本也更新到了 0.12 左右。写了几个 demo 发现，太难了，和传统的逻辑思维根本不同，之后又弃在那里。又过去一年半的时间，对 FRP 编程慢慢有了些了解后再来折腾 elm，发现，啊！好像突然懂了什么。

恩，还没有做自我介绍。我是兔子，一个 frontend developer，是个喜欢看书，喜欢编程，喜欢折腾各种奇怪的东西的女汉子。技术栈的话一下也想不出来，今后会在 blog 中慢慢提现吧。那么现在，不如就聊聊这个 blog。

## 全是些奇怪的东西

功能很简单的三个页面，也算是 1.0 版。两三天的工作量为嘛做了一个月之久呢。所以说，Just for fun。总的来说收获是很大的，也想分享给大家我的研究成果。

前端部分：

* [CoffeeScript](http://coffeescript.org/)
* [Stylus](http://stylus-lang.com/)
* [Postcss](http://postcss.org/)
* [Webpack](https://webpack.github.io/)
* [Elm](http://elm-lang.org/)

后端部分：

* [RAML](http://raml.org/)
* [PostgREST](http://postgrest.com)
* [Nginx]()
* [PostgreSQL]()

接下来当然是挨个介绍。

## Coffee Tea Or Me ?

先来杯咖啡吧主人！恩，我喜欢蓝山，味道很浓厚，香喷喷，不喜欢加糖；猫屎咖啡也喝过几次，有点略苦。闲下来我也会自己煮咖啡，一杯只要 80 元。

哦哦，这里的主角是 CoffeeScript。现在听到的关于 Coffee 最多是，“有了 ES6 还要 Coffee 干嘛？”，所以我要说，你错了，Coffee 并不是你想象的样子，细算下来，我用 Coffee 也有四年左右了。他给我的第一感觉就是，干净！写 Coffee 像是在写小说，就那样一行一行的写。说是没用的，举个栗子好了。

这是一个简单的 demo，大致意思是如果地址栏地址末尾带着`\`，就去掉他，否则就保持原样。我们先来 es6 版本：

```javascript
let path  = location.pathname
let path1 = path.match(/\/$/) ? path.slice(0, -1) : path
```

接下来是 coffee :

```coffeescript
path       = location.pathname
isSlashEnd = path.match /\/$/
trimPath   = path.slice 0, -1
path1      = if isSlashEnd then trimPath else path
```

好像 es6 版本更简单一些，好吧，我承认，es6 的确很厉害，我每天都在用，但是！更喜欢 coffee 多一些的是他的表达式。就好像在讲故事一样按顺序把故事讲完，这种感觉很舒服。

es6 有些语法和 coffee 也很相似，应该是用的最多的箭头函数了吧：

```javascript
[1, 2, 3, 4, 5].reduce((a, b) => a + b) //=> 15
```

再来看看这个：

```coffeescript
[1..5].reduce (a, b) -> a + b #=> 15
```

差不多，是吧？哦，对了，箭头函数除了写起来更清晰之外，还有另外一个重要作用，就是可以绑定 this：

```javascript
$.get(url).then(res => this.setState({ datas: res }))
```

这个 coffee 也有：

```coffeescript
$.get url
 .then (res) => @setState datas: res
```

我知道这里你会讲 coffee 的坏话，因为 coffee 编译出来是这样的代码：

```javascript
$.get(url).then((function(_this) {
  return function(res) {
    return _this.setState({
      datas: res
    });
  };
})(this));
```

很丑陋。恩，还有这样那样的问题也很多，什么性能啊，安全啊什么的。不过，coffee 代码颜值高，这就够了。因为我可以接下来慢慢的欣赏。


## 笔尖的旋律

来说出你最喜欢的 css 预编译器吧。sass 么？我知道你会说这个，我也喜欢，不过那是之前的事了。现在哀家有了新宠，那就是 stylus，真真是极好的。

三大预编译器你木有听说过么？less，sass，stylus。那放弃 sass 而选择 stylus 的理由是什么呢？

首先，sass 有的，stylus 都有。stylus 有的，sass 不一定有。

其次，stylus 代码写起来颜值也很高，sass 写多了会烦，而 stylus 不会。

最后，stylus 可以调用 js，而 sass 需要做 ruby 插件。我相信各位大牛的 Js 水平都是飞上天的，但 ruby 就不一定了，c++？呵呵呵呵。

还是先来聊聊 sass 吧，来说说他是如何被打入冷宫的。我们都知道 sass 有两个版本，两种格式。两个版本指的是 ruby-sass 和 libsass，前者需要 ruby 来编译，后者需要 c++；两种格式是说 Sass 和 SCSS，你一定看出了里边的诚意。这两种格式主要的区别是有没有缩进，Sass 的代码是依赖缩进的，很清晰，但是相信大家并没有怎么用过；SCSS 就像个进化版 css，语法格式和样式表类似。

格式并没有什么问题，版本则是个大坑。ruby-sass 版本要超前一些，有一些很有用的功能，比如说他支持 BEM 写法，缺点是编译速度慢，慢，慢的厉害。libsass 是 c++，编译的很快，但是功能受限，一般来说是安装 node-sass 来用 libsass 编译。对，就是这个恶心的地方！你想要使用 BEM 就必须得先装 ruby，再用 gem 去装 sass。而然，gem 整个被墙掉了，需要换源，好像最近x宝的源还没法用了，只能换 ruby-china 或是翻墙，着实麻烦的很。我为了一个 sass 还要装个 ruby？好的……对了，之前的版本貌似不支持中文，还要在 ruby 源码里改一个地方……

如果你和我一样喜欢清晰的语法，我向你推荐 stylus。stylus 是 TJ 的作品，TJ 是谁？就是那个写 express 的 hentai 啦。顺便一提，coffee 的作者写了 backbone 和 underscore……好吧，既然是出自大牛的手笔，质量什么的就放心好啦。

接下来就展示一下语法，先从基本的选择器开始吧：

```stylus
fz = 14px

.test
  font-size 14px
  color alpha(black, 0.56)
  
  &:hover
    color dark(black)
    
  &-1
    margin 0 1rem
  &-2
    padding 1rem 0
    
    ^[0]:active
      background transparent
```

没有花括号，没有分号，甚至也可有没有冒号，就像函数调用。当然，肯定少不了 mixins 和 extends：

```stylus
transform()
  -webkit-transfrom arguments
  transfrom arguments
  
$flex-center
  display flex
  justify-content center
  align-items center
  
.con
  transform()
  @extend $flex-center
```

你还能在文档中找到 function，@media，hash，循环这些 sass 中的东西。这里再来展示一下 stylus 和 js 的默契配合：

```json
// media-queries.json
{
  "small": "screen and (max-width: 480px)"
}
```

```stylus
json('media-queries.json')

@media small
  .test
    font-size 90%
```

看到这里我相信你会慢慢爱上他的。

如果你用过 compass 的话，那么 stylus 还有个很厉害的框架，叫做 [nib](http://tj.github.io/nib/)，名字就可以看的出实力。好吧，就先这么多。

## 写起来放心，用着舒心

对于 css，我们有了很厉害的矛，就是牛到天上的各种预处理器，不过呢，我们还有更强大的盾。天啊！这是 css 的后处理器，叫做 postcss。所以说，这个东东到底是做什么的。后处理器，字面意思上说就是把产品再加工。如果你有下列需求，那么他很适合你：

* 我需要给属性加前缀来兼容手机端和旧浏览器；
* 样式表写的太麻烦了，想要简单一些；
* 我想要尝试下一代 css 草案中的语法；
* 我在用 react

那么说，postcss 有一系列的插件，很多很多，利用他们就可以做完上面的需求。首先是加前缀的问题，这需要用到 autoprefixer，就不需要细说了，大家都懂的；那第二点是什么意思呢？这里用到了另外一个 postcss 插件，叫做 short，他打包了一些常用语法，比如：

```stylus
.div1
  size 5rem 3rem
.div2
  size 1rem
```

这会编译为：

```css
.div1 {
  width:  5rem;
  height: 3rem;
}
.div2 {
  width:  1rem;
  height: 1rem;
}
```

还有：

```stylus
.footer
  position fixed * 0 0 0
```

我想，你已经猜到了，这会编译成：

```css
.footer {
  position: fixed;
  right:  0;
  bottom: 0;
  left:   0;
}
```

那么下一代语法是怎么回事呢？还是举个栗子好了：

```css
:root {
  --red: #d33;
}
.test {
  color: var(--red)
}
```

还需要解释么？这她喵的就是变量。最后是 react，为嘛 react 需要 postcss 呢？其实不如说 react 需要 css modules。什么鬼？我们都知道 react 的尿性是 Anything to Js，css 也不例外，按照 react 的特点，css 也有了模块的特性，还是来个栗子好解释一些：

```css
/* style.css */

.navBar {
  display: flex;
  align-items: center;
}
```

```javascript
// nav-bar.jsx

import styles from "./style.css"
import React, { Component } from "react"

export default class NavBar extends Component {
  render() {
    return <nav class={styles.navBar}>{this.props.children}</nav>
  }
}
```

而且，css 模块之间还能互相组合，简直了。

不得不说，套了两层 Buff 的 css 现在真的是非常厉害。

## 来打包吧

说到 Js，一个一直以来很都比的事情就是，他没有模块的概念。当然，写一些小程序也用不到什么模块，但项目规模一大之后，这就是个问题了。从最开始的 IIFE，到后来的 requireJS 的 AMD 模块，nodejs 的 CMD 模块，再到后来的 UMD 模块，ES6 模块系统，模块化开发已经不是什么问题了。那么，我们还需要将这些模块打包在一起。

webpack 来做这个，再合适不过，他的作用就是打包，打包，再打包。打包 Js，打包 css，打包图片，还能打包字体……，还能打包 txt，markdown……真的是越来越离谱了。总的来说，webpack 是靠各种 loader 和插件来打包成一个`bundle.js`。当然也能打包成多个，这由你来设置。webpack 相信大家都用过了。

当然，webpack 除了打包之外还提供一些其他很厉害的功能。一般来说也要介绍 webpack-dev-server。这是一个服务器，可以配合 webpack 开发功能。那么他们有哪些变态功能呢？首先不得不说的就是热交换 HMR 了。我们的代码更改之后，就会替换`bundle.js`中对应的部分，这可以大大提升我们开发效率，当然和 file watcher 并不是一路货色，自己体会吧。接下来要说的就是代码分割和异步加载功能。当文件东西太多时，我们可能会用到代码分隔，直观理解就是会分解成多个文件。那么异步加载呢？这个就厉害了。当在做 SPA 时，就会用到这个功能，我们并不需要将整个`bundle.js`全部功能都加载，在路由层，当路由到时我们通过异步加载的方式按需加载代码，这样就可以大大减小`bundle.js`的体积，使页面加载的更快。

但是那需要用到`require()`，作为 ES6 脑残粉怎么能容忍 require 出现呢，所以在新版的 webpack，也就是 webpack2 中出现了 System 加载器，这个东东就可以让 require 见鬼去了。当然，除了新的加载器，webpack2 的配置也会变的更简单和容易扩展，值得一提的是代码压缩功能，webpack2 压缩代码的体积要更小一些。

最近也试了试最新的`webpack@2.1.0.beta.5`和`webpack-dev-server@2.0.0-beta`，结果嘛，你懂的，各种报错搞崩溃了。查 issues 手动修复了几处 bug 成功跑了起来，感觉也确实是不一样的。

## 开始之前一定要好好设计

下面要一并说两个东东，他们是 RAML 和 postgREST。这还要从 emberJs 开始说起。

记得很清楚开始接触 RESTful 时是学习 emberJs 的时候。虽然 RESTful 这个词很早就听说过，也在玩 rails 的时候简单玩过，但因为工作的原因迟迟没有用到，也就忘了个干净。后来在 ember-data 中大量使用了起来，不得不关注起 Api 方面的东东，结果后来还出了 jsonapi 。怎么说呢，这些东西可以简单理解为 url 到资源的映射关系，我喜欢表达丰富的家伙，当然也就爱上了他。与 Java 时代不同的是，这不会只返回 200,404,500，或是清一色的 POST 请求。RESTful 有很多的状态码，201，204，还有不止 GET 和 POST 的请求，而且 url 也与平常的静态文件目录结构不同，他含有丰富的信息。既然这样，那一定有一个设计 API 的工具，木有错，就是 RAML。

还是先来看个栗子的好，恩，就来这个 blog 所用的吧：

```yaml
#%RAML 1.0
title: Post API
version: v1
baseUri: http://www.yufi.me/api/{version}/post
mediaType application/json

types:
  Post:
    type: object
    properties:
      title: string
      datetime: date
      istop: boolean
      intro: string
      filepath: string
      
/post/{postId}:
  get:
    responses:
      200:
        body:
          application/json:
            schema: Post
```

当然，我省略了一些东东，大概部分就是这些，主要由基本信息，类型和路径规则构成。上面的这段也就是从服务器获取文章的路由规则，所匹配的地址是`http://www.yufi.me/api/v1/post/1`。也有很多的前端工具可用，相当的方便。

说到 RESTful 的话有个工具是一定一定要提一下的，这也是我用了好久的东东，那就是 postgREST。这个东东可以算是个小型服务器，数据库链接 postgreSQL，内置了一个 warp 服务器，性能很快，也很方便使用。他有自己的一套路由规则，习惯之后就会上瘾，像普通的取值，排序都很容易做到，比如我像取 id 为 1 的文章只需要请求`/post?id=eq.1`，或者是取用户的某些字段并排序：`/user?age=gte.17&order=score.dest`。由于 postgreSQL 9.4.2 支持 Json，所以他也支持 Json 查询，并且还支持分页，只需要配置一下头信息：

```HTTP
Range-Unit: items
Range: 0-10
```

把他俩放在一起说，恩，其实是一个愿望，是希望 postgREST 快点支持 RAML，这样就不用我去写工具手动支持了，233。至于 nginx 和 postgreSQL 的话并木有什么可以分享的东东，不过也想简单聊聊。

话说我最近玩了下 nginScript，这玩意很有趣，可以在 nginx.conf 中写Js。虽然骂声好像不少的样子，不过挺有趣的，他有点像写 node，来看看这个好了：

```nginx
http {
  js_set $hello "
    var s = ''
    s += 'hello '
    s += ' world'
    ";

  server {
    listen 8080;
    
    location / {
      return 200 $hello;
    }
  }
}
```

是不是很有趣。我们知道 nginx 是有 lua 模块的，很厉害，如果 js 也可以像 lua 模块那样就更好了，不过他目前还在测试版。

然后 postgreSQL 呢，是我最喜欢的数据库，特别是再支持了 JSON 之后，mongoDB 就被弃在了一边。你说 MySQL？那是什么 0 0？

## 这就是为什么要放在最后才说的原因

好吧，如果你忍着性子看到这里，我先要对你表示感谢，然后呢，我要告诉你一件很重要的事情。你一定发现了我有一个东西还没有介绍，并不是我忘记了，而是我想把他放在最后。这是因为，如果你不喜欢他，就一丁点都不会接受；如果对他有点点兴趣，就会彻底喜欢上他，这就是最后要介绍的东东，Elm。
