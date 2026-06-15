# Lucy Verse VRM: Sovereign OS Implementation Plan

The goal is to evolve the Lucy architecture into a true **Virtual Resource Machine (VRM)**—the "Lucy Verse". This establishes a coherent operating system built on Tauri, Rust, and React, replacing the older bridge-heavy stack.

## Finalized Architecture
- **Frontend:** React + Tailwind (NovaShell UI)
- **Commands:** Tauri IPC
- **Core Engine:** Native Rust (Orchestrator, Event Bus, W.E.D.G.I.T, Graph Memory)
- **Runtime Registry:** Centralized tracking for Agents, WASM modules, and Tasks.
- **Terminal:** Embedded first, standalone TUI (`lucy`) second.
- **WASM Runtime:** Real Wasmtime sandbox for execution verification.

---

## Proposed Changes

### Phase 1: Architectural Guardrails & Folder Preparation
- Create the clean `Lucy's_verse_OS_v2` directory.
- Compile all architectural rules, vocabulary guidelines (Emma vs. Lucy), and UI specifications into a `docs/` folder to prevent AI drift during development.

### Phase 2: The NovaShell Desktop & Tauri Foundation
Scaffold the core desktop UI designed to behave like a modern, touch-first Windows environment.

#### `lucy_verse/` (Tauri + Rust + React Project)
- Scaffold the `lucy_verse` application.
- **React Frontend:**
    - Implement the **Global Layout**: Top system bar, Center Workspace, Bottom task rail.
    - Implement **Window Management**: Floating, Docked, and Stacked states.
    - Implement **Swarm Dashboard**: The 4-panel command center (W.A.T.C.H, Task Planner, Cognitive Stream, and W.E.D.G.I.T).
- **Rust Backend (`src-tauri`):**
    - Setup the core daemon structure.
    - Implement the Event Bus and IPC hooks.

### Phase 3: The Runtime Registry
Create a centralized brain to track all system operations so orchestration logic isn't scattered.

#### `src-tauri/src/runtime/`
- `registry.rs`: Global state tracking.
- `process_manager.rs`: OS-level process hooks.
- `module_loader.rs`: WASM payload management.
- `capability_manager.rs`: Permission gates for WASM/Agents.
- `scheduler.rs`: Cognitive loop execution timings.

### Phase 4: Memory V1 to V2 Migration (Graph Engine)
Migrate existing data to the new Semantic Spacetime graph architecture without data loss.

#### `src-tauri/src/memory/`
- Set up the **Memory V2** storage engine using an embedded SQLite-Graph database.
- Define the POLE+O and Semantic Spacetime (`NEAR`, `LEADS_TO`, `CONTAINS`) schema.
- **Migration Pipeline:** Create a parser to read current Lucy memory files (Memory V1) and map flat structures into relationship pairs (e.g., `(User) LIKES (FiveM)`).

### Phase 5: W.E.D.G.I.T (Drag & Drop + Wasmtime Execution)
Implement the central dashboard app function for managing incoming files, autonomous workflows, and sandboxed tasks.

#### `src-tauri/src/wedgit/`
- **Phase 5A: OS Drag & Drop Pipeline:** 
    - Intercept OS file drops in Tauri/Electron, stream to Rust, classify the file (MIME/Content), and either route automatically to an Agent or trigger the "Ask Lucy" UI modal.
- **Phase 5B: Proof of Execution:**
    - Integrate the `wasmtime` Rust crate.
    - Implement a bare-metal WASM execution sandbox (No network, no filesystem, no host access).
    - Expose the API to load a module, verify the permit (via `capability_manager`), execute the payload, and fire a `WasmExecuted` event to the Cognitive Stream.

### Phase 6: Terminal Integration
Unify command-line operations with the visual dashboard using a shared Event Bus.

- **Phase 6A: Embedded Terminal:** Integrate a terminal emulator component directly inside the React NovaShell dashboard.
- **Phase 6B: Standalone TUI:** Build a standalone Rust CLI binary (`lucy`) utilizing the **Ratatui** framework. Commands like `lucy swarm status` will push `SwarmStatusRequested` to the shared event bus.
