## Tessel 2 官方已经支持 io.js 咯！

![](http://jie-du.qiniudn.com/img/tessel2.png)

by [@goddyzhao](https://github.com/goddyzhao)

很多朋友可能对 [Tessel](https://tessel.io/) 不大了解，但是你肯定对 [Raspberry Pi](http://www.raspberrypi.org/) （国内叫：树莓派）不陌生吧！Tessel 就是和 Raspberry Pi 类似的产品。但是它号称可以以最快的速度在 Tessel 上开发原型。

![](http://jie-du.qiniudn.com/img/tessel.JPG)

和 Raspberry Pi 需要装个类似 [Raspbian](http://www.raspbian.org/) 这样的操作系统，再安装好Node才能运行JavaScript不同， Tessel 原生就提供了 JavaScript运行环境，可以直接使用自己喜欢的IDE或者编辑器书写完脚本后，直接 `push` 到 tessel上就可以运行了。 [Tessel] 一开始就支持Node和NPM，而就在前几天， [Tessel 官方宣布了 Tessel 2 已经支持 io.js 了](https://tessel.io/blog/112888410737/moving-faster-with-io-js)

官方提出之所以那么快去支持 io.js 主要出于以下几方面的考虑

1. 功耗
2. JS/Node 的兼容性
3. 支持依赖二进制包的npm模块

Tessel 最早考虑给 JavaScript 提供一个运行环境有两种方案，一种就是直接使用V8，另外一种就是自己写一个。那么最终权衡下来还是采用了V8，因为V8天生就可以兼容 Node 和 io.js。而且目前来看 io.js 是向下兼容 Node 的，所以支持 io.js 对社区来说也是一件很好的事情。

解读：其实从我们上次 @imsobear 发出的 io.js 周报不难看出，io.js 社区得到了各个企业的大力支持：为了让 io.js 能够有持续集成的环境以及不同的测试环境，厂家们纷纷有机器的捐机器，有开发能力的出人力。这次Tessel 又在这么短的时间内宣布支持 io.js 这个对 io.js也好，对Node也好都是很利好的消息。对嵌入式有兴趣的朋友，也可以尝试下 Tessel。

