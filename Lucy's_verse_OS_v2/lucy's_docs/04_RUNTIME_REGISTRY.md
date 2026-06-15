# Runtime Registry Specifications

**DO NOT DEVIATE FROM THIS STRUCTURE. IT IS CRITICAL FOR OS COHESION.**

## Purpose
The architecture must have a dedicated Runtime Registry in the Rust backend to prevent orchestration logic from scattering across subsystems. This serves as the centralized tracking brain for the OS.

## Directory Layout
Located at: `Lucy's_verse_OS_v2/lucy_verse/src-tauri/src/runtime/`

### Required Modules
1. `registry.rs`
   - **Role:** Global state tracking. Maintains the master lists of all known entities.
   - **Tracks:** Active Agents, loaded WASM Modules, open TUI Sessions, active Tasks, queued Memory Jobs.
2. `process_manager.rs`
   - **Role:** OS-level process hooks and management.
3. `module_loader.rs`
   - **Role:** Loading, verifying, and caching WASM payloads before passing them to the Wasmtime sandbox.
4. `capability_manager.rs`
   - **Role:** The SafeGuard. Explicitly grants or denies permissions (e.g., `filesystem.read`, `network.http`) to WASM modules based on agent privileges.
5. `scheduler.rs`
   - **Role:** The cognitive loop timing engine. Ensures W.A.T.C.H events are processed and Swarm loops run at correct intervals.
