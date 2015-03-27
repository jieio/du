## React Native 真的来了！
![](http://jie-du.qiniudn.com/img/react-native.jpg)

by [@goddyzhao](https://github.com/goddyzhao)

今天一早起来就收到了官方一封邮件，标题为：*It's time, Let's Use React Native*。所有此前订阅过官方邮件通知的朋友们都应该已经收到了这封邮件。这也意味着：React Native 真的来了！

笔者大致看了下基本的内容，为大家做一个简单的介绍

1. `React Native` 和 `PhoneGap` 以及 `Ionic` 都不同，后者是给你 JavaScript 的代码提供原生系统的API接口，等于做了一个 `bridge`，但是你的代码还是跑在 `webview` 或者类似 `webview` 的容器中；而前者它是将虚拟DOM直接映射到原生的组件（真的是原生的），这样关于transition各种性能上的诟病理论上都能够得到很好的解决。非要拿它和现有的比的话，那最接近的就是 `Titanium` 了！
2. 主线程负责跑JavaScript应用层代码，其他原生的操作如：图片解码，文件操作等都在其他线程完成，不阻塞主线程的UI，想尽一切办法保证UI的流畅
3. 非常牛逼哄哄的调试支持，直接可以用Chrome的Developer Tool去调试你的代码，不管你的代码是在模拟器中运行还是真机上运行
4. 实现了类似iOS的Touch处理系统，可以非常方便的进行用户操作的捕获和处理
5. 默认支持Flexbox的布局模型
6. 提供了可扩展性，可以将你已有的原生插件以扩展的方式接入进来，不过笔者通过 Github 问了[是否支持Swift写扩展](https://github.com/facebook/react-native/issues/284)，不过很遗憾，得到的答案是不能，由于Facebook内部都是用 Objective-C 因此没有打算对Swift做支持，希望得到社区的帮助

虽然以上这些特性听上去非常的赞，但是笔者也要提醒大家以下几点：

1. `React Native` 目前的只提供了iOS的实现，Android尚未支持，而且官网也没说什么时候会支持
2. 目前发布的版本号是：`0.1.0`，关于这个版本号不用我说大家也明白这意味着不适合直接拿来在生产环境中使用了
3. `React Native` 尽管才发布1天不到，但是目前 open 的 issue 数量是 `91`

笔者认为比较明智的应该是对 `React Native` 保持持续关注，同时可以去尝试下，写写试试，一方面对它有个熟悉，同时也可以对社区做贡献，等到它后续版本更加稳定再投入到生产环境可能是比较好的做法。切勿单纯为了追求新技术而用新技术，如果你是公司产品，那带来的后果可能是非常致命的，当然了如果是你个人的练手项目，那当然没问题，本身既然 `Reactive Native` 已经发布，不管版本号很低，但是起码也保证了相对稳定性。