---
title: 参与一个 GitHub 开源项目
tags:
  - open
categories:
  - github
date: 2018-11-01 20:43:12
---

gitHub是一个面向开源及私有软件项目的托管平台，因为只支持git 作为唯一的版本库格式进行托管，故名gitHub。gitHub作为开源项目的著名托管地，可谓无人不知，越来越多的个人和公司纷纷加入到Github的大家族里来，好多人都想为开源尽一份绵薄之力。对于个人来讲，我们把自己的项目托管到gitHub上并不表示我们参与了gitHub开源项目，只能说我们开源了自己的项目，可以任别人自由下载。那么该如何参与gitHub的开源项目呢？相信很多人都有这方面的疑问，网上也有一些参差不齐的教程教大家如何“pull request”、如何“commit”等等。但这些教程往往不够全面或不够完全正确，搞不好可能让我们陷入一个误区。
下面将涵盖我们在一个典型的项目中可能出现的事情以及如何为开源项目作出贡献。

## 找项目

我们推荐从已正在使用的或感兴趣的项目开始。这里有几个很棒的地方供参考：

**[GitHub Explore](https://github.com/explore)**：受欢迎和热门的项目。
**[GitHub Stars](https://github.com/stars?direction=desc&sort=created)**：被其他人star过的项目（指的是我们自己库的项目）。
**[GitHub Showcases](https://github.com/collections)**：一个能搜索相关库的方法。
**[LayerVault News](https://www.designernews.co/)**：前端和设计相关的项目。


## Github开源项目中可能遇到的因素

### Community（社区）
项目通常会有一个社区维护，由不同角色（正规或非正规）的其他用户组成：
**所有者（Owner）**：即创建该项目且在他们Github账户上有该项目的用户或组织。
**维护者和协作者（Maintainers and Collaborators）**：致力于一个项目并促进该项目发展的用户。通常所有者和维护者是同一个用户或组织，他们对项目库都有写的权限。
**贡献者（Contributors）**：每一个对该项目发出过pull request并合并到项目中的用户都是贡献者。
**社区成员（Community Members）**：即那些经常使用且非常关心该项目的用户，他们在讨论功能特征和pull request上非常活跃。

### Docs（文档）
一般项目中都有的文件。

### Readme
几乎所有的Github项目都包含一个`README.md`文件。readme提供了该项目的一个概览及关于如何使用、构建甚至如何贡献于一个项目的相关细节。

### Contributing
项目和项目维护者不同，所以每个项目所期望的作贡献的最佳方法也会有所不同。一定要注意一个标注为`CONTRIBUTING`的文档，Contributing文档详细描述了一个项目的维护者希望看到贡献的补丁或功能应该符合怎样的规格。这可能包含要写什么测试，代码语法规范或补丁集中的区域。

### License
一个LICENSE文件当然就是该项目的许可证了。一个开源项目的license会告诉用户他们能做和不能做的（例如使用、修改、重新发布），及告诉贡献者他们允许其他人做的。有许多的办法对开源项目加上许可证，我们可以在[choosealicense.com](https://choosealicense.com/)读到更多的关于每个许可证的含义。

### Documentation and Wikis
许多大型项目有的不只有一个readme来指导人么如何使用他们的项目。在这种情况下我们通常能够发现一个指向库中名为“docs”的另一个文件或文件夹的链接。另外，该库也可能使用Github wiki来代替文档。

## 参与项目
既然我们已经找到了理解该项目的相关资料，下面我们就可以采取一些行动了。

### 创建话题
如果我们发现了正在使用的项目中的一个bug（但是我们不知道怎么去修复它），或对文档有不解或对项目有疑问 — 那么创建一个话题吧！这非常容易且一般我们不管创建什么话题，我们都可能不是唯一一个出现该问题的人，所以其他人可能会发现我们的话题很有帮助。关于更多的话题介绍，请查看我们的[Issues guide](https://guides.github.com/features/issues/)。

#### 话题专业提示
在建话题之前检查已有的话题：话题重复对双方都无利，所以搜索整个正开放和已关闭的话题以检查我们遇到的问题是否已经有人解决了。
务必对自己的问题有清晰的认识：期望的结果是什么？然而却发生了什么？ 详细描述其他人如何重现该问题。
在像[JSFiddle](http://jsfiddle.net/)或[CodePen](https://codepen.io/)类似的平台上重现该问题并给出问题demo的链接。
包含一些系统相关的细节，比如用的什么浏览器、库或操作系统及版本号。
在我们的话题或在Gist里贴出我们的错误输出或日志。如果在话题里贴出来，请用三个反引号 \`\`\`，包围起来使得能够良好的呈现给大家。

### Pull Request
如果我们能够修复bug或自己添加功能 — 太棒了，请发一个pull request 吧！确保我们已经读过任何关于contributing的文档，且需要理解license以及已经签过CLA（如果需要的话）。一旦我们提交了一个pull request，维护者就会将我们的分支与已有的分支作比较来决定是否要合并（即pull in）我们作的改动。

#### Pull Request专业提示
* [Fork](https://guides.github.com/activities/forking/)**该项目库**及将它clone到本地。通过添加为远程的方式在本地连接到原来的‘upstream’库。经常从‘upstream’库**pull in**改动以保持库最新，这样当我们提交pull request时，就不大可能发生合并冲突了。点[这里](https://help.github.com/articles/syncing-a-fork/)看更多的指导细节。
* 为我们的编辑**单独建立一个**[分支](https://guides.github.com/introduction/flow/)。
* **务必清楚**所出现的问题以及如何重现该问题或为什么我们的功能有帮助。然后同样的要清楚做一些改变有哪些步骤。
* 最好测试一下。在任何已有的测试（如果存在）上运行我们所做的改动并在必要时创建新的测试。不管测试存不存在，都要确保我们的改动不会破坏已有的项目。
* 如果我们的改动包含了HTML/CSS方面的不同，那么请包含改动前和改动后的截图。将我们的图片拖放到我们pull request的正文里。
* 尽我们所能的在项目的风格上多做努力。这可能意味着使用不同于我们自己Github库中采用的缩进，分号或注释，但是这让维护者更容易合并，也让其他人更容易理解和以后的维护。

### 开放的Pull Requests
一旦我们打开一个pull request，就会有一个讨论，围绕我们提出的改变作出探讨。其他的贡献者和用户可能会参与进来，但最终由维护者做决定。我们可能会被要求对我们的pull request做一些改变，如果这样，请给我们的分支添加更多的commit并push它们 — 它们将自动的加入到已有的pull request里。

如果我们的pull request被合并了 — 太好了！如果没被合并的话，也没什么大不了的，也许这不是项目维护者所期望看到的改动，亦或者他们已经致力于该bug或功能。这种情况有可能发生，所以我们的建议是：对收到的结果做出反馈，进一步努力然后再次pull request出去— 或者创建我们自己的开源项目。

## 大致流程
### 首先需要在github上注册账号并登陆，这个不多说了
### 安装git，到github官网下载安装包。
### 为账号添加添加ssh key
### fork我们想参与的开源项目
浏览github上的开源项目，然后点击fork，这时就跳转到了我们的账号下，此项目就是我们账号下的一个项目了。fork就相当于把别人的项目克隆到自己的账号下一份，以后我们的修改都应是提交到我们自己github账号下的这个项目中，我们是没有权限直接push到原作者账号下的项目中的。

### clone项目到本地
#### 复制项目clone地址
注意是clone自己账号下的项目地址，不是原作者的，原作者的我们虽然也可以clone到本地，但是我们是没push权限的。还要注意这里咱们使用ssh协议，所以要选择ssh类型的地址。

### 将项目原地址添加为远程仓库
复制原作者的项目地址，添加为自己的一个远程仓库，用来实时将原项目的修改更新到咱们本地并合并。注意也是复制ssh协议类型的地址哦。
``` bash
$ git remote add upstream 原作者的远程仓库
```
使用 git remote -v可以看到我们有两个仓库一个origin，咱们自己的github仓库；一个upstream，原作者的远程仓库。当然也可以不用upstream这个名字。

### 创建branch，用于添加自己的修改
这只是一个约定成俗的方式，当然我们也可以在master上添加修改，创建新的branch添加自己的修改的好处是，我们可以同时添加多个修改，在一个修改还没有被原作者merge时，我们可以用master创建新的branch继续我们的其它修改。
在这里我们在新添加的分支上修改：执行如下命令
``` bash
$ git branch test  # 创建test分支

$ git checkout test   # 切换到test分支
```
然后就可以添加我们的修改了。

### 将修改push到我们的github上
由于我们的github上还没有test分支，所以我们得把命令写全了：
``` bash
$ git push origin test:test
```
我们的修改已经push到了我们的github下了，但是我们要向原作者请求合并到原项目中，如果原作者合并了，也就意味着我们是此项目的贡献者了。到我们的github上点击pull request按钮，创建一个pull request。提交完pull request，原作者就会看到我们的合并请求，我们就等待原作者是否采纳了。

## 注意事项
1、clone时一定要注意选择ssh协议的链接。否则可能导致clone失败，或者后续push失败。

2、将公钥添加到github后，一定要更新自己当前的私钥（命令：ssh-add ~/.ssh/id_rsa），否则会push失败。
