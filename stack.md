<!--
Copyright (C) 2025 Chase Finch
SPDX-License-Identifier: MIT
-->
# Software Stack

These are the languages, tiers, and front-end choices that compose into harmonious stacks, along with the trade-offs that motivate each.

## Languages

### Python

- Optimal development experience
  - Pleasing syntax and tight code management == optimization for readability.
  - REPL access, no compilation
- Optimal libraries — Django, pip, mypyc
- Works well with others
- Comparatively slow
  - Use Python free-threading mode
  - Pair with Rust (PyO3/maturin) or C for performance

### Node.js

Peer to Python. Acceptable alternative if you prefer tight integration with SvelteKit instead of Python's best-in-class dev-X, ORMs, code management, and buffer protocol for sharing data with Rust.

### Rust

- Safety
- Embeddable + Heapless-capable
- `unsafe` tools will match C's capability in memory creativity
- "Raw Metal Rust" to match C's compile-time and run-time determinism
- Sufficient abstractions & idioms for clean domain representation without hidden overhead
- Sprawling code (low readability) is a risk
- Static linking preferred (no stable ABI)
- Use `impl` and LTO (Link-Time Optimization) for ideal performance

### C & C++

- Creative freedom with memory as a first-class feature
- Direct access to explicit & deterministic C code within a larger (C++) codebase
- More explicit mapping than Rust for simplest C code in each file (no panic path, drop flags, inlining control)
- Ecosystem advantage over Rust for game dev, UIs, other areas
- Mature certification ecosystem
- Sufficient, low-overhead abstractions for *some* domain representation with C++ when following some best practices (no exceptions, no `std::endl`, pimpl idiom). Sprawling code (low readability) is a huge risk
- Static and/or dynamic linking

### Swift

- Best ergonomics for compiled, polymorphic apps…
- …though excessive features are available. Sprawling code (low readability) is a huge risk.
- Sufficient abstractions for excellent domain representation.
- Acceptable, batteries-included alternative to a Python+Rust stack, where you sacrifice the maintainability of Python and some of the performance of Rust (but not orders of magnitude of either).
- Use `some` and `-O -wmo` for ideal compilation
- Static and/or dynamic linking

### Go

- Consider it a layer of abstraction on top of the Rust/C++ language tier, which bakes in features for concurrency. Garbage collection and injected concurrency cooperation makes for superior multi-threaded IO ergonomics compared to Rust, with sufficient speed compared to re-rolling concurrency with Tokio in Rust.
- Sprawling code is a small risk; fewer features are a bonus
- Cumbersome for SIMD optimizations, compiler optimized for compilation speed over performance in many cases

## Reasonable stacks

- Python + Rust (when you can afford it)
- Node.js + Rust (for dynamic web interface first)
- Swift (for the right ecosystem)
- Go (for I/O concurrency first)
- C & C++ (for memory manipulation and device/ecosystem compatibility)
- Rust (for everything else, incl. embedded programming)

## Desires

- Better code management (linters, formatters, static analysis) for Swift
- Better code management (linters, formatters, static analysis) for Node
- Better libraries & frameworks for Rust

---

## Front-end

### CSS options

- Tailwind
- WebAwesome

### JS options

- AlpineJS (preferred, when components can be open boxes and performance of runtime binding is acceptable)
  - Use via CDN with all-inline declarations for simpler projects
  - Use via bundle step with TypeScript for larger projects
- Svelte using Vite (if front-end performance is paramount)
  - For an SPA or just client-side navigation, use InertiaJS
  - Use TypeScript
  - Can use Storybook with this approach
- JAM stack (if I have to): SvelteKit
  - Server-side rendering
  - CVA to pass utility classes as props
  - API options:
    - Just SvelteKit
    - Sanity (etc) CMS
    - Public service-specific APIs
    - Custom API (Django REST framework, Prisma, Drizzle, raw, etc).
  - Use TypeScript
  - Can use Storybook with this approach
  - I prefer to think of HTML as a document, instead, and to build native apps in native tech stacks. State is good, but URL-changing-state is progressive enhancement.

Limitations on JS: Imperative JS should really only be used for (1) data transformations and (2) wrapping browser functionality and (3) named state changes, mappings, or reductions (which are really functional, rather than imperative).

Pass data to JS, but not UI. Prerender only as a performance enhancement.

Web & Alpine components and CSS components should be used sparingly, and with few DOM elements. They may have some niceties (a dropdown web component, a button Tailwind component) that are worthwhile in a project, but generally UI is too fragmented for this. (Note that with the Svelte and JAM stack options above, the JS components should play a role more similar to template partials.)
