# Hi. 这里是兔子

年前为这个域名续了费，就想着怎么也得更新一下子，毕竟已经荒废两年多了。忙了一个多月的工作，又发生了许多的事情，到 3 月底终于鼓起勇气，恩，开更吧。其实吧，原由还有很多，认识了 mogu 大爷，然后掉进了 julia 的坑，然后不知怎么的就聊起了 elm。哦哦，那个我知道，其实我很早就在关注了，那时才刚刚出来，貌似是 0.10 的版本？不过由于工作忙，初次见面之后就那样了，第一影响是 wtf……第二次见面是因为 redux。在 redux 的官网上看到了他的实现受到 elm 的影响，我才突然想起来，哦，我的天，他貌似比想象的要强大的多，同时版本也更新到了 0.12 左右。写了几个 demo 发现，太难了，和传统的逻辑思维根本不同，之后又弃在那里。又过去一年半的时间，对 FRP 编程慢慢有了些了解后再来折腾 elm，发现，啊！好像突然懂了什么。

恩，还没有做自我介绍。我是兔子，一个 frontend developer，是个喜欢看书，喜欢编程，喜欢折腾各种奇怪的东西的女汉子。技术栈的话一下也想不出来，今后会在 blog 中慢慢提现吧。那么现在，不如就聊聊这个 blog 吧。

## 全是些奇怪的东西

功能很简单的三个页面，也算是 1.0 版。两天的工作量为嘛做了一个月之久呢。所以，Just for fun。总的来说收获是很大的，也想分享给大家我的研究成果。

前端部分：

* CoffeeScript
* Stylus
* Elm
* Handlebars
* Webpack

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

