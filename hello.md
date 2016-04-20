# Hi. 这里是兔子

年前为这个域名续了费，就想着怎么也得更新一下子，毕竟已经荒废两年多了。忙了一个多月的工作，又发生了许多的事情，到 3 月底终于鼓起勇气，恩，开更吧。其实吧，原由还有很多，认识了 mogu 大爷，然后掉进了 julia 的坑，然后不知怎么的就聊起了 elm。哦哦，那个我知道，其实我很早就在关注了，那时才刚刚出来，貌似是 0.10 的版本？不过由于工作忙，初次见面之后就那样了，第一影响是 wtf……第二次见面是因为 redux。在 redux 的官网上看到了他的实现受到 elm 的影响，我才突然想起来，哦，我的天，他貌似比想象的要强大的多，同时版本也更新到了 0.12 左右。写了几个 demo 发现，太难了，和传统的逻辑思维根本不同，之后又弃在那里。又过去一年半的时间，对 FRP 编程慢慢有了些了解后再来折腾 elm，发现，啊！好像突然懂了什么。

恩，还没有做自我介绍。我是兔子，一个 frontend developer，是个喜欢看书，喜欢编程，喜欢折腾各种奇怪的东西的女汉子。技术栈的话一下也想不出来，今后会在 blog 中慢慢提现吧。那么现在，不如就聊聊这个 blog 吧。

## 全是些奇怪的东西

功能很简单的三个页面，也算是 1.0 版。两天的工作量为嘛做了一个月之久呢。所以，Just for fun。总的来说收获是很大的，也想分享给大家我的研究成果。

前端部分：

* [CoffeeScript](http://coffeescript.org/)
* [Stylus](http://stylus-lang.com/)
* Postcss
* Handlebars
* Webpack
* Elm

后端部分：

* Nginx
* PostgreSQL
* PostgREST

接下来当然是挨个介绍。

## Coffee Tea Or Me ?

主人，先来杯咖啡吧～我喜欢蓝山，味道很浓厚，香喷喷，不喜欢加糖；猫屎咖啡也喝过几次，有点略苦。闲下来我也会自己煮咖啡，一杯只要 80 元。

哦哦，这里的主角是 CoffeeScript。现在听到的关于 Coffee 最多是，“有了 ES6 还要 Coffee 干嘛？”，所以我要说，你错了，Coffee 并不是你想象的样子，细算下来，我用 Coffee 也有四年左右了。他给我的第一感觉就是，干净！写 Coffee 像是在写小说，就那样一行一行的写。说是没用的，举个栗子好了。

这是一个简单的 demo，大致意思是如果地址栏地址末尾带着`\`，就去掉他，否则就保持原样。我们先来 es6 版本：

```js
let path  = location.pathname
let path1 = path.match(/\/$/) ? path.slice(0, -1) : path
```

接下来是 coffee :

```coffee
path       = location.pathname
isSlashEnd = path.match /\/$/
trimPath   = path.slice 0, -1
path1      = if isSlashEnd then trimPath else path
```

好像 es6 版本更简单一些，好吧，我承认，es6 的确很厉害，我每天都在用，但是！更喜欢 coffee 多一些的是他的表达式。就好像在讲故事一样按顺序把故事讲完，这种感觉很舒服。

es6 有些语法和 coffee 也很相似，应该是用的最多的箭头函数了吧：

```js
const add = (a, b) => a + b
[1, 2, 3, 4, 5].reduce(add) //=> 15
```

再来看看这个：

```coffee
[1..5].reduce (a, b) -> a + b #=> 15
```

差不多，是吧？哦，对了，箭头函数除了写起来更清晰之外，还有另外一个重要作用，就是可以绑定 this：

```js
$.get(url).then(res => this.setState({ datas: res }))
```

这个 coffee 也有：

```coffee
$.get url
 .then (res) => this.setState datas: res
```

我知道这里你会讲 coffee 的坏话，因为 coffee 编译出来是这样的代码：

```js
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

最后，stylus 可以调用 js，而 sass 需要做 ruby 插件。我相信各位大牛的 Js 水平都是飞上天的，但 ruby 就不一定了。

还是先来聊聊 sass 吧，来说说他是如何被打入冷宫的。我们都知道 sass 有两个版本，两种格式。两个版本指的是 ruby-sass 和 libsass，前者需要 ruby 来编译，后者需要 c++；两种格式是说 Sass 和 SCSS，你一定看出了里边的诚意。这两种格式主要的区别是有没有缩进，Sass 的代码是依赖缩进的，很清晰，但是相信大家并没有怎么用过；SCSS 就像个进化版 css，语法格式和样式表类似。

格式并没有什么问题，版本则是个大坑。ruby-sass 版本要超前一些，有一些很有用的功能，比如说他支持 BEM 写法，缺点是编译速度慢，慢，慢的厉害。libsass 是 c++，编译的很快，但是功能受限，一般来说是安装 node-sass 来用 libsass 编译。对，就是这个恶心的地方！你想要使用 BEM 就必须得先装 ruby，再用 gem 去装 sass。而然，gem 整个被墙掉了，需要换源，好像最近x宝的源还没法用了，只能换 ruby-china 或是翻墙，着实麻烦的很。我为了一个 sass 还要装个 ruby？好的……对了，之前的版本貌似不支持中文，还要在 ruby 源码里改一个地方……

如果你和我一样喜欢清晰的语法，我向你推荐 stylus。stylus 是 TJ 的作品，TJ 是谁？就是那个写express 的 hentai 啦。顺便一提，coffee 的作者写了 backbone 和 underscore……好吧，既然是出自大牛的手笔，质量什么的就放心好了。

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

没有花括号，没有分号，甚至也可有没有冒号。当然，肯定少不了 mixins 和 extends：

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

如果你用过 compass 的话，那么 stylus 还有个很厉害的框架，叫做 [nib](http://tj.github.io/nib/)，名字就可以看的出实力。好吧，就这么多。

## 写起来放心，用着舒心


