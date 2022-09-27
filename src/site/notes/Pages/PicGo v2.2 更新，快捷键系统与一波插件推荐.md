---
{"dg-publish":true,"dg-permalink":"/pages/cc-2022-09-27-113615/","permalink":"/pages/cc-2022-09-27-113615/","dgHomeLink":true,"dgPassFrontmatter":false}
---

# PicGo v2.2 更新，快捷键系统与一波插件推荐 

> [!quote] 本文剪藏自[PicGo v2.2 更新，快捷键系统与一波插件推荐 - 少数派 (sspai.com)](https://sspai.com/post/58223)

## 前言

距离上次更新 (v2.1.2) 已经过去 8 个月了。很抱歉这段时间以来，作为开发者的我并没有给它加入所有预期的功能。不过除了小修小补之外，2.2 版本还是做了一个我觉得比较重要的功能——快捷键系统。除了介绍一些新功能之外，还会介绍一些我觉得做得很棒的插件们，因为它们赋予了 [PicGo](https://github.com/Molunerfinn/PicGo) 更强的生命力。

## 快捷键系统

在此前，我曾收到一些用户的需求：「能否给 PicGo 的剪贴板图片上传的快捷键加个开关？」。当时的 PicGo 只留给了用户设定快捷键的入口，但是却没有一个开关能启用或者禁用快捷键。因此我当时的建议是，如果快捷上传这个功能用不到，可以先设定一个基本用不到的快捷键，然后等待新版本更新加入开关的功能。

如果只是加入一个快捷键的开关，自然不需要这么久的开发。我在考虑这件事的时候，还想着能否给插件也配上快捷键的能力？于是在参考了许多其他软件的快捷键系统的设计与实现之后，我将 PicGo 底层的快捷键系统重写了一遍，让 2.2 版本的 PicGo 插件也能注册快捷键了。

新版的快捷键设置从单一的弹窗变成了一个快捷键列表：

![](https://cdn.jsdelivr.net/gh/Molunerfinn/test/picgo/20200101204942.png)

在快捷键列表上你可以选择禁用、启用或者编辑某个功能对应的快捷键，让误碰的情况降到最低。同时插件也能支持快捷键注册，在快捷键列表可以看出快捷键来自于 PicGo 本身还是某个插件、这个快捷键的作用是什么。

也许有人觉得这个功能没什么值得大书特书的。确实，它可能不是一个很重要的功能，但是有一些插件利用好快捷键系统，能让 PicGo 更好用。比如我现在要介绍的 PicGo 的官方插件：[picgo-plugin-quick-capture](https://github.com/PicGo/picgo-plugin-quick-capture)。

### picgo-plugin-quick-capture

PicGo 在很多人看来还不够好用，主要是在 `截图→PicGo快捷上传→获取URL` 这个流程中，由于 PicGo 没有截图功能，还是需要两步（先用其他工具截图，再用快捷键让 PicGo 上传以获取 URL）才能实现。

而这个插件可以将 `截图→PicGo快捷上传→获取URL` 这个流程缩短到一步：一个快捷键即可实现。效果如下：

![](https://camo.githubusercontent.com/48bcf2b6eaea25e78535ccf3483fe7af979446fb/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f4d6f6c756e657266696e6e2f746573742f506963476f2f717569636b2d636174702e676966)

它的实现就依托了 PicGo 的快捷键系统。原理就是在插件快捷键触发的时候，调用预置的截图脚本开始截图；当用户截图结束后，触发 PicGo 的上传逻辑，从而实现一键获取图片 URL 的高效工作流。

同时截图脚本用户可以根据自己的喜好自定义，只要能在命令行跑起你的截图脚本，配置这个插件也一样能跑起来。目前插件预置了 Windows 和 macOS 两个系统的截图脚本：

![](https://camo.githubusercontent.com/1b5317025f44dee492a0a1cb068a8ab79d330a73/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f4d6f6c756e657266696e6e2f746573742f506963476f2f32303139313232383139333434302e706e67)

相信这个插件能给你带来更好的贴图体验。

## PicGo-Server

从这个版本开始，PicGo 内置了一个非常小型的服务器（有多小型？没有用框架，直接用 node 原生写的...），也就是说你可以通过 HTTP 请求的方式让 PicGo 来上传图片了。

PicGo 默认监听 `127.0.0.1:36677`，当然，如果你能保证环境安全的情况下，改成 `0.0.0.0:36677` 也是可以的，这样你就可以远程通过 HTTP 来调用 PicGo 来上传图片了哈哈。

相关调用方法参考 PicGo 文档 - [高级技巧](https://picgo.github.io/PicGo-Doc/zh/guide/advance.html#picgo-server%E7%9A%84%E4%BD%BF%E7%94%A8)篇，本文就不再赘述啦。

## 插件推荐

PicGo 今年 1 月份的时候更新了 2.0 版本正式支持插件系统，到目前马上一年了。其实发布之后我是很虚的，毕竟 PicGo 还不算一个很出名的工具，使用者不多，使用者里是开发者的就更少了。不过意外的是还是有一些开发者很热心地为 PicGo 开发了插件。有很多用户在 issue 里会一直询问「xxx 图床是否支持呢？」「希望支持 xxx 图床」，殊不知 PicGo 已经有很多插件支持这些图床了。因此，今天我也想推荐一下这些优秀的插件，让更多的人知道它们，完整的插件列表可以在 [Awesome-PicGo](https://github.com/PicGo/Awesome-PicGo) 看到 ：

### 1. [vs-picgo](https://github.com/PicGo/vs-picgo)

使用 VSCode 写 markdown 的你，在没有安装 PicGo 客户端的情况下，也可以用这个 VSCode 的插件来使用大部分 PicGo 提供的功能。

### 2. [picgo-plugin-github-plus](https://github.com/zWingz/picgo-plugin-github-plus)

这个插件提供了比 PicGo 自带的 GitHub 图床支持更多的功能：删除操作同步、可以同步 GitHub 里图片的记录、支持 gitee 等。

### 3. [picgo-plugin-web-uploader](https://github.com/yuki-xin/picgo-plugin-web-uploader)

这个插件提供了自定义图床上传的功能，可以自定义上传的 header、body 等字段，来实现一些第三方图床的上传支持。

### 4. [picgo-plugin-qingstor-uploader](https://github.com/chengww5217/picgo-plugin-qingstor-uploader)

这个插件提供了[青云图床](https://www.qingcloud.com/products/qingstor/)的上传功能。

### 5. [picgo-plugin-super-prefix](https://github.com/gclove/picgo-plugin-super-prefix#readme)

这个插件可以很优雅地生成图片文件存储路径。

### 6. [picgo-plugin-smms-user](https://github.com/xlzy520/picgo-plugin-smms-user)

这个插件新增了 SM.MS 注册用户的支持。使用了 [SM.MS](http://xn--sm-os3c914l.ms/) V2 的 API 上传，适用于注册了 SM.MS 的用户。

### 7. [picgo-plugin-gitlab](https://github.com/bugwz/picgo-plugin-gitlab)

这个插件提供了 GitLab 上传的支持

### 8. [picgo-plugin-gitee](https://github.com/zhanghuid/picgo-plugin-gitee)

这个插件提供了 Gitee 上传的支持

### 9. [picgo-plugin-nextcloud-uploader](https://github.com/jiajiajia343434/picgo-plugin-nextcloud-uploader)

这个插件提供了 NextCloud 上传的支持

### 10. [picgo-plugin-watermark](https://github.com/Dec-F/picgo-plugin-watermark)

这个插件能在图片上传前给图片加上水印，可以自定义水印位置、样式等。**仅支持 2.2.0 + 版本的 PicGo**，不过由于用到了原生模块编译的原因，暂时无法在 PicGo 的插件界面直接安装，需要按照 [README](https://github.com/Dec-F/picgo-plugin-watermark#installation) 的方法来安装使用。

### 11. [picgo-plugin-pic-migrater](https://github.com/PicGo/picgo-plugin-pic-migrater)

这个插件提供了 Markdown 文件图片 URL 地址的图床搬家功能。不过目前还不稳定，会出现失败的情况，可以尝鲜使用。

### 12. [picgo-plugin-quick-capture](https://github.com/PicGo/picgo-plugin-quick-capture)

这个插件上文已经提到了，**仅支持 2.2.0 + 版本的 PicGo**，提供一键截图 + 上传的功能。

等等...

相信未来会有更多更有用、更有意思的插件出现在 PicGo 这个平台上。

PS: 官方的同步插件（基于 GitHub 私人仓库）将在 2.3 版本完成图片列表信息与配置信息分离后上线。

## 其他更新

除了快捷键系统更新了之外，PicGo v2.2.0 版本还做了一些其他方面的更新：

1.  Electron 版本升级到 v6.1.7，具有更佳的性能
2.  优化底层架构，降低内存占用，提升性能
3.  优化启动流程，加快了启动速度
4.  配置添加 alias 选项，能够在配置菜单页、配置对话框中显示配置项的别名（通常是英文→中文）
5.  针对 macOS 的 dark-mode 重新制作了顶部栏图标
6.  Windows 新增 scoop 下载方式
7.  能够用于上传的图床列表与「选择显示的图床」配置做了联动，现在是显示的图床才能被选择
8.  依赖的框架由 electron-vue 转为 vue-cli-plugin-electron-builder ，开发阶段更快的编译速度、更友好的调试方式、以及从 JS 转为 TS，能避免更多的低级错误。后期将考虑加入自动化测试。
9.  修改检查更新的方式，之前从 GitHub 获取最新版本的方式最近发现会被限流。

## 未来的计划

未来的计划在此前有粗略的进行了规划，可以参考 「[PicGo 开发计划](https://github.com/Molunerfinn/PicGo/issues/265)」，不过这个计划是很早以前规划的。就目前而言，我自己觉得比较有意思、有意义的未来计划如下：

1.  已上传图片列表与单纯的配置分离，方便不同设备同步配置与图片列表
2.  i18n 国际化系统支持，目前暂时仅考虑支持英文
3.  网页上的图片拖拽上传支持
4.  插件进程独立化。目前插件和 PicGo 跑在同一进程里，未来将把插件们运行在一个独立进程中，避免插件出错导致主体崩溃。
5.  插件的 UI 化支持，考虑提供给插件 UI 界面让插件拥有更丰富的想象空间，比如提供一个 webview 容器让插件自定义界面。
6.  文件夹内图片上传支持
7.  界面重构，目前界面太过 WEB 化，将界面优化成更接近桌面客户端的 UI。（基于此甚至可以制作一个皮肤系统，让皮肤界面可以自定义化）
8.  等等

不过这些功能是否最后都能完成，就不一定了（笑哭），还是得看有没有时间写。

## 小结

PicGo 的 v2.2.0 版本是个不痛不痒的更新，主要是多了快捷键系统。但是随之而来的是能够提供给你更好的图片上传 + 获取链接的体验，更新一下也无妨。

下载链接：

[https://github.com/Molunerfinn/PicGo/releases](https://github.com/Molunerfinn/PicGo/releases)

Mac 用户请下载 dmg 格式文件，Windows 用户请下载 exe 格式文件，Linux 用户请下载 AppImage 格式文件。鉴于 GitHub 的 release 下载速度过慢的问题，欢迎提供国内 CDN 的朋友！

## 彩蛋

Typora 最近的 Organization 里增加了 [PicGo-cli](https://github.com/typora/PicGo-cli) 的仓库，PicGo 的底层框架 PicGo-Core 还收到了来自 Typora 团队的 [PR](https://github.com/PicGo/PicGo-Core/pull/28)，是不是意味着未来某个版本 Typora 可能支持通过 PicGo 快捷上传图片呢？让我们拭目以待。

## 相关文章

[图床「神器」PicGo v2.0 更新，插件系统终于来了](https://sspai.com/post/52527)  

[图床上传工具 PicGo v1.5 更新：支持腾讯云 COSv5 版本、支持 GitHub 图床、支持上传前重命名文件等等](https://sspai.com/post/44495)  

[PicGo：基于 Electron 的图片上传工具](https://sspai.com/post/42310)