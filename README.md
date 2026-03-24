# Godouni

<img width="100" height="100" alt="GodouniLogo" src="https://github.com/user-attachments/assets/1a92ce67-62c7-4554-882d-b15dfd99bc79" />

Pronounced "Go-doe-you-knee"

**A Godot fork that brings Unity-style workflows to Godot engine.**

<img width="444" height="360" alt="Screenshot 2026-03-23 194109" src="https://github.com/user-attachments/assets/0117b6fc-8e50-4973-aea3-8b8050c3c416" />
<img width="95" height="370" alt="Screenshot 2026-03-23 224452" src="https://github.com/user-attachments/assets/8f8b1ab8-c894-4322-8fee-6c3dcaff4b56" />
<img width="397" height="158" alt="Screenshot 2026-03-23 224248" src="https://github.com/user-attachments/assets/bba33b20-85b5-4f64-a0a4-d1e054e61456" />
<img width="280" height="165" alt="image" src="https://github.com/user-attachments/assets/863655c8-7d31-4bd1-aee3-9d03353dc400" />
<img width="333" height="70" alt="Screenshot 2026-03-23 224521" src="https://github.com/user-attachments/assets/592766c8-0e68-4a81-85a5-72714a588f56" />

### Why?

Just for shits and giggles

Godouni adds a GameObject + Component workflow on top of Godot's node system, making the engine feel more familiar to developers coming from Unity without changing any existing Godot functionality.

## What's Different?

### GameObject Node

A new `GameObject` (3D) and `GameObject2D` node type. They act as containers whose children are treated as **Components**.

### Component Inspector

When you select a GameObject, the inspector shows a dedicated **Components** panel:

- Lists all child nodes as components with their icons and names
- **Fold/unfold** each component to show or hide its properties
- **Nested display** - components that are auto-organized under other components show up indented to reflect the hierarchy
- **Delete button** on each component to remove it
- **"Add Component" button** opens the node picker to attach new components
- **"Add Script" button** lets you attach a script file as a component

### Auto-Organizing Components

When you add components, they automatically arrange themselves into the correct Godot hierarchy:

- **CollisionShape3D / CollisionPolygon3D** — auto-nests under the first physics body (RigidBody3D, StaticBody3D, CharacterBody3D, Area3D)
- **MeshInstance3D** — auto-nests under the first physics body
- **VehicleWheel3D** — auto-nests under VehicleBody3D
- **CollisionShape2D / CollisionPolygon2D** — auto-nests under the first 2D physics body
- **Sprite2D** — auto-nests under the first 2D physics body

It also works in reverse, when you add a **physics body** to a GameObject that already has loose collision shapes or meshes, those existing components get reparented under the new body automatically.

### Hierarchy Warnings

The inspector shows yellow warnings when components need attention:

- Physics body has no collision shape
- Collision shape is loose (not under a physics body)
- VehicleWheel3D without a VehicleBody3D

### Right-Click Create Menu

Right-clicking in the scene tree gives you Unity-style quick create options:

- **Create Empty** — empty GameObject
- **Create Empty 2D** — empty GameObject2D
- **3D Object** — Cube, Sphere, Capsule, Cylinder, Plane, Quad (creates a GameObject with a MeshInstance3D and primitive mesh already attached)
- **Light** — Directional Light, Point Light, Spot Light
- **Camera** — GameObject with Camera3D
- **Audio Source** — GameObject with AudioStreamPlayer3D
- **Particle System** — GameObject with CPUParticles3D

### How It Works

Under the hood, components are just regular Godot nodes, children of the GameObject. The inspector provides a Unity-like UI layer on top of Godot's existing parent/child system. Everything is fully compatible with standard Godot features like signals, scenes, and GDScript.

```
GameObject (selected in scene tree)
  +-- RigidBody3D           <-- component
  |     +-- MeshInstance3D   <-- auto-organized under the body
  |     +-- CollisionShape3D <-- auto-organized under the body
  +-- MyScript               <-- script component
```

### What's planned?

Don't expect this to be maintained along side actual Godot but I would like to add web build support when that is added officially to .net Godot.

## Building

#### C# Version
```bash
scons platform=windows target=editor module_mono_enabled=yes -j12
```

#### GDScript Version:
```bash
scons platform=windows target=editor -j$(nproc)
```

Replace `windows` with `linuxbsd` or `macos` as needed. See the [Godot docs](https://docs.godotengine.org/en/stable/contributing/development/compiling/) for full build instructions.

## License

Same as Godot Engine — [MIT License](LICENSE.txt).



