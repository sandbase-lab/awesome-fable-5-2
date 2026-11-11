# Claude Fable 5.2 vs Claude Opus 5.5, GPT-6 Astra and Gemini 4 Argon

English · [简体中文](zh-CN/model-comparison.md) · [← Back to the collection](../README.md)

Two kinds of evidence, kept apart:

1. **What we measured.** The Lab [Evals boards][evals] show Artificial Analysis data, and
   the Lab [Pelican Test][pelican] runs the same fixed prompt on every model and scores the
   result. Small samples, but the same conditions for everyone.
2. **What creators reported.** Head-to-heads posted on X with their own prompts, costs and
   times. Useful context, not verified by us.

Fable 5.2 shipped on 2026-11-09 and this list ships two days later — the measured side has
not had time to fill in yet. There is no Fable 5.2 row on any Evals board, and no Pelican
Test result either, so this page leans on the creator side and says so plainly.

## What we measured: nothing yet, honestly

Artificial Analysis snapshot of 2026-11-09. Fable 5.2 is absent from every board — the
index, coding, agentic, speed and cost lists simply have no row for it two days after
release. The closest reference points on the same snapshot:

| Model (row on the board) | [Intelligence Index][b-intel] | [Output speed][b-speed] | [Cost per task][b-cost] |
|---|---|---|---|
| Gemini 4 Carbon (High) | 60.0 (#1 of 110) | not listed | not listed |
| Claude Opus 5.5 (Max) | 59.1 (#2) | mid-pack | high end |
| Claude Fable 5.1 (Max) | 49.2 (#20) | 68 tok/s class | $7.63 class |
| DeepSeek V4.1 Flash (Max) | 39.5 class | 231 tok/s class | $0.49 class |

The Pelican Test leaderboard has no Fable 5.2 row either — the collection went live before
any run of the fixed pelican prompt on this model. When the snapshot and the leaderboard
fill in, this section becomes the measured half. Until then, everything below is creator
reports.

## What creators reported

Same-prompt comparisons posted on X in the first two days. Numbers are as the creator
stated them: different tools (Claude Code, Blender, one-shot API), different reasoning
efforts, often one run. Click through to watch both results. Opus 5.5 is the rival in
almost every launch-week head-to-head; GPT-6 Astra and Gemini 4 Argon appear in a few.

| Creator | Task | Claude Fable 5.2 | Rival | Creator's verdict |
|---|---|---|---|---|
| [@EnvolDev][ice] | Ice cathedral, same prompt | $81.10, 1 h 57 m | Opus 5.5: $45.97, 3 h 12 m | "A huge leap" — costlier, but 1 h 15 m faster and visibly better |
| [@Stefan_3D_AI][castle] | Procedural castle in Blender, re-run | 71 min, 380k out, ~$32.9 | Opus 5.5: 55 min, 324k, ~$19.1 | "Really noticeable" detail jump; costlier per run |
| [@Bhavani_00007][rocket] | Rocket launch scene | $23.45, 32 min | Opus 5.5: $10.35, 24 min | "Detailing and realism are incredible"; wished for better pricing |
| [@0xKense1][rig] | Rigged game character in Blender | ~$61, 36 min | Opus 5.5: ~$28, 21 min, more clips | Costlier and slower — Opus produced more clips |
| [@JamesMalsawm][turgle] | Flying Turgle Island (medium) | $79.10, 1 h 43 m | Opus 5.5: $43.97, 3 h 15 m | Noticeable leap; about 1.5 h faster |
| [@mattshumer_][motion] | One-shot motion video | — | Opus 5.5 | "Makes Opus look like a toy" |
| [@petergostev][games] | Playable games | — | Opus 5.5 | "Gaming is A LOT better" — mechanics over looks |
| [@marcthecreatorr][pelicanx] | Animated pelican SVG, five seasons | ~$25, ~25 min | Gemini 4 Hydrogen: ~5 min, cost n/a | Hydrogen "held up surprisingly well" |
| [@0xbobaaa][vicecity] | Neon vice-city drive, one HTML file | 40 min, 248k out, ~$13.8 | Fable 5.1: 27 min, 112k, ~$10.7 | 5.2 wins on detail; 5.1 still cheaper and faster |
| [@Bhavani_00007][carbon] | Same rocket scene, four models | — | Gemini 4 Carbon High | Carbon "near Opus level, more efficient" |
| [@pleometric][bryce] | 3D video, Bryce engine | — | Opus 5.5 | "Planning/execution faster than opus, fewer errors" |
| [@DanielZambrini][stickman] | Stickman fight animation | $40.36 | Opus 5.5: $18.88 | Costlier, but a minute faster under load |

Solo runs and quality notes:

- [@imantiai][fps] let Fable 5.2 run unattended for nine hours at `max` — 179M tokens
  across 27 sub-agents — for a WebGPU first-person shooter rendering ~30M polygons a frame.
- [@notjazii][pirate] one-shotted a 3D pirate ship at ~$34.4: "stuff that opus couldn't
  do, fable is just one shotting at medium or high reasoning".
- [@Stefan_3D_AI][serpent] spent 108 minutes and ~1.03M output tokens (~$89.7) on a
  sea-serpent Blender build; the same brief on Opus 5.5 cost ~$25.2.
- [@d0xxed][hero] reported a 12-hour single-prompt hero-shooter build from early access.
- [@wangray][wangray] got a launch film from one line of Chinese — the style transfer
  works across languages.
- [@aug5thmusic][fugue] had it write a Bach-style organ fugue in LilyPond: "not better
  than Opus 5.5, but good".

The pattern across the first two days: on **detail, motion and game mechanics** creators
consistently put Fable 5.2 ahead of Opus 5.5 — several say "a leap", not an increment.
The counterweight is **cost**: at $8/$40 per million tokens (versus Opus 5.5's list price
and cheaper rivals), the same scene routinely bills 1.5–4x more on Fable, and several
creators explicitly wished the price were closer to Fable 5.1's. Nobody argues it is
cheap; the argument is whether the detail is worth it.

## Rerun before you trust a comparison

Results move with the setup: reasoning effort (`medium` vs `max` alone changed bills by
half in one post), harness, whether the model got the same assets, and whether the rival
saw the same prompt. The creator side here is one run per post, launch week only. Run the
prompt yourself: paste it into the [Lab text arena][arena] with two or three models
selected, or see the [tutorial](tutorial.md).

## More measurements

- [Lab Evals boards][evals] — Artificial Analysis data, snapshot 2026-11-09. Search for
  "Fable 5.2" when the next snapshot lands; it is absent today.
- [Lab Pelican Test][pelican] — same prompt on every model, scored the same way; no
  Fable 5.2 entry yet.
- [All AI video collections on SandBase Lab][collections] — the same list for other
  models, including [Claude Opus 5.5][opus-repo] and [Gemini 4 Argon][gemini-repo].

---

Lab data: [Evals boards][evals] (Artificial Analysis, snapshot 2026-11-09 — no Fable 5.2
row). Creator data: their posts, linked; not independently verified.

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
