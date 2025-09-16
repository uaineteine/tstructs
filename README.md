# tstructs

Tile map data structures for 2D and 3D worlds.

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0) ![Version 1.1.1](https://img.shields.io/badge/version-1.1.1-brightgreen) [![Lint Check](https://github.com/uaineteine/tstructs/actions/workflows/lint_check.yaml/badge.svg)](https://github.com/uaineteine/tstructs/actions/workflows/lint_check.yaml)

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Module Information](#module-information)
- [Installation](#installation)
- [Usage](#usage)
- [API Reference](#api-reference)
	- [Coordinate](#coordinate)
	- [Region](#region)
	- [ChunkedRegion](#chunkedregion)
	- [Cell](#cell)
	- [Group](#group)
	- [Properties](#properties)
- [Testing](#testing)
- [License](#license)

## Overview
`tstructs` is a Python package providing foundational data structures for representing and manipulating tile maps in both 2D and 3D environments. It is designed for use in games, simulations, and applications that require efficient spatial organization of map data.

## Features
- **Coordinate**: Immutable tuple subclass for 2D/3D coordinates with convenient accessors.
- **Region**: Represents a square 3D region in a tile map, with properties for area, volume, and bounds checking.
- **ChunkedRegion**: Extends `Region` to support chunking, allowing subdivision of regions into smaller, manageable chunks.

## Module Information
- **Name**: tstructs
- **Version**: 1.1
- **Description**: Tile map data structures for 2D and 3D worlds.

## Installation
This package is intended for use as part of a larger project. To use it directly or install it as a package.

```basg
# Example pip install
pip install tstructs
```

```bash
# Example: Add to PYTHONPATH
export PYTHONPATH="$PYTHONPATH:/path/to/install/tstructs"
```

## Usage
Import the classes you need:

```python
from tstructs import Coordinate, Region, ChunkedRegion, Cell, Group, Properties

# 2D coordinate
c2 = Coordinate(1, 2)

# 3D coordinate
c3 = Coordinate(1, 2, 3)

# Create a region
region = Region(region_x=0, region_y=0, region_size=16, region_location=Coordinate(0, 0))

# Create a chunked region
chunked = ChunkedRegion(region_x=0, region_y=0, region_size=16, chunk_size=4, region_location=Coordinate(0, 0))

# Create a cell
cell = Cell(coord=Coordinate(1, 2), value=5)

# Create a group of cells
group = Group([cell])

# Create and use properties
props = Properties({'walkable': True, 'cost': 1})
is_walkable = props['walkable']
```

## API Reference

### Coordinate
- 2D or 3D immutable coordinate: `Coordinate(x, y)` or `Coordinate(x, y, z)`
- Properties: `.x`, `.y`, `.z` (z only for 3D)

### Region
- `Region(region_x, region_y, region_size, region_location=Coordinate(0,0))`
- Properties: `.name`, `.n` (size), `.area`, `.volume`, `.centre`
- Methods: `.clamp_coordinates(start_x, start_y, end_x, end_y)`, `.is_edge(x, y)`

### ChunkedRegion
- `ChunkedRegion(region_x, region_y, region_size, chunk_size, region_location=Coordinate(0,0))`
- Properties: `.chunks_per_side`, `.total_chunks`
- Methods: `.get_chunk_coordinates(loc)`, `.get_chunks_in_area(start, end)`

### Cell
- `Cell(coord, value=None, **attributes)`
- Represents a single tile or cell in a map, with a coordinate and optional value/attributes.
- Properties: `.coord`, `.value`, `.attributes` (dict of extra attributes)
- Example: `Cell(Coordinate(1,2), value=5, terrain='grass')`

### Group
- `Group(cells=None)`
- Represents a collection of `Cell` objects.
- Methods:
	- `.add(cell)`: Add a cell to the group
	- `.remove(cell)`: Remove a cell from the group
	- `.find_by_coord(coord)`: Find a cell by its coordinate
- Iterable: Can be iterated over like a list of cells

### Properties
- `Properties(data=None)`
- Dictionary-like class for storing arbitrary properties for tiles, cells, or regions.
- Behaves like a dict: supports item access, update, iteration, etc.
- Example: `Properties({'walkable': True, 'cost': 1})`

## Testing
See [docs/testing.md](docs/testing.md) for information on testing and usage examples.

## License
This package is licensed under the GNU General Public License v3.0 (GPLv3). See the LICENSE file for details.
