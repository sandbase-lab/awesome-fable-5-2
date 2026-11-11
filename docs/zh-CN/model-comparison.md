# Claude Fable 5.2 对比 Claude Opus 5.5、GPT-6 Astra 和 Gemini 4 Argon

[English](../model-comparison.md) · 简体中文 · [← 返回合集](../../README.zh-CN.md)

两类证据分开摆：

1. **我们实测的。** Lab [Evals 榜单][evals] 是 Artificial Analysis 数据，[Pelican
   Test][pelican] 对每个模型跑同一个固定提示词并打分。样本不大，但条件一致。
2. **创作者报告的。** X 上带各自提示词、成本和耗时的对比帖。有用的上下文，
   未经我们核实。

Fable 5.2 于 2026-11-09 发布，这份合集在两天后上线——实测一侧还来不及填上：
任何一张 Evals 榜都没有 Fable 5.2 这一行，Pelican Test 同样没有。所以本页
如实倚重创作者一侧。

## 我们实测的：如实说，还没有

Artificial Analysis 2026-11-09 快照：Fable 5.2 缺席所有榜单——指数、编码、
agentic、速度、成本榜在发布两天后都还没有它的行。同一快照上最接近的参考点：

| 模型（榜上行名） | [智能指数][b-intel] | [输出速度][b-speed] | [单任务成本][b-cost] |
|---|---|---|---|
| Gemini 4 Carbon (High) | 60.0（110 个模型第 1） | 未列出 | 未列出 |
| Claude Opus 5.5 (Max) | 59.1（第 2） | 中游 | 高位 |
| Claude Fable 5.1 (Max) | 49.2（第 20） | 约 68 tok/s 档 | 约 $7.63 档 |
| DeepSeek V4.1 Flash (Max) | 约 39.5 档 | 约 231 tok/s 档 | 约 $0.49 档 |

Pelican Test 榜单上同样没有 Fable 5.2——合集上线时还没有对这只模型跑过固定的
鹈鹕提示词。等快照和榜单补上之后，这一节就是实测半边。在此之前，下面全部是
创作者报告。

## 创作者报告的

发布头两天 X 上的同提示词对比。数字以作者自述为准：工具不同（Claude Code、
Blender、单次 API）、推理强度不同、往往只有一次运行。点开链接可以看两边的结果。
发布周几乎每场对比的对手都是 Opus 5.5；GPT-6 Astra 和 Gemini 4 Argon 出现在少数几场。

| 创作者 | 任务 | Claude Fable 5.2 | 对手 | 作者结论 |
|---|---|---|---|---|
| [@EnvolDev][ice] | 冰教堂，同提示词 | $81.10，1 小时 57 分 | Opus 5.5：$45.97，3 小时 12 分 | "巨大飞跃"——更贵，但快 1 小时 15 分且明显更好 |
| [@Stefan_3D_AI][castle] | Blender 程序化城堡，复跑 | 71 分，38 万输出，约 $32.9 | Opus 5.5：55 分，32.4 万，约 $19.1 | 细节"明显可见"提升；单次更贵 |
| [@Bhavani_00007][rocket] | 火箭发射场景 | $23.45，32 分 | Opus 5.5：$10.35，24 分 | "细节和写实度惊人"；但希望价格更好 |
| [@0xKense1][rig] | Blender 游戏角色绑骨 | 约 $61，36 分 | Opus 5.5：约 $28，21 分，片段更多 | 更贵更慢——Opus 产出的片段更多 |
| [@JamesMalsawm][turgle] | 飞行 Turgle 岛（medium） | $79.10，1 小时 43 分 | Opus 5.5：$43.97，3 小时 15 分 | 明显飞跃；快约 1.5 小时 |
| [@mattshumer_][motion] | 一次生成动效视频 | — | Opus 5.5 | "让 Opus 看起来像玩具" |
| [@petergostev][games] | 可玩游戏 | — | Opus 5.5 | "游戏能力强太多"——机制胜过外观 |
| [@marcthecreatorr][pelicanx] | 四季鹈鹕骑行 SVG | 约 $25，约 25 分 | Gemini 4 Hydrogen：约 5 分，费用不详 | Hydrogen"表现得出乎意料地好" |
| [@0xbobaaa][vicecity] | 单文件霓虹罪恶都市 | 40 分，24.8 万输出，约 $13.8 | Fable 5.1：27 分，11.2 万，约 $10.7 | 5.2 细节更好；5.1 仍更便宜更快 |
| [@Bhavani_00007][carbon] | 同一火箭场景，四模型 | — | Gemini 4 Carbon High | Carbon"接近 Opus 水平且更高效" |
| [@pleometric][bryce] | 3D 视频，Bryce 引擎 | — | Opus 5.5 | "规划/执行比 Opus 更快，错误更少" |
| [@DanielZambrini][stickman] | 火柴人格斗动画 | $40.36 | Opus 5.5：$18.88 | 更贵，但压力下还快一分钟 |

单跑与质量笔记：

- [@imantiai][fps] 让 Fable 5.2 以 `max` 无人值守跑了九小时——27 个子代理、
  1.79 亿 token——得到一个每帧约 3000 万多边形的 WebGPU 第一人称射击游戏。
- [@notjazii][pirate] 一次生成了约 $34.4 的 3D 海盗船："Opus 做不到的东西，
  Fable 在 medium 或 high 推理下就直接一次过。"
- [@Stefan_3D_AI][serpent] 用 108 分钟、约 103 万输出 token（约 $89.7）构建了
  海蛇 Blender 场景；同一需求在 Opus 5.5 上约 $25.2。
- [@d0xxed][hero] 报告了一次早期访问的 12 小时单提示词英雄射击构建。
- [@wangray][wangray] 用一句中文拿到了一条发布视频——风格迁移跨语言成立。
- [@aug5thmusic][fugue] 让它用 LilyPond 写了一首巴赫风格的管风琴赋格：
  "不比 Opus 5.5 好，但不错。"

头两天的整体图景：在**细节、动效和游戏机制**上创作者一致把 Fable 5.2 排在
Opus 5.5 前面——好几个人用的是"飞跃"而不是"提升"。反方筹码是**成本**：按
每百万 token $8/$40 的标价（对比 Opus 5.5 的标价和更便宜的对手），同一场景
在 Fable 上普遍多计 1.5–4 倍，多位创作者明确希望价格更接近 Fable 5.1。
没人说它便宜；争论点是这些细节值不值。

## 信了之前先复跑

结果随配置走：推理强度（一条帖子里仅 `medium` 对 `max` 就把账单改了一半）、
harness、模型是否拿到同样素材、对手是否看到同一提示词。这里创作者一侧是
每帖一次运行、只覆盖发布周。自己跑一遍：把提示词贴进 [Lab 文本竞技场][arena]，
选两三个模型对比，或看[教程](tutorial.md)。

## 更多实测

- [Lab Evals 榜单][evals] — Artificial Analysis 数据，2026-11-09 快照。
  下次快照落地后搜 "Fable 5.2"；今天还没有。
- [Lab Pelican Test][pelican] — 每个模型同一提示词、同一评分；尚无 Fable 5.2。
- [SandBase Lab 全部 AI 视频合集][collections] — 其他模型的同类清单，包括
  [Claude Opus 5.5][opus-repo] 和 [Gemini 4 Argon][gemini-repo]。

---

Lab 数据：[Evals 榜单][evals]（Artificial Analysis，2026-11-09 快照——无
Fable 5.2 行）。创作者数据：各自原帖链接；未经独立核实。

[evals]: https://www.sandbase.ai/leaderboards?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[b-intel]: https://www.sandbase.ai/leaderboards/llm-intelligence?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[b-speed]: https://www.sandbase.ai/leaderboards/llm-speed?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[b-cost]: https://www.sandbase.ai/leaderboards/llm-cost?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[pelican]: https://www.sandbase.ai/arena/pelican-test?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[arena]: https://www.sandbase.ai/arena/text?models=anthropic%2Fclaude-fable-5.2&utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[collections]: https://www.sandbase.ai/lab/ai-videos?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[opus-repo]: https://github.com/sandbase-lab/awesome-opus-5.5
[gemini-repo]: https://github.com/sandbase-lab/awesome-gemini4-argon
[ice]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119907318729245180?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[castle]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120041169719894165?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[rocket]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119902204320780676?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[rig]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119916096098582566?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[turgle]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120162060869025848?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[motion]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119884041331892403?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[games]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119884264019779900?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[pelicanx]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120151349924938083?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[vicecity]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120130913711353937?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[carbon]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120204803771183140?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[bryce]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119901747930186234?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[stickman]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119893834276507954?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[fps]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119979537320534135?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[pirate]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119905661505122575?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[serpent]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120039417981333599?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[hero]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119898886215205358?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[wangray]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120040640423850168?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[fugue]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2119907891419480107?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
