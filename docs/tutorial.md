# Claude Fable 5.2 tutorial: from prompt to video

English · [简体中文](zh-CN/tutorial.md) · [← Back to the collection](../README.md)

From a prompt to an MP4 in four steps. Fable 5.2 writes a web page; you play it and record it.

## 1. Start from a video you like

Open any title in the [collection](../README.md) to reach its page on [SandBase Lab][lab]: the
video, the original post and, when the creator shared one, the prompt. Press **Recreate**. Lab
opens the text arena with the post loaded and Claude Fable 5.2 selected. Sign in, run it, and
you get the HTML back, with a live preview.

No prompt shared? Write one with the [prompt guide](prompt-guide.md). It has a fill-in
template.

## 2. Compare models on the same prompt

In the [text arena][arena], add one or two more models next to Fable 5.2 (for example
`anthropic/claude-opus-5.5`, `anthropic/claude-fable-5.1`, `google/gemini-4-argon` or
`openai/gpt-6-astra`) and run once. Every model gets the same words, and each result
shows its cost and time. That is how most of the head-to-heads in this collection were made:
the same prompt, the same assets, two results side by side. It is also the quickest way to
check a claim from the [comparison page](model-comparison.md) on your own task.

## 3. Or call the API

Claude Fable 5.2 is `anthropic/claude-fable-5.2` on SandBase, OpenAI-compatible.

1. Create a key in the [console][keys] and export it: `export SANDBASE_API_KEY=sk-sb-...`
2. Save your prompt as `prompt.txt`.
3. Run:

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

- `max_tokens: 128000`: that is the model's output ceiling, and hidden reasoning tokens
  come out of the same budget. Ask for the whole budget on long pages; a tight limit gives
  you a truncated page and still bills the reasoning.
- `--max-time 900`: one long page can take minutes. Creators report 10 minutes for a
  cathedral-scale Three.js scene, 40 minutes for a one-file neon city, 71–108 minutes for
  procedural Blender builds and up to 3 hours at `max` effort for the largest films.
- `sed '/^```/d'` removes Markdown fences if the model added them.
- `usage` shows the tokens you were billed for, including
  `completion_tokens_details.reasoning_tokens`. Input is $8 per million tokens and output
  $40 per million; prices are on the [model page][model].
- Optional: `reasoning_effort` trades thinking for speed and cost. Creators who wanted a
  showreel ran at `max`; for a quick draft, start at `medium` and only raise it when the
  composition is right — launch-week posts report Fable one-shotting at medium what Opus
  5.5 needed max for.

Open `fable.html` in a browser. If it is blank, open the developer console: the usual
causes are a truncated file (raise the limit) or a CDN that did not load (ask for everything
inline).

### With the SandBase CLI

The same call through the [SandBase CLI](https://www.npmjs.com/package/@sandbaseai/cli),
which reads `SANDBASE_API_KEY` as well:

```bash
npx -y @sandbaseai/cli@latest inspect anthropic/claude-fable-5.2   # input fields and price, free
jq -n --rawfile prompt prompt.txt '{max_tokens: 128000, messages: [{role: "user", content: $prompt}]}' > input.json
npx -y @sandbaseai/cli@latest run sandbase_anthropic_claude_fable_5_2 -f input.json --timeout 900 -o result.json
```

`-o result.json` saves the response; the page is in the assistant message, as with the API.

## 4. Turn the page into a video

Most creators screen-record the page. To get the same clip every time, record it headlessly
with [`scripts/record.mjs`](../scripts/record.mjs):

```bash
npm i -D playwright@1.56.1
npx playwright install chromium          # or use your installed Chrome: export RECORD_CHANNEL=chrome
node scripts/record.mjs fable.html fable.mp4 12 1920 1080   # 12 seconds at 1080p
```

It opens the page at the size you give, records for that many seconds, and converts to H.264
MP4 with ffmpeg. For a clean result, ask in the prompt for an autoplay camera tour or a
fixed-length loop (see [prompt guide §7](prompt-guide.md#7-have-it-check-its-own-work)),
so nothing depends on a mouse.

Want sound? The recording is picture only, so add audio in the edit. Some creators mixed a
royalty-free track into the page itself so the recording carries it; if you record a page
with audio, capture the tab audio, not the microphone.

Many launch-week videos came out of a harness rather than a single API call: Claude Code
driving Blender for procedural 3D ([@Stefan_3D_AI][stefan]), a project-manager chat that
briefs a fresh Fable chat for a documentary ([@naometzger][doc]), and plain "one prompt,
one HTML file" for the motion-design showreels ([@MatinSenPai][matin]).

## Run generated code safely

The HTML is code you haven't read. Opening it from disk is usually fine for a single-file
page, but it can still load scripts and make network requests. For anything you don't
trust, or to run many pages automatically, use a [SandBase Sandbox][sandbox]: an isolated
environment with a time limit and no access to your files or keys.

[lab]: https://www.sandbase.ai/lab/ai-videos/fable-5-2?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[arena]: https://www.sandbase.ai/arena/text?models=anthropic%2Fclaude-fable-5.2&utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[keys]: https://www.sandbase.ai/console/keys
[model]: https://www.sandbase.ai/model/anthropic/claude-fable-5.2?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[sandbox]: https://www.sandbase.ai/landing/sandbox?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[stefan]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120039417981333599?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[doc]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120269096574939254?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
[matin]: https://www.sandbase.ai/lab/ai-videos/fable-5-2/2120210882382971263?utm_source=github&utm_medium=docs&utm_campaign=awesome-fable-5-2
