---
title: "hexgridkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["AxialHex", "CubeHex", "HexPixel"]
dependencies: []
symbols: ["AxialHex", "CubeHex", "HexPixel"]
related: ["api.md", "getting-started.md", "index.md"]
---

# hexgridkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## AxialHex

`Structure AxialHex`

Axial coordinates. Use MakeHex or validate before doing arithmetic.

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Q` | `Integer` | — | — |
| `R` | `Integer` | — | — |

## CubeHex

`Structure CubeHex`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Q` | `Integer` | — | — |
| `R` | `Integer` | — | — |
| `S` | `Integer` | — | — |

## HexPixel

`Structure HexPixel`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `X` | `Double` | — | — |
| `Y` | `Double` | — | — |

## HexGridKit functions

### MakeHex

`Public Function MakeHex(q As Integer, r As Integer) As AxialHex`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `q` | `Integer` | `ByVal` | Required |
| `r` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `AxialHex` |

### HexToCube

`Public Function HexToCube(cell As AxialHex) As CubeHex`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `cell` | `AxialHex` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `CubeHex` |

### CubeToHex

`Public Function CubeToHex(cube As CubeHex) As AxialHex`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `cube` | `CubeHex` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `AxialHex` |

### HexNeighbor

`Public Function HexNeighbor(cell As AxialHex, direction As Integer) As AxialHex`

Directions: E, NE, NW, W, SW, SE (screen Y points down).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `cell` | `AxialHex` | `ByVal` | Required |
| `direction` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `AxialHex` |

### HexDistance

`Public Function HexDistance(a As AxialHex, b As AxialHex) As Integer`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `a` | `AxialHex` | `ByVal` | Required |
| `b` | `AxialHex` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Integer` |

### HexToPixel

`Public Function HexToPixel(cell As AxialHex, size As Double, originX As Double = 0.0, originY As Double = 0.0) As HexPixel`

Pointy-top layout. Size is center-to-corner radius; screen Y points down.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `cell` | `AxialHex` | `ByVal` | Required |
| `size` | `Double` | `ByVal` | Required |
| `originX` | `Double` | `ByVal` | `0.0` |
| `originY` | `Double` | `ByVal` | `0.0` |

#### Returns

| Type |
| --- |
| `HexPixel` |

### PixelToHex

`Public Function PixelToHex(x As Double, y As Double, size As Double, originX As Double = 0.0, originY As Double = 0.0) As AxialHex`

Nearest cell using cube rounding; exact boundaries have deterministic ties.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |
| `size` | `Double` | `ByVal` | Required |
| `originX` | `Double` | `ByVal` | `0.0` |
| `originY` | `Double` | `ByVal` | `0.0` |

#### Returns

| Type |
| --- |
| `AxialHex` |

### HexCorners

`Public Function HexCorners(cell As AxialHex, size As Double, originX As Double = 0.0, originY As Double = 0.0) As Array Of HexPixel`

Six corners, clockwise in screen coordinates, starting at 30 degrees.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `cell` | `AxialHex` | `ByVal` | Required |
| `size` | `Double` | `ByVal` | Required |
| `originX` | `Double` | `ByVal` | `0.0` |
| `originY` | `Double` | `ByVal` | `0.0` |

#### Returns

| Type |
| --- |
| `Array Of HexPixel` |
