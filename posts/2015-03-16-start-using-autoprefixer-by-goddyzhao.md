## 快用 autoprefixer 解放你双手吧

by [@goddyzhao](https://github.com/goddyzhao)

今天开门见山，直接上代码：

```css
    -webkit-transition: all 4s ease;
    -moz-transition: all 4s ease;
    -ms-transition: all 4s ease;
    -o-transition: all 4s ease;
    transition: all 4s ease;
```

对上面的代码不陌生吧！在CSS 3中部分新特性标准尚未定稿，或者浏览器有非标准的实现，这个时候就需要为不同浏览器添加上类似上面这样的代码才能生效，官方说法叫： `vendor prefix`。下面这个简明的列表就罗列出了不同浏览器对应的前缀：

1. Chrome: -webkit-
2. Firefox: -moz-
3. IE: -ms-
4. Opera: -o-
5. Safari: -webkit-
6. iOS: -webkit-
7. Android: -webkit-


但是每次都要这么写是不是也是醉了？那么怎么解放你的双手呢？方法其实有很多，比如：

1. 利用类似 Sass、Less、Stylus 这类支持可编程 CSS 的工具，再通过mixin的方式
2. 利用编辑器插件（如 prefixr ），直接在书写完类似 `transition: all 4s ease` 后选中按下快捷键直接自动插入包含浏览器前缀的内容

今天呢，笔者推荐大家一个名为 [autoprefixer](https://github.com/postcss/autoprefixer) 的工具，它让你书写 CSS 代码时候完全不需要去关心那些浏览器前缀，在你部署前，运行下它就会自动为你加上前缀，最重要的是，它会实时去 [caniuse.com](http://caniuse.com) 检查你书写的属性是否需要添加前缀。拿我们一开始的例子就是：

你只要书写这样的代码（假设在 `app.css` 文件中）：

```css
    transition: all 4s ease;
```

然后安装 [grunt-autoprefixer](https://github.com/nDmitry/grunt-autoprefixer) 或者 [gulp-autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer)，并定义如下任务（以 grunt 为例）：

```javascript
  grunt.initConfig({
    autoprefixer: {
      options: {
        browsers: ['last 2 version']
      },
      app: {
        src: 'app.css',
        dest: 'app.css'
      }
    }
  });
```
这里`browsers`部分的配置表示只看最新两个版本的浏览器，你还可以根据浏览器份额来定义，如： `> 5% ` 这样的，具体配置查看官网即可。

然后，运行上述任务就会自动为你添加上对应的前缀了。


