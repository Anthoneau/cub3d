# cub3D

`cub3D` is the second graphics project of the 42 curriculum and consists in recreating a **very simple 3D game engine**, inspired by the original *Wolfenstein 3D*.

While often described as a game project, the real objective of `cub3D` is to understand how a **rendering engine** works: raycasting, player movement, projection, input handling, and real-time rendering.

---

## Project Overview

The program renders a first-person view of a 2D map using **raycasting**, creating the illusion of a 3D environment.

The player can move inside the map, look around, and interact with the environment in real time.  
Textures, lighting, and perspective are all handled manually.

This project applies concepts already encountered in previous projects, such as timing, input handling, and state management, to a real-time graphical context.

---

## Raycasting & Wolfenstein 3D

Raycasting is the original technique used to simulate 3D environments from a 2D representation of the world.

In *Wolfenstein 3D* (1992), the world is represented as a 2D grid:
- each cell is either empty or a wall
- the player has a position and a viewing direction

The world itself is not 3D: depth is an illusion created entirely through distance-based projection.

For each vertical slice of the screen:
1. A ray is cast from the player’s position
2. The ray advances through the grid until it hits a wall
3. The distance to the wall determines the height of the slice
4. The wall slice is drawn accordingly

This simple idea is enough to produce a convincing 3D illusion.

---

## Raycasting Implementation (DDA)

This project uses the **DDA (Digital Differential Analyzer)** algorithm to traverse the map grid efficiently.

DDA works by:
- stepping from one grid cell to the next
- comparing distances to the next vertical and horizontal grid boundaries
- stopping as soon as a wall is encountered

This method is fast, deterministic, and perfectly suited for grid-based worlds.

---

## Rendering Pipeline

At a high level, each frame follows this pipeline:

```
Input handling
   ↓
Player state update
   ↓
Raycasting (DDA)
   ↓
Wall projection
   ↓
Shading & effects
   ↓
Final rendering
```

The entire frame is recomputed every iteration to allow smooth movement and rotation.

---

## Player & Camera Controls

The player can:
- Move forward and backward
- Strafe left and right
- Rotate using the keyboard or the mouse
- Look up and down

Movement and rotation are handled independently, allowing smooth and responsive controls.

Player movement includes wall collision detection.
The player cannot walk through walls, and all movements are validated against the map grid before being applied.

---

## Bonus Features

A significant number of bonus features were implemented to extend the basic engine:

- Dynamic minimap that follows the player
- Minimap display modes (square, circular, hidden)
- Jump mechanic
- Crouch mechanic (reduced height and movement speed)
- Sprint / running
- Mouse-based camera rotation
- Vertical camera movement (look up / down)
- Camera bobbing while moving
- Animated weapon (visual only)
- Dynamic lighting:
  - the player acts as a light source
  - walls become darker as distance increases
- FPS counter displayed in the terminal

These features required extending the core raycasting logic and carefully managing player state and rendering timing.

---

## Input Handling

Keyboard and mouse inputs are processed in real time to update the player’s position, orientation, and state.

The engine supports simultaneous inputs (e.g. moving while rotating), contributing to a fluid gameplay experience.

---

## Performance & Fluidity

The rendering loop is optimized to maintain a smooth frame rate.

Raycasting, movement, and rendering are tightly coupled to ensure consistent performance even with additional visual effects enabled.

---

## Why This Project Matters

`cub3D` occupies a particular place in the 42 curriculum.

Coming after projects like `minishell`, it is not the most complex nor the most demanding one from a system perspective. Instead, it offers a different kind of challenge: the opportunity to explore graphics programming and real-time rendering in a relatively free environment.

`cub3D` brings together:
- mathematics
- graphics programming
- real-time constraints
- system-level input handling
- engine architecture

Because the mandatory scope leaves room for creativity, I chose to push the project further by implementing numerous bonus features, turning it into a more complete and interesting experience.

---

## Usage

### Mandatory version

```bash
make
./cub3D maps/example.cub
```

### Bonus version (recommended)

```bash
make bonus
./cub3D maps/example.cub
```

The bonus version includes extended gameplay mechanics and visual features.

---

## Author

**Anthony Goldberg** ***agoldber***

42 student – core curriculum completed