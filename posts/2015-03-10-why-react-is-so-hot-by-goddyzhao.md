## 为什么React.js这么火
![](http://du.jie.io/img/reactjs.png)

by [@goddyzhao](https://github.com/goddyZhao)

就当大家还沉浸在[Angular.js](https://angularjs.org/)巨爽无比的双向数据绑定（Two-Way Data Binding）以及快速的代码编写时，Facebook用[React.js](http://facebook.github.io/react/)瞬间就完成了逆袭。一时间，各大技术社区，论坛，充斥着关于React.js的新闻，大家都开始重新思考前端的框架到底应该是怎么样的，连Angular在2.0中也来了个翻天覆地的变化。

其实Angular和React不属于同一类的东西，Angular是一个框架，而React更多是负责UI视图部分，大家普遍认为React是MVC中的V。

那么到底为什么React.js一下子就火起来了呢？个人觉得可能主要是因为以下几个因素所导致的：


### 单向数据绑定

就在满世界夸赞双向Data Binding好的时候，React说我默认只支持单向数据流，因为在[冯诺依曼体系](http://en.wikipedia.org/wiki/Von_Neumann_architecture)中，数据就是单向流动的。这么一来，小伙伴们都震惊了，纷纷去Google双向和单向数据绑定的区别。单向绑定确实相比之下要更加轻，但事实上呢，双向绑定的需求也确实是存在的，比如：用户填写表单的时候，填写的值就需要更新到Model中，所以，React其实也有通过addon React Link来提供这个功能。只是他默认是不支持双向数据绑定的。

### 虚拟DOM

关于虚拟DOM的好坏，业界众说纷纭，这里不做评价。但单从这个概念本身起码让大家觉得是个新东西。所谓虚拟DOM就是说，在React中如下这段代码：

~~~javascript
  React.render(
    <div className="commentBox">
      Hello, world! I am a CommentBox.
    </div>
  );
~~~

这里的`div`其实和DOM中的div完全是两码事儿了，只不过React提供了和DOM类似的Tag和API，事实上React会通过他自己的逻辑去转化为真正的DOM。所以，把这种重做虚拟DOM。

那么这样做有什么好处呢？最明显的一点好处就是React所谓的`dom diff`，能够实现delta级别的dom更新。当有数据变动导致DOM变动时，React不是全局刷新，而是通过它内部的`dom diff`算法计算出不同点，然后以最小粒度进行更新。这也是React号称性能好的原因。

其次，还有一点非常好的地方就在于，有了虚拟DOM就可以让UI脱离设备，换句话说，只要有对应的转化关系，如：虚拟DOM -> 浏览器DOM，就能进行渲染。[React Native](http://www.reactnative.com/)就是一个很好的例子，它把虚拟DOM转化为Native UI组件，这样理论上就解决了DOM在移动端性能的问题。当然，缺点也是有的，比如：就无法和已有的原生DOM组件进行兼容。

### JSX

JSX其实本质上是一种新的语言，只不过它设计成JavaScript一种扩展，所以，其语法绝大部分都和JavaScript一样。而同时它搭配一个JSX Transform的工具可以将JSX编译为原生的JavaScript。

那么这样做好处是什么呢？当然了，首要任务就是让你写代码方便点，否则想想每次都要`React.createElement`也是醉了！

其次呢，另一个好处就是它可以让你书写ES6之类的语法，就和CoffeeScript是一个道理，最终它会翻译到浏览器兼容的语法。

### 背后有Facebook这条大腿

Facebook这条大腿支撑着React的开发，在项目活跃度和质量上自然是可以得到保证的。就好比Angular背后有Google一样，相比之下，Ember.js就薄弱了不少，尽管有[@wycats](https://github.com/wycats)、[@tomdale](https://github.com/tomdale)这样的大牛，但是毕竟个人和大企业还是不能相比的。

其实纵观以上几点都有一个共性就是`推陈出新`，上述这些点是否真的如它描述的那么好另当别论，但最起码，它提出了一些新的概念。新鲜的东西总是能够吸引大家的眼球的。

本文仅表达个人对React火爆原因的粗浅分析，不对其好坏做评价。其实，说React比Angular好或者反过来都是没有意义的，各自都有各自的优缺点，大家也不要盲目的从众，根据自己应用的特点选择合适的才是王道。