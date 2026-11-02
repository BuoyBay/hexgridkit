---
title: "Hexagonal grid geometry getting started"
summary: "Use hexgridkit with a complete example and explicit numerical conventions."
category: "Guides"
order: 10
keywords: ["hexgridkit", "example", "import"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

## Prepare the package

Place the sealed `hexgridkit-0.1.0.buipkg` archive in your project's `packages/` directory. The example imports the package by its manifest name and uses explicit methods.

## First use

Create valid axial cells with `MakeHex`. Pick a center-to-corner radius and an origin, use `HexToPixel` to draw a cell, and use the same radius and origin with `PixelToHex` for pointer picking. Convert to cube coordinates when a three-coordinate representation is useful.

```basic
Import hexgridkit

Sub Main()
    Dim cell As AxialHex = MakeHex(2, -1)
    Dim neighbor As AxialHex = HexNeighbor(cell, 0)
    Print HexDistance(cell, neighbor)
    Dim center As HexPixel = HexToPixel(cell, 24.0, 100.0, 100.0)
    Dim picked As AxialHex = PixelToHex(center.X, center.Y, 24.0, 100.0, 100.0)
    Print picked.Q
    Print picked.R
End Sub
```

## Conventions

The layout is pointy-top with screen Y increasing downward. Size is the center-to-corner radius, not hex height. Directions 0..5 are E, NE, NW, W, SW, SE. Corners are clockwise from 30 degrees. Picking uses cube rounding beginning with Floor(component + 0.5), repairing the largest-error component; exact ties favor Q, then R, then S. Boundary ownership is deterministic for the computed values, but floating-point error near an edge can change it. Very large origins combined with tiny radii can erase adjacent-center distinctions; use suitably scaled local coordinates.

## Handle invalid inputs

All public operations validate structures, including manually changed fields. Cube Q/R/S each lie within +/-1,000,000 and must sum to zero. Radius must be finite and in 1e-6..1e6; origins must be finite and within +/-1e12. Pixel inputs must be finite and within +/-4e12, and mapped cells must still fit coordinate limits. Invalid inputs throw `InvalidArgumentException`; a neighbor at a coordinate boundary can also throw. There is no wraparound topology.

For pointer picking, keep the previous selection until `PixelToHex` succeeds. A rejected pointer position then leaves the selection usable:

```basic
Import hexgridkit

Sub Main()
    Dim selected As AxialHex = MakeHex(0, 0)
    Dim pointerX As Double = 100.0
    Dim pointerY As Double = 100.0
    Try
        Dim candidate As AxialHex = PixelToHex(pointerX, pointerY, 24.0, 100.0, 100.0)
        selected = candidate
    Catch e As InvalidArgumentException
        Print "Pointer is outside the supported grid"
    End Try
    Print selected.Q
End Sub
```

## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
