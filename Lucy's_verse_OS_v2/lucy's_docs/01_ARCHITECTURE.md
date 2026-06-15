# Lucy Verse OS: System Architecture

**Version:** 2.0 (Sovereign Rust Edition)
**DO NOT DEVIATE FROM THIS ARCHITECTURE WITHOUT EXPLICIT USER APPROVAL.**

## Core Principles
1. **Sovereignty First:** The system must run entirely offline, securely, and privately. No arbitrary cloud dependencies.
2. **Coherent OS vs. Bridge Sprawl:** Avoid creating endless Python-to-Node bridges. The core engine is Native Rust.
3. **Graph-Linked Memory:** Flat memory is deprecated. Use Semantic Spacetime graphs (SQLite-Graph or LadybugDB).

## System Stack

```text
React UI (NovaShell)
    │
Tauri Commands (IPC)
    │
Rust Core (src-tauri)
    │
────────────────────────────────────────
│                                      │
│  Memory Engine (SQLite Graph)        │
│  Runtime Registry                    │
│  W.E.D.G.I.T (WASM Execution)        │
│  Event Bus                           │
│                                      │
────────────────────────────────────────
```

## Directory Structure Enforcement
All future development must adhere to this structure:
```text
Lucy's_verse_OS_v2/
├── docs/
│   ├── 01_ARCHITECTURE.md
│   ├── 02_VOCABULARY.md
│   ├── 03_UI_UX_SPEC.md
│   └── 04_RUNTIME_REGISTRY.md
├── lucy_verse/                # Main Tauri application root
│   ├── src/                   # React frontend (NovaShell)
│   ├── src-tauri/             # Rust backend
│   │   ├── src/
│   │   │   ├── memory/        # Graph DB implementations
│   │   │   ├── runtime/       # Runtime Registry (tracking logic)
│   │   │   ├── wedgit/        # Wasmtime sandbox and capabilities
│   │   │   └── main.rs        # Tauri entrypoint
├── lucy_cli/                  # Standalone Ratatui Terminal (Phase 6)
```
