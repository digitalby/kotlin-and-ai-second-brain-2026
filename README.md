# Second Brain

A local-first, privacy-respecting notetaker you own outright. Capture a thought in one
tap, store it as a plain Markdown file on your own disk, and surface it later with
search, a knowledge graph, and AI. No cloud lock-in, no subscription, no vendor who can
degrade, paywall, or delete your work.

Built with Kotlin Multiplatform and Compose Multiplatform, so one codebase runs on
Android (great on GrapheneOS / AOSP), Desktop, and the Web, with iOS as an optional
target.

> Companion project to the talk **"Build a second brain with AI (and a bit of Kotlin)
> at home."** This repo is the blueprint; you are meant to fork it and build *your*
> version in a weekend.

## Why own it instead of renting it

Most notetaking apps live on someone else's server. That server can analyze your data,
sell it back to you as ads, hide features behind a paywall, redefine what "buy" and
"delete" mean, or shut down and take your work with it.

This project takes the opposite path. It starts with a folder. Inside that folder are
Markdown text files. As long as there are computers, you can open them, move them, copy
them, email them to a friend, or edit them in VS Code, Vim, Obsidian, or Notepad.

- 🔓 **No DRM, no walled garden, no subscription.**
- 📴 **Offline-first.** Capture, storage, search, and the graph all work with no network.
- 📄 **Plain Markdown.** Your notes stay human-readable and tool-agnostic forever.
- 🕵️ **Zero telemetry.** Nothing is tracked or reported anywhere.

## The framework: Capture, Store, Surface

A "second brain" is not one app. It is three decoupled systems in a continuous loop.
You record a thought, it persists durably, it is surfaced later, and that surfacing
sparks the next thought.

### 1. Capture (ultra-low friction)

The goal is to collapse the usual "unlock the phone, find the app, find the note, start
typing" ritual down to two steps: *have a thought* and *have the system record it*.
Capture is reachable from anywhere, not just by tapping an app icon.

- A traditional notetaker app built with Compose Multiplatform.
- Android Home Screen Widgets, Lock Screen Widgets, and Quick Settings Tiles via
  Jetpack Glance.
- The Android Intent API (`ACTION_SEND`, `ACTION_PROCESS_TEXT`) and Deep Links, so
  other apps and the OS can hand text straight into a capture flow.
- On-device speech-to-text dictation via OpenAI Whisper, with no cloud call.
- Optional contextual metadata (timestamp, location, Bluetooth / Wi-Fi / NFC presence)
  written into front-matter, strictly opt-in per signal.

### 2. Store (durable and portable)

The WHERE and HOW of your thoughts, owned by you.

- A file-system-backed **Markdown vault** with `[[wikilinks]]` and `#tags`.
- Shared business logic in pure Kotlin Multiplatform (`commonMain`).
- An optional **derived index** (SQLite + FTS5) for fast lookup. The index is always
  rebuildable from the files and is never the source of truth. The files are.

### 3. Surface (intelligent retrieval and the knowledge graph)

A second brain is only useful if it gives information back. The bar: you can find and
recall exactly the thought that was in your mind.

- **Graph view**: every note is a node, every link an edge, rendered on a Compose
  Canvas.
- **Full-text search** with relevance ranking.
- **Semantic search** via local embeddings, so searching "frequent flyer points" finds
  the note you wrote about "airline loyalty programs".
- **Retrieval-Augmented Generation (RAG)**: ask "what did I learn in California?" and
  get the right notes back, sending only the relevant chunks to an LLM, never the whole
  vault.

## Make it yours

This is *your* notetaker, so the shape is deliberately left open. During planning you
decide which platforms to target, which features matter this weekend (and which do not),
how your vault is organized, and whether the AI layer runs fully locally, through an API,
or not at all. Maybe you skip handwriting. Maybe you want RSS and podcast transcripts
surfaced alongside your notes. Maybe you are writing a book, doing research, or
cataloguing your plants. Bend it to your needs.

## Platforms

| Target  | Status            | Notes                                         |
|---------|-------------------|-----------------------------------------------|
| Android | Primary           | Optimized for GrapheneOS / AOSP               |
| Desktop | Supported         | macOS, Linux, Windows via Compose Multiplatform |
| Web     | Supported         | Compose Multiplatform on WebAssembly          |
| iOS     | Optional          | Supported KMP target, off by default          |

## Honest limits

This is a weekend-scale, single-user, local-first project. Deliberately out of scope:

- No accounts or authentication.
- No proprietary cloud sync or real-time collaborative editing.
- No serious security or encryption layer, so **keep regulated or genuinely sensitive
  data (medical, financial, legal, trade secrets) out of it**.
- No analytics, no in-app purchases, no subscriptions.

The guiding question for a first build is simply: **is it useful?**

## Building

Source code is coming to this repo. It is a standard Kotlin Multiplatform / Gradle
project built with an agentic coding harness; build and run instructions will live here
as the code lands. The full spec that drives development is in
[`CLAUDE.md`](./CLAUDE.md).

## License

MIT
