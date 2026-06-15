# NovaShell UI & Swarm Dashboard Spec

**DO NOT DEVIATE FROM THIS UI LAYOUT WITHOUT EXPLICIT USER APPROVAL.**

## The 4-Panel "NovaShell" Layout
The desktop UI is an advanced, touch-first Windows-style environment built in React. The core dashboard is divided into 4 permanent panels:

### 1. Left Column: Event System (W.A.T.C.H Battalion)
**W.A.T.C.H = Windows Awareness & Task Coordination Hub**
*Responsibilities:*
- Monitor OS
- Monitor Apps
- Monitor Browser
- Monitor Network
- Monitor User Activity
- Monitor Lucy Agents
- Detect new tasks
- Publish events (via the Event Bus Live Stream, filtered by severity).

### 2. Center-Left Column: Task & Planning
- Task Intake Queue (Pending tasks).
- Planner View (Goal interpretation, confidence scores).
- Decomposition Tree (Atomic subtasks).

### 3. Center-Right Column: Cognitive Stream (OS Thought Stream)
- The OS equivalent of Windows Event Viewer + Task Manager + AI Thought Stream.
- A live, vertical chronological feed of cognitive actions:
  - `[Emma] Approved task`
  - `[Swarm] Created plan`
  - `[Lucy] Updated memory graph`
  - `[WEDGIT] Executed WASM payload`
  - `[Lucy] Result stored`

### 4. Right Column: W.E.D.G.I.T (Workflow Execution, Decision, Governance & Intelligent Tasks)
- Swarm & Agent Assignment Status.
- **WASM Execution Visualizer:** Monitors execution states (pending -> denied -> allowed -> executed).
- **Drag & Drop Ingestion Pipeline:** W.E.D.G.I.T manages dropped files via the Tauri/Electron boundary.
  - User drops a file -> W.E.D.G.I.T classifies it (MIME, Content, Safety) -> Triggers "Ask Lucy" modal or auto-routes to Agents (Vision, Audio, Document).
- Blackboard & Memory Live View.

## Universal Event Bus Integration
- The Dashboard and the Standalone Terminal (`lucy_cli`) MUST operate on the exact same Event Bus.
- When `lucy swarm status` is run in the PowerShell terminal, it MUST push a `SwarmStatusRequested` event to the bus, which will instantly reflect in the NovaShell **Cognitive Stream** and **W.A.T.C.H** panels.
