# Showcase archetype

For READMEs where the file itself is the demo. Animated headers, typed taglines, gradient banners, theme-aware images, stats cards, contribution graphs, skill badges. The reader's first impression is "wow," and the second is "and it's all real."

Use this archetype only when the project earns it. Most repos don't. The ones that do are GitHub profile READMEs, hackathon submissions, personal portfolios, and side projects whose author wants the README to be a showpiece.

## When to pick this archetype

- The repo is a **GitHub profile README** (lives at `username/username`).
- The project is a **hackathon submission** or **personal portfolio**.
- The author has explicitly asked for "make it look really cool," "animated," "visually stunning," "showcase," or named a profile they want to match.
- A side project where the README is part of the brand and the author wants flair.

Do **not** pick this archetype for:

- Libraries, CLIs, frameworks, or apps targeting other developers as users. Visual flair on a serious dev tool reads as a red flag.
- Internal monorepo packages. Coworkers want owner contacts, not a typing animation.
- Production-grade products or anything aimed at enterprise readers.

If in doubt, don't pick this. The user will tell you they want it.

## Default tone

Tone follows whatever the project would have *without* the visuals. Visuals are the addition, not a replacement for substance. A profile README about a backend engineer should read backend-engineer underneath the wave banner; a hackathon submission can be excited but still concrete.

The skill is creative *within* the chosen tone. No marketing-speak just because the page is colorful.

Sentence-case headings unless the project's existing brand uses title case. First person is fine for profile READMEs.

## Visual elements toolkit

Pick **2 to 4** elements, not 12. Density is the difference between "showcase" and "tacky." The toolkit below is a menu; treat it as such.

### Animated banner / hero

- **capsule-render** for animated wave/gradient headers and footers:
  ```md
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=180&section=header&text=Project%20Name&fontSize=60&animation=fadeIn" alt="banner" />
  ```
  Types: `waving`, `wave`, `slice`, `cylinder`, `egg`, `rounded`, `soft`. Animations: `fadeIn`, `twinkling`, `blinking`. Choose one, not all.
- **readme-typing-svg** for an animated typing tagline:
  ```md
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=22&duration=3500&pause=600&color=8A2BE2&center=true&vCenter=true&width=600&lines=Frontend+engineer.;Side-project+enthusiast.;Caffeine+converter." alt="typing" />
  ```
  Keep `lines` to 2 to 4. Each line should be a real claim, not marketing.
- **Static gradient SVG** as an alternative if you don't want network-fetched assets. Hand-rolled SVG checked into the repo loads faster and never breaks.

### Theme-aware images

GitHub renders different images for light and dark mode if you use `<picture>`:

```md
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/hero-dark.png" />
  <source media="(prefers-color-scheme: light)" srcset="docs/hero-light.png" />
  <img alt="Hero" src="docs/hero-light.png" />
</picture>
```

Always provide both. A dark-mode-only image is invisible on a light reader's screen.

### Stats and activity widgets

Network-fetched, render as live SVG, refresh on view:

- **github-readme-stats** (anuraghazra): general stats card.
- **github-readme-streak-stats** (DenverCoder1): contribution streak.
- **github-profile-trophy** (ryo-ma): trophies for milestones.
- **github-readme-activity-graph** (Ashutosh00710): line chart of activity.
- **Snake** (Platane/snk via GitHub Action): the contribution graph eaten by a snake. Requires a workflow.

Pick at most two. A README with five stats cards is unreadable.

```md
<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=USER&show_icons=true&theme=transparent&hide_border=true" height="160" alt="stats" />
<img src="https://github-readme-streak-stats.herokuapp.com/?user=USER&theme=transparent&hide_border=true" height="160" alt="streak" />

</div>
```

Use `theme=transparent` and `hide_border=true` for a cleaner look that adapts to either theme.

### Tech / skill badges

- **skillicons.dev** for compact icon rows:
  ```md
  <p align="center">
    <a href="https://skillicons.dev"><img src="https://skillicons.dev/icons?i=ts,react,nextjs,tailwind,postgres,docker" alt="stack" /></a>
  </p>
  ```
  6 to 12 icons. Don't list every language you've ever touched.
- **shields.io** for prose-style badges with custom colors and links.

### Demos and motion

- **Animated GIF** (preferred for short, recorded interactions). Keep under 2 MB; compress aggressively. Embed at the top of the relevant section.
- **MP4 / WebM** via HTML `<video>`: works on GitHub for some accounts; fall back to GIF if it doesn't render.
- **Lottie** (JSON-based animations): not natively rendered by GitHub. Convert to GIF or short MP4 first.

### Section dividers and footer

- A second capsule-render with `type=waving&section=footer` echoes the hero.
- Centered horizontal SVG line with gradient: less common but more restrained.

## Section structure

Showcase READMEs are usually shorter than they look. The visuals carry the weight; the text is sparse. A typical structure:

```md
<animated banner>

<typing svg with 2 to 4 real claims>

## About
<two short paragraphs: who/what, real specifics, no marketing>

## Stack / Tools
<skill icon row>

## Featured work / Projects
<2 to 4 project cards or a stats widget>

## Stats
<at most two stat widgets>

## Contact / Links
<short list of links: site, blog, email, social>

<animated footer (optional)>
```

For a project showcase (not a profile), replace "About" with "What it does" and "Featured work" with a single hero screenshot or demo GIF.

## Mini example skeleton (profile flavor)

```md
<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=180&section=header&text=Vivek&fontSize=72&animation=fadeIn" alt="banner" />

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=22&duration=3500&pause=600&color=8A2BE2&center=true&vCenter=true&width=600&lines=Frontend+engineer.;Local-first+enthusiast.;Building+md-craft." alt="typing" />
</p>

## About

I build local-first developer tools and the occasional weekend app. Most of what I ship is small, opinionated, and TypeScript.

I work at [Acme](https://acme.com) by day and on side projects by night. Currently rewriting my note-taking app for the third time. I will keep doing this.

## Stack

<p align="center">
  <a href="https://skillicons.dev"><img src="https://skillicons.dev/icons?i=ts,react,nextjs,tailwind,postgres,docker,go" alt="stack" /></a>
</p>

## Featured

| Project | What it is |
| --- | --- |
| [md-craft](https://github.com/me/md-craft-skill) | A Claude skill for writing project markdown that doesn't read like AI |
| [tilde](https://github.com/me/tilde) | Local-first Markdown notes app, plain `.md` files |
| [drift](https://github.com/me/drift) | Typed env var loader for Node, zero dependencies |

## Stats

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=me&show_icons=true&theme=transparent&hide_border=true" height="160" alt="stats" />
<img src="https://github-readme-streak-stats.herokuapp.com/?user=me&theme=transparent&hide_border=true" height="160" alt="streak" />

</div>

## Links

[site](https://valeti.live)  ·  [blog](https://valeti.live/writing)  ·  [email](mailto:hi@valeti.live)

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=80&section=footer" alt="footer" />
```

## Mini example skeleton (project flavor)

```md
<img src="https://capsule-render.vercel.app/api?type=slice&color=gradient&height=180&section=header&text=Tilde&fontSize=72" alt="banner" />

<p align="center">A local-first Markdown notes app. Plain files, fast as anything, no cloud.</p>

<p align="center">
  <a href="https://tilde.app">Live demo</a>  ·
  <a href="https://docs.tilde.app">Docs</a>  ·
  <a href="https://discord.gg/tilde">Discord</a>
</p>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/hero-dark.png" />
  <source media="(prefers-color-scheme: light)" srcset="docs/hero-light.png" />
  <img alt="Tilde" src="docs/hero-light.png" />
</picture>

## What it is

Tilde stores everything in plain `.md` files on your machine. No accounts, no cloud, no lock-in. Sync is opt-in via Git or iCloud.

## Try it

Hosted demo at [tilde.app/demo](https://tilde.app/demo) or download the desktop app from [tilde.app/download](https://tilde.app/download).

## Run locally

```bash
git clone https://github.com/me/tilde
cd tilde
pnpm install
pnpm dev
```

## Stack



## License

AGPL-3.0

```

## Anti-patterns specific to showcase

- **Visual overload**. Five widgets, three banners, a typing SVG, a snake graph, a trophy wall, a Lottie, and a contribution chart all on one page. Pick 2 to 4 elements; the rest is noise.
- **Stale or fake stats**. A profile README showing a 200-day streak that ended in 2023 looks worse than no streak at all. Either keep the widgets or remove them when they go cold.
- **Marketing copy in the typing animation**. "Innovating the future of code." Nobody believes it. Use the typing SVG for real claims: roles, projects, current focus.
- **Skill-icon walls of 30 logos**. If you list every tool you ever read a tutorial about, the section means nothing. Pick the 6 to 10 you actually use.
- **Dark-mode-only images**. Always pair light/dark via `<picture>`, or use a transparent-background asset.
- **Heavy GIFs**. A 12 MB GIF in the hero ruins the load. Compress, dither, drop frames, or convert to short MP4.
- **Profile-style widgets on a project README**. Streak cards and trophies belong on `username/username`, not on a library or product repo.
- **Showcase-as-distraction-from-substance**. If the project is thin, no banner saves it. Make the project good first.

## Notes for the AI being creative here

The point of this archetype is creative latitude inside structural restraint. Things to try, with the user's permission:

- A **custom hand-rolled SVG hero** instead of capsule-render, for a unique look that doesn't depend on a third party.
- A **theme-matched color palette** pulled from the project's logo or brand site, used consistently across banner, typing SVG, and badge colors.
- A **mermaid diagram with deliberate typography** (custom node shapes, arrow labels) to show project structure visually instead of as a bullet list.
- A `**<details>` "easter egg"** at the bottom: a short, fun fact, a TODO list, or a hidden ASCII art. Optional, never required.
- An **animated favicon-sized SVG** in the corner of the hero block as a personal mark.

Always: ask before adding. Always: keep the count low. Always: make sure the page still tells the reader what the project *is*, even if all the network-fetched widgets fail to load.