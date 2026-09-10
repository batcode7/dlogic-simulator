# DLogic — Digital Logic Simulator

**DLogic** is a browser-based digital logic design and simulation environment built for education. It combines an interactive schematic editor, configurable digital components, live simulation, truth-table analysis, diagnostics, project files, and advanced circuit-editing tools.

**Current version:** v0.9.7  
**Purpose:** Digital Logic Design teaching, laboratory work, practice, and circuit analysis.

---

## Features

### Schematic Editor

- Drag-and-drop component placement
- Direct pin-to-pin connections
- Orthogonal/Manhattan wire routing with 90° corners
- Automatic shared fan-out trunks
- Editable wire bend points
- Explicit junction support
- Move, rotate, and resize components
- Multi-selection and marquee selection
- Group / ungroup components
- Group move, rotation, and scaling
- Copy, paste, and duplicate
- Undo / redo
- Zoom in/out and Fit View
- Optional minimap
- Focus/fullscreen workspace mode
- Select and delete components or wires
- Hide/show Inspector and bottom panel

### Wire Editing

Wires remain editable after they are created.

- **Click a wire** — select it
- **Drag a bend point** — reshape the selected wire
- **Double-click a wire** — add a bend point
- **Double-click a bend point** — remove it
- **Shift + Double-click a wire** — insert an explicit junction
- Wire routing snaps to a 10 px grid
- Manual waypoints are saved with the project
- Multiple connections from one output automatically share a source trunk
- Shared fan-out trunk position can be adjusted
- Branch points are visually indicated
- Manual routing overrides automatic fan-out routing when appropriate

---

## Component Library

### Input / Output

- **Input Toggle** — manually switches between logic 0 and 1
- **LogicState (Right)** — Proteus-inspired interactive logic-state source
- **LogicState (Left)** — left-facing LogicState
- **LogicProbe** — displays the current logic value
- **Bulb** — visual output indicator

### Logic Gates

- AND
- OR
- NOT
- NAND
- NOR
- XOR
- XNOR

Gate components use standard digital schematic symbols.

### Combinational Circuits

- Half Adder
- Full Adder
- Parallel Adder
- Encoder
- Decoder
- Multiplexer (MUX)
- Demultiplexer (DEMUX)

#### Parallel Adder

- Configurable from **4 to 32 bits**
- `A(n-1)...A0` inputs
- `B(n-1)...B0` inputs
- `S(n-1)...S0` outputs
- `Cin`
- `Cout`
- Component body automatically grows with bit width

#### MUX / DEMUX

- Configurable line count
- Selector pins generated automatically
- Selector ordering begins with `S0` as the least-significant selector bit
- Component size grows according to configuration

#### Encoder / Decoder

- Configurable sizes
- Pins generated automatically
- Encoder inputs use `I0...`
- Decoder outputs use `O0...`
- MSB/LSB indications are displayed where appropriate

### Sequential / Storage

#### Binary Cell

A simple one-bit storage component.

- **Select** — top
- **R/W** — bottom
- **Data In** — left
- **Data Out** — right
- Stored `0` or `1` is displayed inside the component

The architecture is ready for additional latches, flip-flops, registers, counters, and other sequential circuits.

---

## Logic Signals

The custom simulation engine supports four digital signal states:

| Signal | Meaning |
|---|---|
| `0` | Logic LOW |
| `1` | Logic HIGH |
| `X` | Unknown / unresolved |
| `Z` | High impedance |

---

## Simulation

Use **Run** to start simulation and **Stop** to return to circuit editing.

While simulation is running:

- Structural circuit editing is locked
- Components cannot be moved, resized, deleted, rotated, grouped, or rewired
- Component properties cannot be changed
- Interactive inputs remain usable
- Logic signals propagate through the circuit
- Stateful components can update their internal state

This prevents accidental circuit modification while a design is being tested.

### Interactive Inputs

**Edit mode**

- Single-click selects
- Drag moves the component
- Double-click toggles the logic value

**Run mode**

- Single-click toggles the interactive input value

---

## Bottom Analysis Panel

The bottom panel contains three teaching/analysis tools:

### Simulation Log

Displays simulation activity and signal-related information while testing a circuit.

### Truth Table

Provides a dedicated truth-table workspace for Digital Logic Design analysis.

### Diagnostics

Helps identify circuit problems such as:

- Floating inputs
- Invalid pin connections
- Conflicting or multiple drivers
- Missing component plugins
- Simulation non-convergence

The entire bottom panel can be hidden to maximize canvas space.

---

## Inspector

The Inspector configures the currently selected component.

Depending on the component, it can be used to:

- Change component properties
- Configure bit width or line count
- Change the visible component name
- Edit visible pin labels

The Inspector can be hidden when more canvas space is required.

### Custom Component Names

Default display names such as `LS1`, `PA1`, `MUX1`, and `FA1` can be changed.

The display name may also be blank if no name should be shown.

Changing the display name does **not** alter the stable internal component ID.

### Custom Pin Labels

Pin labels can be visually renamed.

Custom pin labels do not alter the underlying electrical pin IDs, so changing a displayed label does not break circuit connections.

---

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + A` | Select all |
| `Ctrl + C` | Copy selection |
| `Ctrl + V` | Paste |
| `Ctrl + D` | Duplicate selection |
| `Ctrl + G` | Group selected components |
| `Ctrl + U` | Ungroup |
| `R` | Rotate selected component(s) 90° |
| `Delete` / `Backspace` | Delete selected component(s) or wire |
| `Esc` | Clear selection or exit Focus Mode |
| `Ctrl` / `Shift` / `Cmd` + Click | Add/remove an item from the current selection |
| `Shift` + Drag on empty canvas | Marquee selection |
| Left-drag empty canvas | Pan the canvas |

---

## Mouse Controls

### Components

| Action | Result |
|---|---|
| Single-click | Select component |
| Drag | Move component |
| Double-click interactive input in Edit mode | Toggle input |
| Single-click interactive input in Run mode | Toggle input |
| Click empty canvas | Clear selection |

### Wires

| Action | Result |
|---|---|
| Click wire | Select wire |
| Drag bend point | Change wire route |
| Double-click wire | Add bend point |
| Double-click bend point | Remove bend point |
| `Shift + Double-click` wire | Insert explicit junction |

---

## Toolbar

The main toolbar uses compact symbol-only controls with tooltips.

Available actions include:

- New
- Open
- Save
- Save As
- Undo
- Redo
- Copy
- Paste
- Run
- Stop
- Select All
- Group
- Ungroup
- Duplicate
- Rotate
- Decrease Size
- Increase Size
- Delete
- Show/Hide Inspector
- Show/Hide Bottom Panel

---

## Focus Mode

Focus Mode maximizes the schematic workspace while keeping the editor mounted and active.

Focus-mode canvas controls include:

- Zoom
- Fit View
- Run
- Stop
- Exit Focus Mode
- Minimap

Press `Esc` to exit Focus Mode.

---

## Project Files

DLogic projects use the **`.dlogic`** extension.

The format stores circuit information including:

- Components
- Component type/plugin information
- Positions
- Sizes
- Rotation
- Groups
- Display labels
- Properties
- Component state
- Connections
- Manual wire waypoints
- Wire labels
- Shared fan-out routing information

### Unsaved Changes

An asterisk beside the filename indicates unsaved work:

```text
my-circuit.dlogic *
```

After a successful save, the `*` disappears.

New projects begin as:

```text
untitled.dlogic *
```

---

## Autosave and Recovery

DLogic keeps a local recovery snapshot to protect work if the browser is unexpectedly closed or reloaded.

If recoverable work exists, the simulator can offer **Recover** or **Discard**.

The recovery system does not silently overwrite the user's `.dlogic` project file.

---

## Plugin Architecture

DLogic uses a modular, plug-and-play component architecture.

A component plugin can define its own:

- Pins
- Visual representation
- Properties
- Simulation behavior
- Internal state
- Configuration rules

The simulation engine does not hard-code individual component names. Complex components can dynamically generate pins from their properties.

This allows the simulator to grow with new gates, combinational circuits, sequential circuits, memory elements, and educational components without redesigning the core simulation engine.

---

## Edit Mode vs Run Mode

### Edit Mode

You can:

- Add components
- Move and resize components
- Rotate components
- Connect/disconnect wires
- Edit wire routes
- Delete elements
- Group/ungroup components
- Change properties and labels

### Run Mode

Structural editing is locked, while interactive inputs remain available for circuit testing.

---


## Educational Purpose

DLogic is designed as an educational Digital Logic Design environment. Its goal is to make schematic construction, simulation, debugging, and analysis accessible from one interface while retaining familiar digital-circuit conventions.

---

## Author

**Partha Bhoumik**

Digital Logic Simulator  
Built for educational purpose.

---

## Version

**DLogic v0.9.7**

© 2026 Partha Bhoumik
