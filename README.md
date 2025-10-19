# Awesome Local-First [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of **local-first software**, resources, and development tools.  
Local-first software prioritizes **data ownership**, **offline functionality**, and **synchronization** — keeping user data primarily on their devices.

---

## 🧩 Core Resources

### Foundational Articles
- [Local-First Software](https://www.inkandswitch.com/local-first/) – The original article introducing local-first principles by Ink & Switch  
- [Building Local-First Software](https://martin.kleppmann.com/papers/local-first.pdf) – Academic paper on local-first principles  
- [Why Haven’t Local-First Apps Taken Off? (2025)](https://marcobambini.com/posts/local-first-challenges) – Examines distributed complexity and adoption barriers  

### Architecture & Implementation
- [Are Sync Engines the Future of Web Applications?](https://dev.to/isaachagoel/are-sync-engines-the-future-of-web-applications-1bbi) – Deep dive into sync engine design  
- [Building Data-Centric Apps with a Reactive Relational Database](https://riffle.systems/essays/prelude) – Reactive DB patterns by Riffle  
- [End-to-End Encryption in the Browser](https://blog.excalidraw.com/end-to-end-encryption/) – E2E encryption technical breakdown  
- [Designing Data Structures for Collaborative Apps](https://mattweidner.com/2022/02/10/collaborative-data-design.html) – Practical guide to CRDT structure design  
- [Beehive (Ink & Switch 2024)](https://www.inkandswitch.com/beehive/) – Decentralized access control and convergent capabilities  
- [Ossa Protocol (2025)](https://ossa.dev) – Open universal sync protocol for local-first interoperability  

### Performance & UX
- [Why Superhuman Is Built for Speed](https://blog.superhuman.com/superhuman-is-built-for-speed/) – Applying the 100 ms rule  
- [Why Local-First Apps Feel Instant](https://linear.app/blog/local-first-architecture) – Linear’s IndexedDB-first architecture  
- [A Gentle Introduction to CRDTs](https://vlcn.io/blog/gentle-intro-to-crdts.html) – Beginner-friendly CRDT explanation  

### Video Content
- [What Is Local First?](https://www.youtube.com/watch?v=KrPsyr8Ig6M) – Overview by Peter van Hardenberg  
- [Local-First Development](https://www.youtube.com/watch?v=NMq0vncHJvU) – Introduction to local-first concepts  
- [Local-First Conf 2024](https://www.youtube.com/@localfirstconf/videos) – Full conference playlist  
- [SyncConf 2025 (Preview)](https://localfirstconf.com/syncconf2025) – Conference focused on synchronization  

---

## ⚙️ Development Tools & Libraries

### Database Solutions
- [Electric SQL](https://electric-sql.com/) – Sync Postgres data into local apps with offline support  
- [WatermelonDB](https://watermelondb.dev) – Reactive DB for React / React Native  
- [Fireproof](https://use-fireproof.com/) – Browser-native local-first database  
- [Evolu](https://www.evolu.dev/) – Type-safe offline-first database with sync  
- [Dexie.js](https://dexie.org/) – IndexedDB wrapper with sync  
- [TanStack DB (2025)](https://tanstack.com/db) – Reactive local SQL-like DB with optimistic mutations  
- [LiveStore (2024)](https://livestore.dev) – Event-sourced local-first framework using in-memory SQLite  
- [Triplit](https://triplit.dev) – Full-stack sync engine + database (acquired by Supabase 2025)  
- [InstantDB (2024)](https://instantdb.dev) – Firebase-style backend with offline & real-time sync  
- [Zero (2024)](https://zero.rocicorp.dev) – Reactive sync engine from the Replicache team  
- [RxDB](https://rxdb.info) – Reactive NoSQL DB with replication, encryption, multi-tab  
- [PowerSync](https://www.powersync.com) – Offline-first sync engine for mobile/web  
- [Y-Sweet](https://jamsocket.com/y-sweet) – Hosted backend for Yjs sync  
- [Turso Sync (2025)](https://turso.tech) – Sync local SQLite with edge-hosted SQLite  

### State Management & Sync
- [Legend State](https://github.com/LegendApp/legend-state) – Reactive state with persistence  
- [Replicache](https://replicache.dev) – Client-side sync with conflict resolution  
- [PowerSync](https://www.powersync.com) – Enterprise-scale offline sync  
- [Y-Sweet](https://jamsocket.com/y-sweet) – CRDT backend service  
- [Tinybase](https://github.com/tinyplex/tinybase) – Reactive data store & sync engine  

### CRDT Libraries
- [Automerge 2.0](https://automerge.org) – Fast binary format & WASM “Automerge Anywhere”  
- [Yjs](https://docs.yjs.dev/) – High-performance CRDT framework  
- [Loro](https://loro.dev/) – JSON and rich-text CRDT  
- [Collabs](https://collabs.readthedocs.io/en/latest/) – Composable CRDTs from CMU  

---

## 💡 Real-World Examples

### Case Studies
- [Figma’s Multiplayer Technology](https://www.figma.com/blog/how-figmas-multiplayer-technology-works/) – Real-time collaboration internals  
- [Notion’s WASM SQLite](https://www.notion.com/blog/how-we-sped-up-notion-in-the-browser-with-wasm-sqlite) – Browser local-DB performance  
- [Trello’s Offline Architecture](https://www.atlassian.com/blog/atlassian-engineering/sync-architecture) – Offline support patterns  
- [Linear’s Local-First Architecture (2025)](https://linear.app/blog/local-first-architecture) – Instant UX through IndexedDB-first design  
- [Logseq & Obsidian](https://logseq.com) – Markdown-based offline knowledge tools  

### Example Applications
- [Excalidraw](https://excalidraw.com) – Collaborative drawing  
- [Actual](https://actualbudget.com) – Local-first budgeting  
- [Bangle.io](https://bangle.io) – Local-first notes  
- [Finbodhi (2025)](https://finbodhi.com) – Encrypted personal-finance app  
- [Timelinize (2025)](https://timelinize.app) – Offline timeline journaling  
- [Hyperdrift / Biscuits (2025)](https://hyperdrift.dev) – P2P family productivity apps  
- [Local-First Podcast Player (2025)](https://github.com/localfirst-podcast) – Offline PWA demo  

### Learning Resources
- [SQLite in Vue Guide](https://alexop.dev/posts/sqlite-vue3-offline-first-web-apps-guide/) – Building offline-first Vue apps  
- [An Interactive Intro to CRDTs](https://jakelazaroff.com/words/an-interactive-intro-to-crdts/) – Hands-on tutorial  
- [Operational Transformation Visualization](https://operational-transformation.github.io/) – Interactive OT demo  
- [CRDT Tutorials](https://github.com/siliconjungle/crdt-tutorials) – Practical examples  
- [TinyRooms](https://github.com/tinyplex/tinyrooms) – Multiplayer game using local-first  
- [RxDB Blog – Why Local-First Is the Future](https://rxdb.info/articles/why-local-first.html) – Deep dive  

---

## 🌍 Community

### Stay Connected
- [Local-First Web](https://localfirstweb.dev/) – Community hub  
- [localfirst.fm](https://www.localfirst.fm/) – Developer podcast  
- [Local-First Discord](https://discord.com/invite/ZRrwZxn4rW) – Active discussion server  
- [Local-First News](https://www.localfirstnews.com/) – Weekly newsletter with releases & meetups  
- [LoFi Meetups (2024-25)](https://localfirstweb.dev/meetups) – Monthly online community events  
- [Braid IETF WG](https://braid.org) – Working group for sync protocols  

---

## 🎤 Conferences & Talks
- [Local-First Conf 2024 Videos](https://www.youtube.com/@localfirstconf/videos) – Sessions by Kleppmann, Artman (Linear), etc.  
- [LoFi / 28 Meetup (2025)](https://localfirstnews.com/lofi28) – Dexie, Replication 3 Ways, Legend State performance talk  
- [SyncConf 2025 Preview](https://localfirstconf.com/syncconf2025) – Dedicated sync-tech event  

---

## 🤝 Contributing
Pull requests welcome!  
Add tools, libraries, or case studies that advance **local-first**, **offline-first**, or **sync-centric** development.

---

## 🪪 License
[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0)
