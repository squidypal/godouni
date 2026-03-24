# Goduni
<img width="100" height="100" alt="GodouniLogo" src="https://github.com/user-attachments/assets/1a92ce67-62c7-4554-882d-b15dfd99bc79" />

**A Godot fork that brings Unity-style workflows to Godot engine.**

### Why?
Just for shits and giggles

Goduni adds a GameObject + Component workflow on top of Godot's node system, making the engine feel more familiar to developers coming from Unity — without changing any existing Godot functionality.

## What's Different?

### GameObject Node
A new `GameObject` node type available in the Create Node dialog. It acts as a container whose children are treated as **Components**.

### Component Inspector
When you select a GameObject, the inspector shows a dedicated **Components** panel:

- Lists all child nodes as components with their icons and names
- **Drag-to-reorder** components to control processing order
- **Click a component** to inspect its properties
- **"Add Component" button** opens the node picker to attach new components

### How It Works

Under the hood, components are just regular Godot nodes, children of the GameObject. The inspector provides a Unity-like UI layer on top of Godot's existing parent/child system. Everything is fully compatible with standard Godot features like signals, scenes, and GDScript.

```
GameObject (selected in scene tree)
  +-- Sprite2D        <-- shown as "component" in inspector
  +-- CollisionShape2D
  +-- RigidBody2D
  +-- MyScript
```

## Building

```bash
scons platform=windows target=editor -j$(nproc)
```

Replace `windows` with `linuxbsd` or `macos` as needed. See the [Godot docs](https://docs.godotengine.org/en/stable/contributing/development/compiling/) for full build instructions.

## Changes from Upstream Godot

| File | Change |
|------|--------|
| `scene/main/game_object.h/cpp` | New `GameObject` node class |
| `editor/inspector/game_object_editor_plugin.h/cpp` | Inspector plugin with component list UI |
| `editor/icons/GameObject.svg` | Cube icon for the node |
| `scene/register_scene_types.cpp` | Registers `GameObject` in ClassDB |
| `editor/register_editor_types.cpp` | Registers the editor plugin |

## License

Same as Godot Engine — [MIT License](LICENSE.txt).
