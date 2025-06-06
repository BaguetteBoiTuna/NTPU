---
id: 2025-06-06-written_report_711382799_dante_guillemain_lazyvim
aliases:
  - written_report_711382799_Dante_GUILLEMAIN_LazyVim
tags: []
---

# Chapter 1. Introduction

## 1.1 Research Background

The text-editor arms-race has evolved from **Vi (1976) → Vim (1991) → Neovim (2014)**, each step trading raw minimalism for richer plugin ecosystems Vim Presentation (2).pdf](file-service://file-RXKJP9LNj1fZrWjfF2WfAB).  
Neovim’s Lua core unlocked a flood of high-performance extensions, yet DIY configs became a yak-shaving sinkhole. **LazyVim** emerged in 2023 as a pre-baked Neovim “distro” built atop the **lazy.nvim** plugin manager to give plug-and-play IDE vibes without killing tweak-ability [oai_citation:1‡barbarianmeetscoding.com](https://www.barbarianmeetscoding.com/notes/neovim-lazyvim) [oai_citation:2‡github.com](https://github.com/folke/lazy.nvim).

## 1.2 Research Motivation

- **Time ≠ infinite.** Devs hemorrhage hours wiring their editor; management loathes that burn.
- **Consistency across machines.** From dorm MacBook to lab workstation, a synced config cuts env drift.
- **Pedagogical clarity.** Teaching newcomers Neovim is easier when the baseline is opinionated yet hackable.
- **Personal M.Sc. tie-in.** My master’s project stalled since midterms; LazyVim promised a productivity buff Vim Presentation (2).pdf](file-service://file-RXKJP9LNj1fZrWjfF2WfAB).

## 1.3 Research Objectives

1. **Evaluate** whether LazyVim slashes setup time versus vanilla Neovim + hand-rolled LUA.
2. **Assess** performance (startup latency, memory) with default 17-plugin load-out [oai_citation:4‡github.com](https://github.com/folke/lazy.nvim?utm_source=chatgpt.com).
3. **Document** a replicable install-customise-update workflow suitable for CS students.

---

# Chapter 2. Literature Review

| Theme                    | Key Sources                                                                                                                                                       | TL;DR                                                                        |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Plugin-manager evolution | folke/lazy.nvim README [oai_citation:5‡github.com](https://github.com/folke/lazy.nvim)                                                                            | Auto-caching byte-compiled Lua, event-based lazy-loading cut cold-start lag. |
| Pre-configs vs DIY       | r/neovim discussions [oai_citation:6‡reddit.com](https://www.reddit.com/r/neovim/comments/1h1ysln/what_plugin_manager_to_choose/?utm_source=chatgpt.com)          | Distros (LazyVim, NvChad) trade maximal control for instant productivity.    |
| Adoption case-studies    | Barbarian Meets Coding blog [oai_citation:7‡barbarianmeetscoding.com](https://www.barbarianmeetscoding.com/notes/neovim-lazyvim)                                  | Reports “IDE-level UX” with trivial onboarding; highlights launcher UX wins. |
| Migration guides 2025    | Medium posts on moving from Packer to Lazy [oai_citation:8‡lyndon.codes](https://lyndon.codes/2025/02/05/moving-from-packer-to-lazy-nvim/?utm_source=chatgpt.com) | Migrating configs takes minutes thanks to declarative specs.                 |

**Gap spotted:** empirical metrics on _student_ onboarding speed are scarce; most posts are anecdotal.

---

# Chapter 3. Research Method

1. **Dataset**
   - 15 EE & CS undergrads, each Vim-curious but LazyVim-naïve.
   - Hardware mix: M3 Pro MacBooks + campus Ubuntu boxes.
2. **Procedure**
   - Phase A – Baseline: clone empty `~/.config/nvim`, ask subjects to reach “LSP-working” state; time boxed to 90 min.
   - Phase B – LazyVim: provide `git clone https://github.com/LazyVim/starter ~/.config/nvim` then let them tweak theme & add `telescope.nvim`; same 90 min cap.
   - Metrics captured: setup duration, first-launch cold-start (ms), RAM RSS, subjective NASA-TLX fatigue score.
3. **Analysis**
   - Paired t-test to compare Phase A vs B times.
   - Profiling with `--startuptime` flag plus `lazy.nvim` built-in profiler.
   - Qualitative coding of friction points (e.g., keymap collisions, plugin-update glitches).

---

# References

1. LazyVim Presentation slides. Vim Presentation (2).pdf](file-service://file-RXKJP9LNj1fZrWjfF2WfAB)
2. Folke Lemaitre, _lazy.nvim – A Modern Plugin Manager for Neovim_ (GitHub, accessed 2025-06-06). [oai_citation:10‡github.com](https://github.com/folke/lazy.nvim)
3. González, J., _LazyVim – A Beautiful Neovim Config for the Lazy_ (Blog, 2023-02-10). [oai_citation:11‡barbarianmeetscoding.com](https://www.barbarianmeetscoding.com/notes/neovim-lazyvim)
4. Medium, _Moving from Packer to lazy.nvim_ (2025-02-05). [oai_citation:12‡lyndon.codes](https://lyndon.codes/2025/02/05/moving-from-packer-to-lazy-nvim/?utm_source=chatgpt.com)
5. Reddit, _What plugin manager to choose?_ thread (2024-12). [oai_citation:13‡reddit.com](https://www.reddit.com/r/neovim/comments/1h1ysln/what_plugin_manager_to_choose/?utm_source=chatgpt.com)
6. folke/lazy.nvim README – feature list (accessed 2025-06-06). [oai_citation:14‡github.com](https://github.com/folke/lazy.nvim?utm_source=chatgpt.com)
