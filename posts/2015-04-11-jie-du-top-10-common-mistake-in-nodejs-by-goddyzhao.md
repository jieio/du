## [解读] 10个 Node.js 开发者最常犯的错误

by [@goddyzhao](https://github.com/goddyzhao)

本文解读自 [toptal](http://www.toptal.com/) 的文章——[Need Node.js Help? Check These Top 10 Common Node.js Developer Mistakes](http://www.toptal.com/nodejs/top-10-common-nodejs-developer-mistakes)，文章地址： http://www.toptal.com/nodejs/top-10-common-nodejs-developer-mistakes

文中提到了 10 个 Node.js 开发者最常犯的错误，笔者记得类似的文章很早就有了，这些错误基本都是对JS中异步编码不熟悉会犯的，笔者挑了几个比较有意义的拿出来给大家分享下，希望对Node新手有所帮助（特别是从其他语言转过来的）。

下文中错误编号和原文都保持一致。

### 错误#1：阻塞事件循环

原文中给了如下这段代码例子：

```javascript
  function sortUsersByAge(users) {
    users.sort(function(a, b) {
      return a.age < b.age ? -1 : 1;
    })
  }
```

代码本身其实是没问题，只是当`users`数据量很大的时候，这段代码就会阻塞主线程。所以，类似这种对数据做排序的操作，尽量在查询`db`的时候交给`db`去排序，排好再拿出来。当然，要是数据拿过来就是没排序的，非得要排序那也没办法，正如原文中提到的，这个世界木有银弹！

### 错误#2：多次调用同一个回调函数

原文中的例子是正确的例子，我把它改成了错误的写法方便大家看：

```javascript
  module.exports.verifyPassword = function(user, password, done) {
    if(typeof password !== ‘string’) {
      done(new Error(‘password should be a string’))
    }

    computeHash(password, user.passwordHashOpts, function(err, hash) {
      if(err) {
        done(err)
        return
      }
      
      done(null, hash === user.passwordHash)
    })
  }
```

发现问题了吗？没错，`done(new Error...`这段代码完成后木有`return`就会导致`computeHash`执行后再次调用`done`，这种问题一不小心就会漏写`return`，要时刻小心。另外笔者觉得，实在会忘记呢，就记得每次`if`完后写好`else`也行。

### 错误#3：深度嵌套回调

这个老生常谈的问题了，就像这样：

```javascript
  db.f1(function (err, data1) {
    db.f2(data1, function (err, data2) {
      db.f3...
    });
  });
```

这种问题其实代码执行上没问题的，只是代码很难看，而且可读性很不好。解决方案就是用各种类似`Q`、`Async`等库或者es6中的`generator`。

### 错误#6：在回调中抛异常

来看下错误代码：

```javascript
  try {
    db.User.get(userId, function(err, user) {
      if(err) {
        throw err
      }
      // ...
      usernameSlug = slugifyUsername(user.username)
      // ...
    })
  } catch(e) {
    console.log(‘Oh no!’)
  }
```

上述代码在回调中抛异常是捕获不到的，这也是为什么`Node`中都是`cb(err)`这类代码。

