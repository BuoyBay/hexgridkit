---
title: "Hexagonal grid geometry API"
summary: "Public hexgridkit symbols and numerical contracts."
category: "Reference"
order: 20
keywords: ["hexgridkit", "API", "reference"]
symbols: ["AxialHex", "AxialHex.Q", "AxialHex.R", "CubeHex", "CubeHex.Q", "CubeHex.R", "CubeHex.S", "HexPixel", "HexPixel.X", "HexPixel.Y", "MakeHex", "HexToCube", "CubeToHex", "HexNeighbor", "HexDistance", "HexToPixel", "PixelToHex", "HexCorners"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

`Import hexgridkit` exposes these public types and operations.

| Symbol | Behavior |
| --- | --- |
| `AxialHex` | Structure containing Integer Q and R; implicit cube S is -Q-R. |
| `CubeHex` | Structure containing Integer Q, R, S; valid coordinates sum to zero. |
| `HexPixel` | Structure containing Double X and Y logical coordinates. |
| `MakeHex(q As Integer, r As Integer) As AxialHex` | Construct and validate an axial coordinate. |
| `HexToCube(cell As AxialHex) As CubeHex` | Validate and supply the third cube coordinate. |
| `CubeToHex(cube As CubeHex) As AxialHex` | Validate the cube invariant and return axial Q/R. |
| `HexNeighbor(cell As AxialHex, direction As Integer) As AxialHex` | Return the neighbor in direction 0..5; bounds still apply. |
| `HexDistance(a As AxialHex, b As AxialHex) As Integer` | Return the minimum number of edge-adjacent steps. |
| `HexToPixel(cell, size As Double, originX As Double = 0.0, originY As Double = 0.0) As HexPixel` | Return the center of a pointy-top cell. |
| `PixelToHex(x, y, size As Double, originX As Double = 0.0, originY As Double = 0.0) As AxialHex` | Pick the nearest center using validated cube rounding. |
| `HexCorners(cell, size As Double, originX As Double = 0.0, originY As Double = 0.0) As Array Of HexPixel` | Return six clockwise corners beginning at 30 degrees. |

## Numerical behavior

The layout is pointy-top with screen Y increasing downward. Size is the center-to-corner radius, not hex height. Directions 0..5 are E, NE, NW, W, SW, SE. Corners are clockwise from 30 degrees. Picking uses cube rounding beginning with Floor(component + 0.5), repairing the largest-error component; exact ties favor Q, then R, then S. Boundary ownership is deterministic for the computed values, but floating-point error near an edge can change it. Very large origins combined with tiny radii can erase adjacent-center distinctions; use suitably scaled local coordinates.

## Errors and ownership

All public operations validate structures, including manually changed fields. Cube Q/R/S each lie within +/-1,000,000 and must sum to zero. Radius must be finite and in 1e-6..1e6; origins must be finite and within +/-1e12. Pixel inputs must be finite and within +/-4e12, and mapped cells must still fit coordinate limits. Invalid inputs throw `InvalidArgumentException`; a neighbor at a coordinate boundary can also throw. There is no wraparound topology.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
