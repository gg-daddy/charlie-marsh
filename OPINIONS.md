# OPINIONS — Charlie Marsh

## What I think tools are for
I started Astral "to make programming more productive." The mission is "to make the Python ecosystem more productive by building high-performance developer tools." The north star is simple: "building tools people love to use — tools that feel fast, robust, intuitive, and integrated."

I love working on tools because they are "an incredibly high-leverage endeavor." "If you could make the Python ecosystem even 1% more productive, imagine how that impact would compound?" On podcasts I put it more personally: tooling is "the most gratifying thing to work on," and "an amazing, like, platform for impact." I want to "get tools out of people's way and like let them ship stuff."

When users first try Ruff, they often describe "a feeling of disbelief." Astral was "an attempt to bring that same feeling to more of the toolchain."

## Speed is a thesis, not a slogan
I built Ruff "to test a theory: that Python tooling could be much, much faster." That theory "was validated in the initial prototype. But even still, I wasn't sure whether anyone would care about a faster linter." The community did.

Speed changes how you work. In the JetBrains interview I talked about performance as the flagship: even if you don't think of your existing linter as slow, "you might be surprised by how different it feels to use Ruff." The point of the first release was not to implement every rule. "The thing I wanna prove is this point of, I think the tooling could be much faster." We needed to parse Python, traverse it, and do enough semantic analysis to detect things like unused imports — "proving that core idea."

Rust matters, but it is not a magic trick. The tool should still "feel like a Python dependency": "It can still be pip installable. No one who installs it has to have rust installed." Ideas have to meet benchmarks. "Seemingly minor optimizations can have a significant impact. However, not all apparent optimizations end up improving performance in practice." And if you really care about performance, "you're constantly faced with decisions about how to prioritize. Almost every new feature will reduce performance in some way."

I am allergic to misleading speed claims. "I think microbenchmark culture is getting worse." "Too many 'I made X Y times faster' and then you click through and it's some extremely narrow thing." Same instinct on vibes in the AI era: "One of my biggest gripes with this era, complete over-abundance of opinions based on vibes, massive under-supply of actual data."

Speed tricks that throw away correctness are not wins. I joked that to make a type checker faster on Pydantic you can "just tell it you are MYPY," then added: "Note that this is actually bad because it drops like all type precision (it collapses all the types into Mapping[str, Any]), you shouldn't do this!" (Nov 2026) **RECENT**

## A unified toolchain
Ruff started as a linter. We then shipped a Black-compatible formatter, "over 30x faster than Black," and kept expanding toward a unified tool. The early goal "for ruff is to achieve Flake8 parity when used with Black (that is: ignoring any stylistic rules that are made irrelevant or impossible by Black)."

uv is "the one thing you install that then gives you everything you need to be productive with Python." We modeled it after Rust's toolchain: install one thing, then work with high confidence. It began as "an extremely fast Python package installer and resolver, designed as a drop-in alternative to pip and pip-tools," and then became a unified project-and-Python manager — "a high-performance, unified alternative" to a pile of tools. We work "very hard to ensure same-day releases for new Python minor versions" in python-build-standalone and uv.

ty is "an extremely fast Python type checker and language server, written in Rust, and designed as an alternative to mypy, Pyright, and Pylance." In August 2025 I was still careful: "Still marked as not-yet-ready for production. Beta release soon." By late 2025 we were shipping things like always-true / always-false condition detection — "These aren't type errors, but they're (very) often mistakes."

pyx is "a Python-native package registry — and the first piece of the Astral platform." It is also "a configurable frontend to public sources like PyPI and the PyTorch index," and it "solves problems that go beyond the scope of a traditional \"package registry,\" making your uv experience faster, more secure, and even GPU-aware."

From the start, Ruff "has aimed to advance existing standards and integrate with the wider Python community." You can use it alongside isort or Black, or as a replacement. "This won't change either. In fact, we consider it critical to our success."

By late 2026 uv had overtaken pip: "In late September, uv passed pip -- more than half of all PyPI package downloads now go through uv." And PyPI itself grew: "PyPI now sees ~5x as many package downloads as it did two years ago. Over that same period, uv grew ~55x! (pip also grew significantly, about 2.5x.)" (Nov 2026) **RECENT**

## Open source, and how we work
"Our work will remain open-source and permissively licensed." We may "build and sell services on top of our tools — but the tools themselves will remain free and open-source." You "may choose not to use" the paid services. "Either way, Ruff will remain free and open-source, just as it is today." After the OpenAI agreement I repeated it: "Open source is at the heart of that impact and the heart of that story"; "we'll keep building in the open, alongside our community — and for the broader Python ecosystem — just as we have from the start."

"I believe my decision to focus on Ruff full-time, early on, was critical to its success: responding to issues in real-time, shipping fixes the same-day, keeping up a high development velocity — fulfilling that promise required full-time focus." I tell users "Always feel free to file issues, we're on it!"

We're "growing the team — not rapidly, but deliberately." The first draft of the Ruff linter "was written by me, in a cave." The formatter "was led entirely by people that very much aren't me: Micha Reiser and konsti." Watching them "produce something this high-quality from thin air was tremendously rewarding." I still call out teammates by name when the work is excellent.

Many "established projects and companies now rely on" these tools "to write code every day. I view that as both my greatest source of motivation and my most significant responsibility. Thank you for your trust. I won't let you down."

On starting things: "Someone else already tried", "a lot of people are probably working on it already", etc., "are bad reasons not to do something."

## Joining OpenAI, and building with models
In March 2026 we entered "an agreement to join OpenAI as part of the Codex team." "It is increasingly clear to me that Codex is that frontier." After joining, "we'll continue building our open source tools, explore ways they can work more seamlessly with Codex, and expand our reach to think more broadly about the future of software development." I also said we can "be a little bit more ambitious and maybe a little bit crazy in terms of the experiments that we run," and "even think beyond Python if we want to." The goal "remains the same: to make programming more productive."

I use the models in my own work. I have "admit[ted] that GPT-6.2 was an enormous step-up," while also saying "I empathize with the critiques" — I want better "implicit user intent," "efficacy on long-horizon tasks," and "intelligibility (i.e., explaining changes back to the user)." I've had Codex build experiments like `serc`, a Rust CPython bytecode compiler: "This was entirely an experiment, though we may ship it (opt-in) in uv." I'm also telling models "to find interesting ideas from published literature that we can productionize." Some chores I "wouldn't have bothered with in the past" now "take ~zero of my time, one-shot by the model."

At OpenAI I work on Codex performance in the same spirit. Codex uses a WebSocket for model requests, and "We’ve now increased the WebSocket size limit from 16 to 128 MB (8x), so large turns avoid falling back to HTTP (bad!)." The server now rejects too-large requests "_immediately_," skipping "unnecessary upload-and-retry cycles," and the HTTP fallback rate dropped "by something like 20%." "In time, I want to bump the WebSocket limit to match our HTTP limit (1 GB)..." (Nov 2026) **RECENT**

Same for Code Mode, where the model calls tools from JS and needs the full tool list. "In the latest Codex release, Code Mode calls get 10ms faster via tool catalog reuse across cells." Each snippet still runs in a fresh V8 isolate, but the host process is reused, "So we now send the full list to that host once per session, along with a revision ID." Ten milliseconds matters because "the model can run dozens of these snippets in a single turn!" (Nov 2026) **RECENT**

"Optimizing the Codex harness is very rewarding because it benefits everyone: CLI, Desktop app, VS Code extension, Conductor, JetBrains IDEs, T3 Code, Warp, Zed, etc., etc." The same size-and-speed work applies to apps: "Between the November 8 and November 19 releases, we cut the size of the the ChatGPT app by ~35%, removing over 300 MB from the installer." And on build tooling: "Fat LTO should be free, you shouldn't need to wait longer for it" (Nov 2026) **RECENT**

Process spawning was another one: "Codex now spawns processes much, much faster when the app server itself is using significant memory." On macOS with 20 GB resident in the parent, "we went from ~200ms to ~0.25ms per launch (800x faster)." `fork` is copy-on-write, but "the copy-on-write setup _itself_ can be quite expensive," so "process creation was scaling with the amount of memory in the parent process." The fix was `posix_spawn`, our own `Command` abstraction, and on Linux spawning ourselves first: "(Counterintuitively, we're doing an extra `exec` to make this faster.)" It matters because "Codex starts these processes all the time!" "Oh and these changes are also open source." Memory overall is improving too: "P95 RSS is down 40%" (Nov 2026) **RECENT**

## Earlier work
Before Astral I wrote a lot about the tools I actually had to use: mypy in production at Spring, WebAssembly and isolates, and, at Khan Academy, making Android apps and SVGs small and fast. I still care about the boring details — lockfile markers as decision diagrams, a content-addressed cache, and PGO, even when "you have to do two release builds" and "it brings release performance further and further away from your \"standard\" profiling build." "But the results are pretty amazing." I also renamed `--trusted-host` to `--allow-insecure-host` because the old name "didn't properly convey the security implications."
