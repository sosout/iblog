---
title: NPM依赖包版本号~和^的区别及最佳实践
date: 2018-05-01 23:56:07
tags:
    - npm
categories:
    - nodejs
---
我们经常发现项目的依赖包版本号前面有的是 ~，有的是 ^，我们以 angular 为例：

![img1.png](/images/npm-package-version/img1.png)

**那么 ~ 和 ^ 有什么作用和区别？**
* **~：**匹配最近的小版本依赖包，比如~1.2.3会匹配所有1.2.x版本，但是不包括1.3.0。
* **^：**匹配最新的大版本依赖包，比如^1.2.3会匹配所有1.x.x的包，包括1.3.0，但是不包括2.0.0。

**实际项目中我们该如何选择呢？**

**固定版本：**首先我们可以指定特定的版本号，直接写1.2.3，前面什么前缀都没有，这样固然没问题，但是如果依赖包发布新版本修复了一些小bug，那么需要手动修改package.json文件。
**^版本：**^版本虽然不需要手动修改package.json文件就可享用修复后的依赖包，但^版本之间跨越比较大，更甚至有些高版本于低版本不兼容。
**~版本：**^版本不仅不需要手动修改package.json文件，也不像^版本之间跨越比较大，这样可以保证项目不会出现大的问题，也能保证包中的小bug可以得到修复。
**\*版本：**\*版本意味着时刻安装最新版本的依赖包，缺点同^版本，可能会造成版本不兼容。

综上所述，实际项目中我们推荐用 ~ 版本。