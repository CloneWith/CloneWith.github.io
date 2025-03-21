---
date:
  created: 2025-03-21
tags:
  - thoughts
  - fiction
  - coding
categories:
  - misc
---

# 来自错觉

本文的主体是一批虚构人物的日记，他名为 **Moetori**，正在参与一个社区项目的开发，他很喜欢做这件事。可能有其他的信息，但是目前无关紧要，会在后续补充。<!-- more -->

所有的日期以他参与项目开发的第一天开始计算，只记录相对日期。大概与真实情况的时间是对不上的，这方面还请谅解。

参考资料：[包有的](https://github.com/ppy/osu/pull/30357)

## 日记正文

### 第 60 天·午间

啊啊啊，好久不见了。

今天在程序里随便点来点去的时候，突然就来想法了！长话短说，得赶快记下来...

那个模组预设菜单，看着好不顺眼啊。一个单纯的模组显示，只有一个按钮可以把它改成现在用户选中的模组，总觉得逻辑上怪怪的。加个删除按钮多少得好点吧？

不错的主意，我这就开干！

### 第 60 天·晚

欸，原来显示模组的列表项和预设没有关联关系吗？当时没想到这点呢...不然的话工具提示的模组列表上也会显示删除按钮了。

不过也好办吧，在构造函数里传个可 null 的集合参数，非 null 的话就说明是编辑器的一部分了，点击之后，让它隐藏起来然后消掉就可以了。

*一会儿后...*

看起来果然不错呢。开个 PR 看看效果好了。

### 第 61 天·午后

很多人 React 了，反响还挺好的，看来这是他们都想要的功能；不过一个叫 Bdach 的协作者发话了...

> Before we go too far into bikeshedding here I kind of don't get why this feature exists.

不是哥们，你是给大伙泼冷水呢？我寻思也没哪地方做错啊，也许有吗？看看问题：

> Is remaking / editing a preset really such an issue that this is required to exist? The "Use current mods" button exists, what's the point?
>
> Why is *removing* mods made explicitly easier? Adding mods to a preset is still as cumbersome as it presumably was before. Why distinguish removal? Why introduce such asymmetry between the two operations?

额...看来是有点问题，在理解上？也许我该阐述一下观点。

- 现在的版本来看，编辑预设确实是成问题的。既然社区反应都是这样，那我想我一定是在做正确的事情，更何况只是在做必要的小改动。
- 操作不平衡的问题，并不是我引入的（因为一开始就是这样不是吗），只是呈现，**呈现**了一下而已！毕竟删东西一定是最顺手的嘛。
- 当然如果要让它们平衡一点，也不是不可以...不过要多做点功课了。

感觉这样应该差不多了...看看他怎么说。

### 第 61 天·傍晚

> You still haven't told me why the current methods of doing this (either remaking the preset, or clicking "Use current mods") are insufficient or inadequate. I'd like the answer to that before considering this feature on merit.

啊啊啊，有点烦啊。是我的问题吗？让我再想想有什么能补充的，打开界面动一下看看：

- 嗯...我该告诉他为什么我要改界面。
- 首先这个弹出框的设计就挺反人类的吧...要改预设模组就得从大列表中选，但是你这个对话框又把它挡住了，这不起冲突了嘛？
- 整个模组列表向右滑的时候，这个框就卡在那儿了，也很奇怪啊。
- 这样的话就没法从头开始建一个预设了（必须先选中一些才行），所以不太好。

是的，迄今为止我找不到一个理由不改它，但是该改的利用我找到了这么多。所以没问题。嗯！

> I dunno this feels fixing an issue nobody should have.

哎，真对不上路子吧。不过他请来项目主了，接下来就等他意见了...希望他能同意吧。

---

> I don't see any harm in having it if the complexity overhead is minimal, but also not sure it's required.
>
> Additionally, I see less value in adding a "remove" button if there's not also an "add" button.

哈哈，看来还有希望；没有添加按钮的话、删除按钮就没啥意义吗？那我加个不就好了？这么一看，还是大工程啊，准备好开工了！

### 第 68 天

不对，要做个添加按钮的话，它该做什么呢？再开个弹出框？那很糟糕了；不如说从一开始就把对话框分成两栏，左边显示已经加入的，右边显示没加入的，这样添加按钮显示在右边就好了。

这样的话，我们肯定还会想在右边（两边）加个自定义部分，实现和自定义菜单相同的功能，这不就省劲了嘛！

但是调试起这东西是真费劲吧，要么是列表里删了预设没删，要么是项目对不上报错了，真是错误百出呢。不过好事多磨，这个功能做出来一定够好用的！

### 第 70 天·早

好，好，好...噫，我成啦！在调试了 114 个小时、重写了 514 行代码后，这些点都修复停当了！推上去试试看吧，给他们一点小小的双面板震撼~

### 第 70 天·傍晚

> I'm sorry but... my feedback is mostly 'just no'. This is literally duplicating the entire mod select content inside the popover. You can't do that.
>
> Is editing a popover using one of the flows described above really such an issue?

不行吗...有点 emo 了。这么有前途的发展方向，怎么会出问题呢？既然你这么说，那就没办法了。

不过我现在也释怀了，毕竟谁没犯错的时候呢，就跟我突然起兴写了这么多代码一样...

> Thanks for trying this out regardless. Sometimes we need to try and realise it doesn't work 😅

## 回首之日

!!! warning "友情提示"
    本文接下来的部分可能包含有攻击性的内容，或者并不适合所有人阅读。如果您没做好心理准备，请现在离开；如果您感觉被冒犯了或生理不适，Moetori 在此深表遗憾。

你改悔罢，活爹！

你还真有胆量跟核心开发者交锋啊？看这个 PR 我都能替你抠个三室一厅出来了。

想要加个删除按钮，然后呢？就这么开干了？？？真怀疑你有没有认真阅读过项目贡献指南，有没有考虑过你这个想法有多危险。白纸黑字搁那呢，怕你困了读不到那边，给你端上来了咧，少爷！

> In the case of simple issues, a direct PR is okay. However, if you decide to work on an existing issue which doesn't seem trivial, **please ask us first**. This way we can try to estimate if it is a good fit for you and provide the correct direction on how to address it. In addition, note that while we do not rule out external contributors from working on roadmapped issues, we will generally prefer to handle them ourselves unless they're not very time sensitive.

那我问你，你觉得这问题算简单问题吗，认真考虑过了吗？你说你考虑过了，那我问你，为什么人家问你为什么这么改的时候，你怎么脑筋又转不过弯来了？

到这也就算了，你还嘴硬，把人家模组面板结构刨了一遍，八竿子打不着的几个问题就硬扯来扯去。搁这扯面皮呢？你吃吗？有着牙口还不如去刨土，帮忙疏松土地去。

然后等到人家host发话了，你又觉得有希望了？痴心妄想！动动脑子，这希望是你这 PR 的希望吗？答案很明确了吧！英语都读不懂吗？重点在 `not sure`，不确定！不确定哪来的希望？我看倒是绝望呢，`hope of DEAD END`！

再往下看，您还想着给人家做左右面板、做自定义、做增删查改哪？AUV 您吉祥嘞！说好只做个删除按钮呢，现在做到这么多？不觉得累啊？真该这样的话，那您真是天生抖 NM，当牛马潜质！写代码的，自己不想想吗？人家话摆着了就让你自己放弃的，还钻牛角尖扣字眼呢，把项目开发当文字游戏咧！

到你把双面板写出来了，人家明摆着说不行了，你又不高兴了。还问“怎么会出问题呢”？就看是不是你问题吧！host说试试才知道不行，都在替你可惜呢！自己写这么多代码，开 PR，狡辩，关 PR，满意了吧？

少爷，一下气急说了这么多话，可别生气嗷。你知道的，我一向都是对你好，让你少走弯路，能多省点时间做其他喜欢的事情不好嘛？等着你好好学习、好好发挥，写点高质量的代码，为社区切身做点实事吧，加油！
