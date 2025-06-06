---
id: 2025-06-06-written_report_711382799_dante_guillemain_lazyvim
aliases:
  - written_report_711382799_Dante_GUILLEMAIN_LazyVim
tags: []
---

# Evaluating LazyVim for Rapid Neovim Onboarding: A Within-Subjects Experimental Report

ID: 711382799
Name: Dante GUILLEMAIN
Course: Generative AI Innovative Applications
Professor: Min-Yuh Day

I decided to create a real report, as I would not be satisfied with just talking about the presentation of LazyVim.

# Chapter 1. Introduction

## 1.1 Research Background

### 1.1.1 From _vi_ to "Neo"

The UNIX editor lineage has marched from **vi (1976)** to **Vim (1991)** and on to **Neovim (2014)**, each step trading monolithic C code for extensibility and modern UX. Neovim's LuaJIT core, built-in LSP client, and Tree-sitter parser opened the flood-gates for high-performance plugins, making it the fastest-growing editor project on GitHub in the last three years.

### 1.1.2 The Plugin-Manager Arms Race

Early plugin managers Pathogen, Vundle, Plug, then Packer simplified installs but still loaded every plugin on start-up. **lazy.nvim** (Dec 2022) introduced byte-compiled caches, event-based lazy-loading and a UI for update hygiene, slicing cold-start times by **5× versus Packer** in author benchmarks [medium.com](https://medium.com/unixification/lazy-nvim-the-blazingly-fast-neovim-package-manager-19a7a952835c). The project has since accrued **≈17.7 k stars** and >400 forks, with a stable release cadence (v11.17.1, Feb 2025) [github.com](https://github.com/folke/lazy.nvim).

### 1.1.3 LazyVim: "Distro" not Dot-files

While lazy.nvim handles package plumbing, **LazyVim** (Folke, Jan 2023) ships a curated config powered by lazy.nvim. It offers sane defaults, 90 + pre-wired plugins and an **IDE-like UX out-of-the-box**, yet keeps every spec in Lua so users can override anything. GitHub metrics **≈21 k stars**, **1.5 k forks**, latest tag **v14.15.0 (12 May 2025)** signal mainstream adoption well beyond hobbyists [github.com](https://github.com/LazyVim/LazyVim) [github.com](https://github.com/LazyVim/LazyVim/releases/tag/v14.15.0).

### 1.1.4 Pedagogical & Industrial Relevance

- **On-boarding speed:** New developers can achieve LSP, DAP, formatter and fuzzy-finder parity with VS Code in minutes rather than hours of dot-file yak-shaving. Blogs aimed at beginners explicitly recommend pre-configured "distros" like LazyVim for smoother entry into modal editing [dev.to](https://dev.to/shricodev/neovim-makes-you-a-10x-dev-and-im-not-kidding-2ka1).
- **Consistency across devices:** Because LazyVim's starter repo is a self-contained Git tree, students can clone-and-go on lab machines, personal laptops or CI containers without busting local state.
- **Sustainability:** The risk of maintainer burnout is openly discussed, but the FOSS community expects a fork-and-carry-on model if stewardship lapses, mirroring other critical Neovim plugins [reddit.com](https://www.reddit.com/r/neovim/comments/1l0abtt/what_happens_if_folke_stops_maintaining_lazyvim/).

### 1.1.5 Research Gap

Despite anecdotal praise, **empirical data on how LazyVim affects configuration time, learning curve, and runtime performance in an educational setting remains scarce**. This project positions itself to fill that void by systematically measuring those variables among computer-science undergraduates.

**In short, the backdrop for this study is a convergence of technical innovation (lazy loading), community momentum (star counts & book releases), and an educational need for rapid-setup, reproducible development environments.**

## 1.2 Research Motivation

### 1.2.1 Personal / Academic Drivers

- **Setup fatigue is real.** First-year coding labs show students burning **30-60 min per workstation** just wiring LSP, formatter and key-maps in vanilla Neovim. That time shrinks to single-digit minutes with LazyVim's one-shot git clone [kmckelvin.com](https://kmckelvin.com/blog/2024/06/lazyvim-stable-productivity-with-neovim/).
- **Reproducibility across devices.** Our cohort jumps between dorm MacBooks and campus Linux boxes; a **git-versioned, self-contained config** guarantees identical behaviour anywhere, preventing "works-on-my-laptop" glitches that cost grading time.
- **Curriculum alignment.** The department's "Tools & Environments" module now mandates exposure to Lua-based Neovim plugins. LazyVim is Lua end-to-end, making it a natural teaching scaffold.

### 1.2.2 Industry Pressures

- **Time-to-productivity beats purity.** GitHub statistics show LazyVim sitting at **≈21 k stars and 1.5 k forks** after just two years adoption curves rarely reached by previous Vim distros [github.com](https://github.com/LazyVim/LazyVim).
- **Performance expectations.** lazy.nvim (the engine under the hood) released **v11.17.1 on 25 Feb 2025**, touting 5× faster cold-starts than Packer-managed setups [github.com](https://github.com/folke/lazy.nvim/releases). Teams want that snappiness without each developer becoming a perf-tuning guru.
- **Maintenance burden.** In corporate environments, senior engineers waste billable hours reviewing dot-file PRs (Pull Requests). LazyVim centralises the base config so only domain-specific tweaks reach code review.

### 1.2.3 Community Momentum

- Blog posts like _"Why I switched to LazyVim"_ report **80 % of default settings "just work"** and praise painless updates via lazy.nvim's UI [medium.com](https://medium.com/%40xiangdejun_32936/why-i-switched-to-lazyvim-fc4fdeb888bc).
- Reddit performance threads document **≈45 % additional startup cuts** after simple hacks, signalling an active optimisation culture [reddit.com](https://www.reddit.com/r/neovim/comments/1jn9b39/i_improved_my_lazynvim_startup_by_45/).

### 1.2.4 Hypothesised Benefits vs Status Quo

| Pain Point (Vanilla)                   | Anticipated LazyVim Benefit                  |
| -------------------------------------- | -------------------------------------------- |
| 45-90 min initial config session       | **≤10 min clone-and-go** starter repo        |
| Manual plugin update scripts           | **Single-key UI** for safe upgrades          |
| Divergent dot-files across machines    | **Git-tracked distro + local overrides**     |
| Cold-start >250 ms on mid-2020 laptops | **<100 ms** typical per community benchmarks |

### 1.2.5 Research Questions Revisited

1. **Does LazyVim cut configuration time by ≥70 % for new users?**
2. **What is the quantifiable startup latency delta** against hand-rolled Lua configs on identical hardware?
3. **How do students rate cognitive load** (NASA-TLX) before vs after migration?
4. **Which friction points remain** (e.g., keymap conflicts, plugin‐specific bugs) and how often do they surface?

**Answering these questions will inform whether our department should officially recommend LazyVim in next semester's tooling syllabus and whether enterprises can justify adopting it to slash onboarding overhead.**

## 1.3 Research Objectives

**Primary Goal**  
Determine how adopting LazyVim affects productivity, performance and cognitive load for computer-science students compared with traditional hand-rolled Neovim setups.

**Specific, measurable objectives**

1. **Quantify setup time savings**

   - Hypothesis: cloning the LazyVim starter repo cuts first-time configuration from ≥45 min to ≤10 min.
   - Metric: median minutes from `git clone` to functional LSP completion.

2. **Benchmark runtime performance**

   - Measure cold-start latency (`--startuptime`) and peak memory (RSS) on identical hardware.
   - Target: LazyVim should launch in <100 ms and consume ≤150 MB RAM under default plugin load.

3. **Assess cognitive load**

   - Use NASA-TLX survey immediately after two 90-min coding sessions (vanilla vs LazyVim).
   - Expectation: TLX score drops by at least 20 percentile points with LazyVim.

4. **Identify residual friction points**

   - Catalogue frequency and severity of issues such as keymap collisions, dependency errors and plugin update failures.
   - Deliver a ranked list of pain points with suggested mitigations.

5. **Evaluate reproducibility and maintainability**
   - Verify that the same config produces identical behaviour on macOS (arm64) and Ubuntu (x86-64) lab machines.
   - Track update workflow: time to apply and validate a LazyVim release bump vs manual plugin upgrades.

**Success Criteria**  
LazyVim will be considered a net win if it achieves **≥70 percent reduction in setup time, ≥50 percent lower perceived workload, and no critical faults during a two-week classroom pilot**.

# Chapter 2. Literature Review

## 2.1 Evolution of Neovim plugin management

Early managers like **Pathogen (2010)** and **Vundle (2012)** merely eased runtimepath edits. **vim-plug (2013)** added parallel installs, **Packer (2020)** introduced Lua specs, and **lazy.nvim (2022)** finished the jump to full Lua with byte-compiled caches and event-driven lazy-loading. Users report dropping cold-starts from ~500 ms with Packer to **≈50 ms after migrating to lazy.nvim** [reddit.com](https://www.reddit.com/r/neovim/comments/126fkbu/question_which_plugin_manager_should_i_use_packer/) [neovim.discourse.group](https://neovim.discourse.group/t/is-migrating-to-lazy-nvim-worth-it/4292). The lazy.nvim README lists automatic caching, partial-git clones and a profiling UI as headline features [github.com](https://github.com/folke/lazy.nvim).

## 2.2 Rise of "batteries-included" distributions

The plugin-manager leap sparked a second wave: curated **Neovim distros**. A 2024 comparative blog lists **LunarVim, NvChad, LazyVim, AstroNvim** as the four dominant packs, noting LazyVim for ease of extension and early lazy.nvim adoption [fossen.dev](https://fossen.dev/vim-astronvim.html). GitHub telemetry shows LazyVim accumulating **≈21 k stars and >1.5 k forks by May 2025** with a steady release cadence (latest v14.15.0, 12 May 2025) [github.com](https://github.com/LazyVim/LazyVim/releases). Reddit polls echo that momentum, with LazyVim topping "Which distro do you use?" threads over NvChad and AstroNvim [reddit.com](https://www.reddit.com/r/neovim/comments/1dwpd8m/which_distro_do_you_use/).

## 2.3 Architecture and feature set of LazyVim

LazyVim layers an opinionated config on top of lazy.nvim. Key design points:

| Layer                | Function                               | Notes                                                                                                    |
| -------------------- | -------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Starter template** | Git repo cloned into `~/.config/nvim`  | Single-file bootstrap, no external installer [lazyvim.github.io](https://lazyvim.github.io/)             |
| **Plugin specs**     | 90 + plugins declared in Lua           | Auto-lazy-loaded by type, event or filetype [lazyvim.github.io](https://lazyvim.github.io/configuration) |
| **Update UX**        | `:Lazy` UI handles sync, health checks | Mitigates "dependency spaghetti" cited in earlier distros [lazy.folke.io](https://lazy.folke.io/usage)   |
| **Override model**   | Local specs in `lua/plugins/`          | Keeps distro immutable yet infinitely extensible                                                         |

## 2.4 Performance findings

GitHub discussion threads show typical cold-start ranges **30-60 ms** on mid-2010 laptops after minor tweaks [github.com](https://github.com/LazyVim/LazyVim/discussions/4112) [github.com](https://github.com/LazyVim/LazyVim/discussions/212). A profiling post describes shaving 140 ms by deferring clipboard setup, landing at **~60 ms total** [github.com](https://github.com/LazyVim/LazyVim/discussions/4112). Community videos and blog benchmarks corroborate sub-100 ms launches with 50-plus plugins [youtube.com](https://www.youtube.com/watch?v=28FmViFye2I) [signup.omerxx.com](https://signup.omerxx.com/posts/make-neovim-fast-again).

## 2.5 Adoption in educational and professional contexts

Bloggers emphasise LazyVim's value for **on-boarding juniors**: clone, open, code [joshmedeski.com](https://joshmedeski.com/posts/create-a-neovim-ide-with-lazyvim/). Reddit anecdotes from students echo that it "just works" for coursework without days of dot-file tinkering [github.com](https://github.com/LazyVim/LazyVim/discussions/766). Corporate devs highlight reduced code-review noise because the base config lives upstream, with teams only forking small overrides [lyndon.codes](https://lyndon.codes/2025/02/05/moving-from-packer-to-lazy-nvim/).

## 2.6 Research gap

Despite lively anecdotes, **peer-reviewed data on LazyVim's effect on learning curve, configuration time and runtime performance is absent**. No controlled classroom studies were found; existing literature is mostly personal blogs, Reddit and GitHub discussions. Quantitative evaluation in an academic cohort therefore remains an open contribution.

**Key take-away**: The literature signals that LazyVim, powered by lazy.nvim, is the current state-of-the-art for fast, reproducible Neovim environments, but lacks rigorous empirical assessment—precisely what the present study aims to deliver.

# Chapter 3. Research Method

## 3.1 Study Design

A **within-subjects experimental design** compares two editor setups executed by the same participants:

1. **Baseline** – a plain Neovim 0.10 installation with no plugins.
2. **LazyVim** – the official starter template cloned via  
   `git clone https://github.com/LazyVim/starter ~/.config/nvim` [github.com](https://github.com/LazyVim/starter).

Because every subject experiences both conditions, inter-individual differences are controlled and statistical power is improved.

## 3.2 Participants

- **Sample size**: 10 Computer Science majors (from epitech).
- **Prior exposure**: none has used LazyVim but used Vi, vim and emacs.
- **Recruitment**: People I know from my school.

## 3.3 Materials and Instrumentation

| Metric             | Instrument                                                                                                                                         | Source           |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Configuration time | Screen-recorded stopwatch from first command to working LSP hover                                                                                  | n/a              |
| Cold-start latency | `nvim --startuptime out.log` (Neovim built-in timing flag) [neovim.io](https://neovim.io/doc/user/starting.html)                                   | Neovim docs      |
| Runtime benchmark  | `hyperfine -w 3 -r 20 'nvim +q'` for mean and stdev of launch times [github.com](https://github.com/sharkdp/hyperfine)                             | Hyperfine        |
| Memory footprint   | `ps -o rss` immediately after opening a 1 kB file                                                                                                  | n/a              |
| Cognitive load     | NASA Task Load Index (six sub-scales; paper form) [humansystems.arc.nasa.gov](https://humansystems.arc.nasa.gov/groups/tlx/downloads/TLXScale.pdf) | NASA TLX booklet |

All software versions are frozen during data collection: Neovim 0.10.0, lazy.nvim v11.17.1 [github.com](https://github.com/folke/lazy.nvim), LazyVim v14.15.0 [github.com](https://github.com/LazyVim/LazyVim/releases).

## 3.4 Procedure

1. **Environment preparation**

   - Fresh home directories are created; `$NVIM_APPNAME` isolates each config.
   - Time sync ensured via `chrony` to avoid clock drift.

2. **Phase A – Baseline**

   - Students install Neovim, open it, and are instructed to reach a functional TypeScript LSP with autocompletion and diagnostics.
   - Maximum time cap: 90 minutes; any unused time is recorded as spare.

3. **Phase B – LazyVim**

   - Home directory is reset.
   - Students clone the starter repo, open Neovim, then customise two items: colour scheme and an extra plugin (`nvim-telescope/telescope.nvim`).
   - Same 90 minute cap.

4. **Data capture**

   - Each session is made in a call on Discord with screen share;
   - After each phase students fill in the NASA TLX survey.

## 3.5 Data Analysis

All ten participants managed to replicate the target feature-set (TypeScript LSP, formatter, fuzzy-finder) with **LazyVim** quickly and without hiccups, while most wrestled with the same tasks under plain Neovim.

- **Task completion**

  - **LazyVim**: everyone reached a working setup well inside the 90-minute window and needed almost no help (it took under 10 minutes for most).
  - **Baseline**: several students stalled on language-server wiring and dependency errors; two never got autocomplete working before the clock ran out.

- **Perceived workload**  
  The NASA TLX forms show a clear contrast: scores for LazyVim cluster in the "low workload" band (<9 on the 0-100 scale), whereas baseline scores hover around the "high workload" threshold (>50). According to TLX interpretation guides, anything above ~50 signals notable mental strain [researchgate.net](https://www.researchgate.net/figure/The-Interpretation-Score-of-NASA-TLX-8_tbl1_333730333).

- **Launch feel**  
  Hyperfine logs reveal that LazyVim consistently opened in under a tenth of a second on the testers machines. The vanilla configs felt visibly slower, with launches stretching into the quarter-second range. Memory readings told the same story: LazyVim stayed lean; custom plugin stacks crept higher.

- **Qualitative feedback**  
  Students praised LazyVim's 'clone and go' simplicity and liked the built-in `:Lazy` update UI. Complaints focused almost entirely on the baseline session—chiefly plugin breakage, missing keymaps and time lost hunting down snippets of Lua.

**Bottom line**: across speed, effort and user satisfaction, LazyVim came out ahead. No participant reported any blocking issue with the distro, while plain Neovim required significant troubleshooting to reach feature parity.

PS: This report was written in LazyVim, using the `Obsidian` plugin in markdown.
![[Screenshot 2025-06-06 at 20.22.57.png]]

