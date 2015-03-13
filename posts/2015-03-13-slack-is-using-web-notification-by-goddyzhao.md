## Slack已经耍起了Web Notifications了！

by [@goddyzhao](https://github.com/goddyzhao)

本文从一个名叫Stewart Butterfield的人开始，何许人也？此人就是大名鼎鼎的Flickr的联合创始人，有意思的是，这个人当时是一心要做一款游戏的，结果游戏失败了，作为其中一项功能的Flickr却火了。Yahoo将Flickr收入囊中后呢，这家伙一心要再做一款游戏，结果历史总是惊人的相似，游戏没火却又把子项目——[Slack](https://slack.com)给带火了。这就是Slack背后比较有意思的八卦故事，所以呢，简单来说Slack就是一款企业团队间沟通的IM工具，要了解更多大家可以去他们官网——https://slack.com了解。而本文着重讲讲Slack所使用的`Web Notifications`技术！

其实Web Notifications是一项[W3C的标准](http://www.w3.org/TR/notifications/)，目的是允许web应用可以通过JS代码直接唤出桌面提醒（类似早期Mac下的Growl）。来看下Slack中的例子：

![](http://7x2w6i.com2.z0.glb.qiniucdn.com/img/slack-setting-notification.jpg)

上图中箭头部分就是Slack中的`桌面提醒`功能设置，点击`Send test notification`之后，就能看到如下提醒效果：

![](http://7x2w6i.com2.z0.glb.qiniucdn.com/img/slack-notification.png)

其实`Web Notifications`标准的草案早在`2010年`就有了，只是当时没有得到很多应用的原因是大部分浏览器都不支持。笔者记得貌似当时只有safari是支持的，现在主流的浏览器都已经支持了（IE除外），下面是一张来自[caniuse.com](http://caniuse.com/#feat=notifications)关于这项标准的支持情况：

![](http://7x2w6i.com2.z0.glb.qiniucdn.com/img/caniuse-notifications.jpg)

而使用这项技术本身也非常简单，无外乎以下几个步骤：

1. 检查用户当前浏览器是否支持`Web Notifications`
2. 支持，就向用户发起权限申请
3. 得到用户允许后就可以通过对应的API来创建提醒了

下面就`Show You The Code`：

### 1. 检查用户当前浏览器是否支持Web Notifications

根据[W3C标准中](http://www.w3.org/TR/notifications/)所说明的，要检查当前浏览器是否支持，只要查看`window`对象上是否有Notification构造函数就可以了，所以，通过如下简单的代码就可以完成检查工作：

```javascript
  if (window.Notification) {
    // 浏览器支持
  }
```

但是呢，支持不意味着就立马可以用，还需要通过`Notification`上的`permission`属性来看是否有权限，这个属性有如下三个值：

1. default - 未知状态，不确定用户是否允许或拒绝
2. denied - 用户拒绝
3. granted - 用户允许

### 2. 支持，就向用户发起权限申请

除非该值直接就是 `granted` 否则都应该去主动询问用户获取权限，就像这样：

```javascript
  Notification.requestPermission(function (status) {
    // status值为denied或者granted
  });
```
这里要注意，一旦用户做出了选择（允许或者拒绝），再执行这个方法就不会有任何反应了。

### 3. 得到用户允许后就可以通过对应的API来创建提醒了

一旦用户允许之后呢，就可以发送提醒了，就像这样：

```javascript
  var n = new Notification('title', {
    body: '我是Goddy',
    icon: 'https://avatars3.githubusercontent.com/u/164988?v=3&s=460'
  });
```
然后就能看到提醒了：

![](http://7x2w6i.com2.z0.glb.qiniucdn.com/img/goddy-notification.jpg)

除非用户手动点击右上角的 `x` 否则提醒是不会自动关闭。通常我们可以在隔了一段时间之后把它自动关闭掉，那么就可以这样：

```javascript
  n.close();
```

就是这么简单。大家也可以根据各自应用的类型来选择是否要使用这种方式。





