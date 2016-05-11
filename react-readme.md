# React 从入门到放弃

> #1 Q：React是什么？

A：React是一个视图层框架，他的主要作用是将程序的状态映射为虚拟dom，然后用虚拟dom来替换真实dom

> #2 Q：React有哪些部分组成？

A：React有两个库，分别为`react`和`react-dom`。`react`提供了组件的相关功能，大量用到的`Component`就出自这里，`react-dom`与dom相关，比如我们要将React标签插入目标dom节点就需要用到`react-dom`的`render`方法。

> #3 Q：React是框架么？

A：是，也不是。是是因为React很强大，只用他就可以构建出我们想要的程序；不是的原因是，他并不如大型框架的功能齐全，像Angular，Ember等，比如说，React没有路由。

> #4 Q：React需要会Js么？

A：是的，需要掌握Js语法，尤其是对this的绑定和对集合的操作。

> #5 Q：React需要会ES6么？

A：不需要，不过推荐入手学习ES6。学习和使用ES6可以让代码逻辑更加清晰，也易与其他工具搭配模块化开发。

> #6 Q：如果我想使用ES6的语法来写React，需要做哪些准备工作呢？

A：由于浏览器兼容性问题，目前普遍的做法是将ES6代码转为各浏览器厂商广泛支持的ES5代码。编译工具可以选择babel或Typescript等，推荐使用babel。安装babel我们需要提前安装nodejs与npm包管理器，可以使用npm用下面的命令安装：

```shell
npm i -D babel-core babel-preset2015 babel-react
```

安装完成后我们可以使用webpack工具打包es6代码。

> #7 Q：React必须使用nodejs么？

A：不是必须。由于React中的JSX语法需要编译为React的虚拟dom树，如果不使用nodejs来编译，我们只能将JSX编译器加载到浏览器中，但是编译器体积一般较大，为了提高性能，通常还是使用工具来编译而不是将编译器加载到浏览器中。使用babel的babel-react插件配合工具打包就可以编译JSX。同理，如果我们写ES6代码也是需要编译的。所以在开发阶段，我们需要使用nodejs来构建我们的项目。但是作为练习和快速熟悉这么做还是可以的。

> #8 Q：React项目为什么需要使用webpack？

A：webpack的作用是打包代码，有助于我们进行模块化开发。通过使用模块的导入导出，我们可以将代码切割为多个部分，也更容易整合第三方代码库。此外，webpack还提供了诸多有用的功能，如代码切割，异步加载等，这些我们在开发过程中也可能会用到。

> #9 Q：开发React需要会nodejs么？

A：不需要。更多情况下nodejs只是作为一个构建工具来使用，这就是说我们并不需要较为深入的研究nodejs，只要会使用工具就足够了。但我还是建议学习nodejs，他对于我们定制化工具来说是必须的。

> #10 Q：React学习过程一般是多久？

A：一般来说一个月时间就可以掌握，三个月就能达到理解层次，不过还是要跟自身的努力程度而决定。

> #11 Q：我要如何开始学习React？

A：首先要先完成阅读官方的**getting start**，对React的基本语法形式有个初步的了解。如果想要尝尝鲜，可以像这样创建一个`index.html`，库资源使用免费的CDN即可：

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Hello World</title>

    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/react/15.0.2/react.js"></script>
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/react/15.0.2/react-dom.js"></script>
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
  </head>
  <body>
    <div id="app"></div>

    <script type="text/babel">
      const Hello = React.createClass({
        render: function() {
          return (<h1>Hello world!</h1>)
        }
      })

      ReactDOM.render(
        <Hello />,
        document.getElementById('app')
      );
      </script>
  </body>
</html>
```

在浏览器中打开文件，会看到`Hello world`标题。当然，还有中更好的办法尝试，那就是使用在线的Js沙箱环境，如[jsbin](jsbin.com)，在`HTML`选项卡中填入：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
  <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/react/15.0.2/react.js"></script>
  <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/react/15.0.2/react-dom.js"></script>
</head>
<body>
  <div id="app"></div>
</body>
</html>
```

`JavaScript`选项卡要选择JSX(React)：

```javascript
const Hello = React.createClass({
  render: function() {
    return (<h1>Hello world!</h1>)
  }
})

ReactDOM.render(
  <Hello />,
  document.getElementById('app')
);
```

也可以达到相同的效果。当然，前面也提到过的就是，这只是作为联系和快速熟悉可以这么做，实际当中我们需要构建一个React工程。

> #12 Q：要如何构建一个React工程

A：首先我们需要[nodejs](http://nodejs.org)，如果还没有安装，那么在nodejs的官网网站下载并安装他。

