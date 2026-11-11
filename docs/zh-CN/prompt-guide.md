# Claude Fable 5.2 提示词写法：七条来自真实作品的模式

[English](../prompt-guide.md) · 简体中文 · [← 返回合集](../../README.zh-CN.md)

下面每一条都来自本合集里作者公开的提示词，并链接到对应帖子。它们不是模型强制的规则，
而是发布周里"想要一个页面或一支片子、并且真的拿到了"的写法。

一句话版本：**说清交付物和渲染器、给一个创作标尺、交一个没法糊弄的任务、编排运动、
写出物理约束、选好推理强度、并让它自查。**

## 1. 第一句就写清交付物和渲染器

这个合集里被复用最多的提示词没有任何画面描述：

> "make a dynamic 15-second motion graphics video that shows what an incredible motion
> designer you are, like it's your showreel for a résumé. go all out."
> — [@MatinSenPai][matin]

在语言模型那里，"视频"其实是"一个能渲染出视频的网页"——你不写，模型就自己选渲染器、
时长和画幅。直接写出来：单个 HTML 文件、1920×1080、15 秒、Canvas/SVG/Three.js。
如果要的是构建而非渲染，也可以直接点名工具：

> "Can you write the most intricate photorealistic simulation of honey in WebGL in the
> browser"
> — [@deedydas][honey]

## 2. 给一个创作标尺，而不是一份规格表

"go all out" 和 "showreel for a résumé" 在做实事——它们让模型展示品味，而不是打勾。
发布周里互动量最高的作品都带着标尺："AAA quality"、"the most beautiful video you can"、
或一个明确风格：

> "make me the most beautiful video you can"
> — [@aollivier82][aollivier]

> "build a hyper-realistic first person shooter set on a tropical island, AAA quality
> visuals and sound effects, make no mistakes"
> — [@imantiai][fps]

标尺一句话就够："像苹果发布会"、"AAA 级画质"、"做出你能做的最美视频"——写在交付物旁边。

## 3. 交一个没法糊弄的任务

写实向的提示词之所以有效，是因为它们点名的产出只有"做对"才能成立：真实的物理、真实的
几何、真实的机制。"每帧渲染 3000 万多边形的超写实射击游戏"，或"浏览器里最精细的蜂蜜
物理仿真"，都堵死了"一张静态图加个播放键"的退路：

> "I gave Fable 5.2 (max) a single prompt … and let it run unattended. Everything
> procedural in raw WebGPU, no engine."
> — [@imantiai][fps]

目标是仿真、游戏或可交互场景时，要写视频必须演示的机制——物理、车流、可玩循环——
而不只是外观。

## 4. 编排运动，一节拍一节拍

描述"运动"而不是"物件"的帖子得到的是影片，不是幻灯片。反复出现的发布片提示词会写
状态如何过渡——一个形状、一次推镜——而不是罗列场景：

> "参考这个 launch video 风格给 BlewUp 做一个类似的视频"
> — [@wangray][wangray]

> "create an svg of a pelican riding a bicycle across five animated seasons"
> — [@marcthecreatorr][pelican]

写清过渡、季节切换、带动视线的东西——模型会补中间帧。只给场景列表，得到的就是跳切。

## 5. 把物理约束明写出来

程序化 3D 和动画的提示词，约束本身就是内容。最强的例子明确写出不允许发生的事——
穿插、穿透、骨骼数、帧预算：

> "generate a sea serpent and animate it in Blender, 20 seconds of coiling around a ship
> without ever passing through the hull."
> — [@Stefan_3D_AI][serpent]

> "make it check its own work with numbers. grip within 1 cm of the palm, exactly 2 eyes…"
> — [@0xKense1][rig]

一句否定式不变量（"never passing through the hull"、"one continuous take, no cuts"）
只要一句话，就能防住最常见的失败——模型在时限前中途停住、留下一帧破画面。

## 6. 选好推理强度——并写出来

发布周创作者对 `reasoning_effort` 喊得很响：同一个提示词在 `medium` 和 `max` 下是
两支片子，画质、时长和账单都不同。把你要的强度写出来，帖子里也标上，对比才成立：

> "Run on medium by the way" — [@JamesMalsawm][james]
> "Via Claude Code + Blender on Max effort." — [@Stefan_3D_AI][serpent]
> "(Extra High effort)" — [@aug5thmusic][fugue]

打草稿先用 `medium`，构图对了再上调；多位创作者报告，Opus 要 `max` 才一次成功的东西，
Fable 在 `medium` 就能一次过。

## 7. 让它自查

最长的构建里反复出现两种模式：模型自己打开并修复页面，或被交给一个检查循环。一位
纪录片作者最大的突破是让模型*逐帧研究*参考素材再动手：

> "make your ai study your references one large frame every quarter second, not skim
> them."
> — [@naometzger][doc]

> "use a project manager chat. one chat turns your thoughts into a brief, then hands the
> whole job to a fresh fable chat … it changes only what's on the list"
> — [@naometzger][doc]

自查配一条录制路径——固定时长的循环或自动运镜——这样不依赖鼠标。
[教程](tutorial.md) 用 [`scripts/record.mjs`](../scripts/record.mjs) 录屏。

## 填空模板

```text
单个自包含 HTML 文件，1920x1080，{秒数} 秒，{渲染器}，不用外部素材。

目标：{一句话——观众应该感受到或理解什么}。
创作标尺：{像苹果发布会 / AAA 画质 / 你的作品集——全力以赴}。
任务：{必须真正成立的机制——物理、车流、可玩循环}。

节拍：开场 {首帧}；然后 {过渡 1 -> 2 -> 3}；收尾 {与首帧呼应的末帧}。
不变量：{始终不变的东西——一镜到底、不跳切、绝不穿过 X}。
强度：reasoning_effort={medium|high|xhigh|max}。

结束前：打开页面、修掉控制台错误，并让动画可以干净循环 {秒数} 秒用于录屏。
```

## 出处

- [@MatinSenPai][matin] — 被反复复用的十五秒作品集提示词。
- [@deedydas][honey] — 一句话的 WebGL 蜂蜜写实仿真。
- [@aollivier82][aollivier] — "你能做的最美视频"。
- [@imantiai][fps] — 九小时无人值守的 WebGPU FPS 构建及其遥测。
- [@wangray][wangray] — 一句话的发布视频风格迁移。
- [@marcthecreatorr][pelican] — 四季鹈鹕骑行 SVG 测试。
- [@Stefan_3D_AI][serpent] — 海蛇 Blender 约束及其 token 账单。
- [@0xKense1][rig] — 让它用数字自查。
- [@JamesMalsawm][james] — medium 强度下同提示词 Fable 对 Opus。
- [@aug5thmusic][fugue] — 在提示词里写明 Extra High 强度。
- [@naometzger][doc] — 逐帧研究参考素材与项目经理对话。
- [@0xbobaaa][bob] — 单 HTML 文件、零素材、Fable 5.1 对 5.2 并排。

[matin]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120210882382971263?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[honey]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119930300990177509?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[aollivier]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119920990893244510?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[fps]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119979537320534135?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[wangray]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120040640423850168?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[pelican]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120151349924938083?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[serpent]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120039417981333599?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[rig]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119916096098582566?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[james]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120162060869025848?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[fugue]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119907891419480107?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[doc]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120269096574939254?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[bob]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120130913711353937?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
