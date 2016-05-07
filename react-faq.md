# React FAQ

> Q：React是什么？

A：React是一个视图层框架，他的主要作用是将程序的状态映射为虚拟dom，然后用虚拟dom来替换真实dom

> Q：React有哪些部分组成？

A：React有两个库，分别为`react`和`react-dom`。`react`提供了组件的相关功能，大量用到的`Component`就出自这里，`react-dom`与dom相关，比如我们要将React标签插入目标dom节点就需要用到`react-dom`的`render`方法。

> Q：React是框架么？

A：是，也不是。是是因为React很强大，只用他就可以构建出我们想要的程序；不是的原因是，他并不如大型框架的功能齐全，像Angular，Ember等，比如说，React没有路由。

> Q：React需要会Js么？

A：是的，需要掌握Js语法，尤其是对this的绑定和对集合的操作。

> Q：React需要会ES6么？

A：不需要，不过推荐入手学习ES6。学习和使用ES6可以让代码逻辑更加清晰，也易与其他工具搭配模块化开发。

> Q：如果我想使用ES6的语法来写React，需要做哪些准备工作呢？

A：由于浏览器兼容性问题，目前普遍的做法是将ES6代码转为各浏览器厂商广泛支持的ES5代码。编译工具可以选择babel或Typescript等，推荐使用babel。安装babel我们需要提前安装nodejs与npm包管理器，可以使用npm用下面的命令安装：
'''shell
npm i -D babel-core babel-preset2015 babel-react
'''
安装完成后我们可以使用webpack工具打包es6代码。

> Q：React必须使用nodejs么？

A：不是必须。由于React中的JSX语法需要编译为React的虚拟dom树，如果不使用nodejs来编译，我们只能将JSX编译器加载到浏览器中，但是编译器体积一般较大，为了提高性能，通常还是使用工具来编译而不是将编译器加载到浏览器中。使用babel的babel-react插件配合工具打包就可以编译JSX。同理，如果我们写ES6代码也是需要编译的。所以在开发阶段，我们需要使用nodejs来构建我们的项目。但是作为练习和快速熟悉这么做还是可以的。

> Q：React项目为什么需要使用webpack？

A：webpack的作用是打包代码，

