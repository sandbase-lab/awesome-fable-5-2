# Claude Fable 5.2 教程：从提示词到视频

[English](../tutorial.md) · 简体中文 · [← 返回合集](../../README.zh-CN.md)

四步从提示词到 MP4：Fable 5.2 写出一个网页，你播放并录屏。

## 1. 从一条喜欢的视频开始

打开[合集](../README.zh-CN.md)里的任意标题，进入它的 [SandBase Lab][lab] 页面：
视频、原帖，以及作者公开时的提示词。点 **复刻**——Lab 会打开文本竞技场、载入帖子
内容并选中 Claude Fable 5.2。登录后运行，就能拿回 HTML 和实时预览。

没有公开提示词？用 [提示词写法](prompt-guide.md) 自己写一条，里面有填空模板。

## 2. 同一提示词对比模型

在[文本竞技场][arena]里，在 Fable 5.2 旁再加一两个模型（例如
`anthropic/claude-opus-5.5`、`anthropic/claude-fable-5.1`、`google/gemini-4-argon`
或 `openai/gpt-6-astra`），一次运行。每个模型拿到同样的文字，各自的花费与耗时
会并排显示。本合集里大多数对比就是这么来的：同一提示词、同一素材、两个结果。
这也是验证[对比页](model-comparison.md)某个说法最快的方法。

## 3. 或者直接调 API

Claude Fable 5.2 在 SandBase 上是 `anthropic/claude-fable-5.2`，兼容 OpenAI。

1. 在[控制台][keys]创建 Key 并导出：`export SANDBASE_API_KEY=sk-sb-...`
2. 把提示词存为 `prompt.txt`。
3. 运行：

```bash
jq -n --rawfile prompt prompt.txt '{
  model: "anthropic/claude-fable-5.2",
  max_tokens: 128000,
  messages: [{role: "user", content: $prompt}]
}' |
curl -sS --max-time 900 https://api.sandbase.ai/v1/chat/completions \
  -H "Authorization: Bearer $SANDBASE_API_KEY" \
  -H "Content-Type: application/json" \
  -d @- > response.json

jq -r '.choices[0].message.content' response.json | sed '/^```/d' > fable.html
jq '.usage' response.json
```

- `max_tokens: 128000`：这是模型的输出上限，隐藏推理 token 也占用同一额度。
  长页面请给满预算；额度太小会得到截断的页面，推理 token 照样计费。
- `--max-time 900`：一个长页面可能要几分钟。创作者报告过教堂级 Three.js 场景 10
  分钟、单文件霓虹城市 40 分钟、程序化 Blender 构建 71–108 分钟，以及 `max` 强度下
  最大的片子约 3 小时。
- `sed '/^```/d'` 去掉模型可能加上的 Markdown 代码围栏。
- `usage` 显示实际计费的 token，包括 `completion_tokens_details.reasoning_tokens`。
  输入每百万 token $8、输出每百万 $40；价格见[模型页][model]。
- 可选：`reasoning_effort` 用思考换速度和成本。想要作品集效果的用 `max`；打草稿
  先 `medium`，构图对了再上调——发布周的帖子报告，Opus 5.5 要 `max` 才一次成功的
  东西，Fable 在 `medium` 就能一次过。

用浏览器打开 `fable.html`。如果是空白页，打开开发者控制台：常见原因是文件被截断
（调大额度）或 CDN 没加载（让它全部内联）。

### 用 SandBase CLI

同样的调用也可以用 [SandBase CLI](https://www.npmjs.com/package/@sandbaseai/cli)
（同样读 `SANDBASE_API_KEY`）：

```bash
npx -y @sandbaseai/cli@latest inspect anthropic/claude-fable-5.2   # 输入字段和价格，免费
jq -n --rawfile prompt prompt.txt '{max_tokens: 128000, messages: [{role: "user", content: $prompt}]}' > input.json
npx -y @sandbaseai/cli@latest run sandbase_anthropic_claude_fable_5_2 -f input.json --timeout 900 -o result.json
```

`-o result.json` 保存响应；页面在 assistant 消息里，和 API 一致。

## 4. 把网页录成视频

多数作者直接录屏。要每次得到同样的片段，用 [`scripts/record.mjs`](../scripts/record.mjs)
无头录制：

```bash
npm i -D playwright@1.56.1
npx playwright install chromium          # 或用本机 Chrome：export RECORD_CHANNEL=chrome
node scripts/record.mjs fable.html fable.mp4 12 1920 1080   # 1080p 录 12 秒
```

它按你给的大小打开页面，录相应秒数，再用 ffmpeg 转成 H.264 MP4。要干净结果，在
提示词里要求自动运镜或固定时长循环（见[提示词写法第 7 条](prompt-guide.md#7-让它自查)），
这样不依赖鼠标。

想要声音？录制只含画面，声音在剪辑里加。也有作者把免版税音轨混进页面本身，录屏
自然带上；如果录制带音页面，采集的是标签页音频，不是麦克风。

发布周的很多片子出自 harness 而不是单次 API 调用：Claude Code 驱动 Blender 做程序化
3D（[@Stefan_3D_AI][stefan]），项目经理对话先把思路整理成简报再交给新的 Fable 对话
拍纪录片（[@naometzger][doc]），以及纯粹的"一个提示词一个 HTML"动效作品集
（[@MatinSenPai][matin]）。

## 安全运行生成的代码

HTML 是你没读过的代码。单文件页面从磁盘打开通常没问题，但它仍可能加载脚本、发起
网络请求。不信任的内容，或需要批量自动运行时，用 [SandBase Sandbox][sandbox]：
有运行时限、无法接触你的文件和 Key 的隔离环境。

[lab]: https://www.sandbase.ai/lab/ai-videos/fable-5-2?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[arena]: https://www.sandbase.ai/arena/text?models=anthropic%2Fclaude-fable-5.2&utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[keys]: https://www.sandbase.ai/console/keys
[model]: https://www.sandbase.ai/model/anthropic/claude-fable-5.2?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[sandbox]: https://www.sandbase.ai/landing/sandbox?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[stefan]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120039417981333599?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[doc]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120269096574939254?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[matin]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120210882382971263?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
