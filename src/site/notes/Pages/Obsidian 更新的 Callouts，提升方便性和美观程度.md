---
{"dg-publish":true,"dg-permalink":"/pages/cc-2022-09-26-215713/","permalink":"/pages/cc-2022-09-26-215713/","dgHomeLink":true,"dgPassFrontmatter":false}
---

# Obsidian 更新的 Callouts，提升方便性和美观程度

> [!quote] 本文剪藏自[Obsidian更新的Callouts，提升方便性和美观程度 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/494647464)

在 Obsidian 最新更新的 14.0 版本中，终于上线了 “Callout” 功能。

使用这样的符号就可以启用 callout 模块: `> [!INFO]`.

```
> [!INFO]
> 这里是callout模块
> 支持**markdown** 和 [[Internal link|wikilinks]].

```

呈现出来是这样的

![](https://pic3.zhimg.com/v2-86ef1d3141e0b3bc915e2aad7a621162_r.jpg)

## 样式

默认有 12 种风格。每一种有不同的颜色和图标。

只要把上面例子里的 `INFO` 替换为下面任意一个就行。

*   note
*   abstract, summary, tldr
*   info, todo
*   tip, hint, important
*   success, check, done
*   question, help, faq
*   warning, caution, attention
*   failure, fail, missing
*   danger, error
*   bug
*   example
*   quote, cite

## 标题和内容

可以自定义标题，然后直接不要主体部分，比如

```
> [!TIP] Callouts can have custom titles, which also supports **markdown**!

```

![](https://pic3.zhimg.com/v2-ff3e8ccd97a28fe54982b7c303de90f6_r.jpg)

## 折叠

可以使用 `+` 默认展开或者 `-` 默认折叠正文部分。

```
> [!FAQ]- Are callouts foldable?
> Yes! In a foldable callout, the contents are hidden until it is expanded.

```

显示为:

![](https://pic1.zhimg.com/v2-9a1c6964e3badb6b52fae96e630515cc_r.jpg)

## 如果需要自定义

Callout 的类型和图标是用 CSS 来描述，颜色是`r, g, b` 三色组，图标有相应的 icon ID (比如`lucide-info`)。也可以自定义 SVG 图标。

```
.callout[data-callout="my-callout-type"] {
    --callout-color: 0, 0, 0;
    --callout-icon: icon-id;
    --callout-icon: '<svg>...custom svg...</svg>';
}

```

参考自英文文档：[Use callouts](https://link.zhihu.com/?target=https%3A//help.obsidian.md/How%2Bto/Use%2Bcallouts)