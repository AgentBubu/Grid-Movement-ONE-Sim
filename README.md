# GridCrowdMovement

This class implements a custom movement model for the ONE simulator, where nodes move between a set of "areas" arranged in a grid, with special behavior for "home" areas and a "gathering place".

## Overview

- **Areas:** There are 12 areas: 11 "home" areas (numbered 1–11) and 1 "gathering place" (area 12).
- **Grid Layout:** The grid is 4 columns by 3 rows. Each area is mapped to a cell in the grid.
- **Movement Logic:**
  - Each node is assigned a random home area (1–11) at initialization.
  - Nodes start at their home area.
  - At each movement step, the next area is chosen probabilistically:
    - From home: 80% chance to go to the gathering place, 20% to another home.
    - From gathering place: 90% chance to return home, 10% to another home.
    - From other homes: 90% chance to return home, 10% to a different home (not current or home).
- **Waypoints:** Each move is a direct path from the current location to the next area.

## Key Methods

- `getInitialLocation()`: Assigns a home area and returns its coordinates.
- `getPath()`: Generates a path to the next area based on the movement logic.
- `chooseArea()`: Implements the probabilistic area selection.
- `getAreaCoord(int area)`: Maps an area number to a random coordinate within its grid cell.

## Usage

This class is intended to be used as a movement model in the ONE simulator. To use it, specify `movement.GridCrowdMovement` as the movement model in your scenario settings.

## Example

```java
Settings settings = ...; // your simulation settings
MovementModel model = new GridCrowdMovement(settings);
```

## File

- [`src/movement/GridCrowdMovement.java`](src/movement/GridCrowdMovement.java)
