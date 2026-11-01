---
title: "Hexagonal grid geometry"
summary: "Convert, measure, and pick bounded pointy-top axial hexagonal grids."
category: "Overview"
order: 0
keywords: ["hexgridkit", "mathematics", "geometry"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# Hexagonal grid geometry

`hexgridkit` supplies pure Buoy axial/cube structures, neighbor directions, step distances, centers, corners, and pixel picking. It has no native dependency or drawing ownership; a Canvas or other renderer consumes the returned logical coordinates.

## Install

Copy `hexgridkit-0.1.0.buipkg` into the consuming application's `packages/` directory and use `Import hexgridkit`. The package is independently usable on macOS, Windows, and Linux. It requires no native bridge or drawing surface.

## Scope and provenance

This independently implemented geometry package was informed by Eugene Dakin's HexagonalGridXojo source study. Its pointy-top axial coordinates are not compatible with the inspected older flat-top offset-coordinate API. Offset compatibility helpers, obstacle maps, pathfinding, rings, spirals, line of sight, sprites, pan/zoom, and serialization are separate work.

## Validation and limits

All public operations validate structures, including manually changed fields. Cube Q/R/S each lie within +/-1,000,000 and must sum to zero. Radius must be finite and in 1e-6..1e6; origins must be finite and within +/-1e12. Pixel inputs must be finite and within +/-4e12, and mapped cells must still fit coordinate limits. Invalid inputs throw `InvalidArgumentException`; a neighbor at a coordinate boundary can also throw. There is no wraparound topology.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
