# Claude Fable 5.2 prompt guide: seven patterns from real videos

English · [简体中文](zh-CN/prompt-guide.md) · [← Back to the collection](../README.md)

Every pattern below is lifted from a prompt a creator published with a video in this
collection, and each one links to that post. They are not rules the model enforces; they are
what worked during launch week when someone asked for one page or one film and got it.

The short version: **name the deliverable and the renderer, set a creative bar, give it a
job it cannot fake, choreograph what moves, write the physical constraint, choose the effort,
and have it check its own work.**

## 1. Name the deliverable and the renderer in the first sentence

The most-reused prompt in this collection contains no visual description at all:

> "make a dynamic 15-second motion graphics video that shows what an incredible motion
> designer you are, like it's your showreel for a résumé. go all out."
> — [@MatinSenPai][matin]

On a language model, "video" means "a page that renders a video" — the model picks the
renderer, duration and frame unless you say them. Say them: one HTML file, 1920×1080,
15 seconds, Canvas/SVG/Three.js. Or skip the page and name the tool directly when you want a
build, not a render:

> "Can you write the most intricate photorealistic simulation of honey in WebGL in the
> browser"
> — [@deedydas][honey]

## 2. Set a creative bar instead of a specification

"Go all out" and "showreel for a résumé" do real work — they tell the model to show taste,
not to tick boxes. The highest-engagement launch-week pieces all carried a bar like "AAA
quality", "the most beautiful video you can" or a named style:

> "make me the most beautiful video you can"
> — [@aollivier82][aollivier]

> "build a hyper-realistic first person shooter set on a tropical island, AAA quality
> visuals and sound effects, make no mistakes"
> — [@imantiai][fps]

A bar is one line: "like an Apple keynote", "AAA quality", "the most beautiful video you
can". Put it next to the deliverable.

## 3. Give it a job it cannot fake

Photorealism prompts work because they name a thing the output can only achieve by being
right: real physics, real geometry, a real mechanism. "A hyper-realistic shooter" that
renders 30 million polygons a frame, or "the most intricate photorealistic simulation of
honey" that is a physics-based realtime render, leave no room for a static picture with a
play button:

> "I gave Fable 5.2 (max) a single prompt … and let it run unattended. Everything
> procedural in raw WebGPU, no engine."
> — [@imantiai][fps]

If the target is a simulation, a game or an interactive scene, name the mechanism the video
must demonstrate — physics, traffic, a playable loop — not just the look.

## 4. Choreograph what moves, beat by beat

Posts that describe motion rather than objects get films, not slideshows. The recurring
launch-film prompts say how one state becomes the next — a shape, a wipe, a camera push —
instead of listing scenes:

> "参考这个 launch video 风格给 BlewUp 做一个类似的视频" (make a video like this launch
> video for BlewUp) — [@wangray][wangray]

> "create an svg of a pelican riding a bicycle across five animated seasons"
> — [@marcthecreatorr][pelican]

Describe the transition, the season change, the thing that carries the eye — and the model
animates the in-between. A scene list alone gets cuts.

## 5. Write the physical constraint out loud

For procedural 3D and animation, the constraint is the prompt. The strongest examples name
exactly what must not happen — penetration, intersection, a bone count, a frame budget:

> "generate a sea serpent and animate it in Blender, 20 seconds of coiling around a ship
> without ever passing through the hull."
> — [@Stefan_3D_AI][serpent]

> "make it check its own work with numbers. grip within 1 cm of the palm, exactly 2 eyes…"
> — [@0xKense1][rig]

A negative invariant ("never passing through the hull", "one continuous take, no cuts")
costs one sentence and prevents the most common failure — the model hitting the time limit
mid-scene and leaving a broken frame.

## 6. Pick the effort — and say it

Launch-week creators were loud about `reasoning_effort`: the same prompt is a different
film at `medium` and `max`, in quality, time and bill. Name the effort you want — and put
it in the post so the comparison is honest:

> "Run on medium by the way" — [@JamesMalsawm][james]
> "Via Claude Code + Blender on Max effort." — [@Stefan_3D_AI][serpent]
> "(Extra High effort)" — [@aug5thmusic][fugue]

For a draft, start at `medium` and only raise it when the composition is right; several
creators report Fable one-shotting at medium what Opus needed max for.

## 7. Have it check its own work

Two patterns recur in the longest-running builds: the model opens and fixes its own page,
or it is handed a checking loop. One documentary creator's biggest unlock was making the
model *study* its references frame by frame before writing:

> "make your ai study your references one large frame every quarter second, not skim
> them."
> — [@naometzger][doc]

> "use a project manager chat. one chat turns your thoughts into a brief, then hands the
> whole job to a fresh fable chat … it changes only what's on the list"
> — [@naometzger][doc]

Pair a self-check with a recording path — a fixed-length loop or an autoplay camera tour —
so nothing depends on a mouse. The [tutorial](tutorial.md) records with
[`scripts/record.mjs`](../scripts/record.mjs).

## Fill-in template

```text
One self-contained HTML file, 1920x1080, {seconds} seconds, {renderer}, no external assets.

Goal: {one sentence — what the viewer should feel or understand}.
Creative bar: {like an Apple keynote / AAA quality / your showreel — go all out}.
Job: {the mechanism that must actually work — physics, traffic, a playable loop}.

Beats: open on {first frame}; then {transition 1 -> 2 -> 3}; close on {last frame}.
Invariant: {what never changes — one take, no cuts, never passing through X}.
Effort: reasoning_effort={medium|high|xhigh|max}.

Before you finish: open the page, fix console errors, and make the animation loop cleanly
for a {seconds}-second recording.
```

## Where these came from

- [@MatinSenPai][matin] — the fifteen-second showreel prompt that keeps being reused.
- [@deedydas][honey] — the one-line photorealistic WebGL honey simulation.
- [@aollivier82][aollivier] — "the most beautiful video you can".
- [@imantiai][fps] — the nine-hour unattended WebGPU FPS build and its telemetry.
- [@wangray][wangray] — the one-line launch-video style transfer.
- [@marcthecreatorr][pelican] — the pelican-across-seasons SVG test.
- [@Stefan_3D_AI][serpent] — the sea-serpent Blender constraint and its token bill.
- [@0xKense1][rig] — make it check its own work with numbers.
- [@JamesMalsawm][james] — same-prompt Fable vs Opus at medium effort.
- [@aug5thmusic][fugue] — Extra High effort named in the prompt.
- [@naometzger][doc] — studying references and a project-manager chat.
- [@0xbobaaa][bob] — one HTML file, zero assets, Fable 5.1 vs 5.2 side by side.

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
