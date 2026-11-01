# HexGridKit 0.1.0

Pure Buoy geometry for pointy-top hexagonal grids. `Import hexgridkit` works
from the source package or sealed archive. There are no native dependencies;
the Canvas demo is a separate consumer.

| API | Contract |
| --- | --- |
| `MakeHex(q, r)` | Validated axial coordinate; cube S is `-q-r` |
| `HexToCube(cell)`, `CubeToHex(cube)` | Convert structures and validate cube invariant |
| `HexNeighbor(cell, direction)` | Directions 0..5: E, NE, NW, W, SW, SE |
| `HexDistance(a, b)` | Minimum edge-adjacent steps |
| `HexToPixel(cell, size, originX = 0, originY = 0)` | Center in pointy-top layout; screen Y increases downward |
| `PixelToHex(x, y, size, originX = 0, originY = 0)` | Nearest hex center using cube rounding |
| `HexCorners(cell, size, originX = 0, originY = 0)` | Six `HexPixel` corners clockwise from 30 degrees |

`AxialHex` has Integer Q/R fields, `CubeHex` Integer Q/R/S, and `HexPixel`
Double X/Y. Size means center-to-corner radius, not cell height. Pixel coordinates
and geometry are logical units; a caller supplies any zoom or display scale.

All public operations validate input, including manually modified structures.
Q/R/S must each be within +/-1,000,000. Size must be finite and between 1e-6 and
1e6; origin components must be finite and within +/-1e12. Pixel input components
must be finite and within +/-4e12; points mapping outside coordinate bounds reject
before conversion to Integer. Invalid inputs throw `InvalidArgumentException`.
Neighbor queries at the coordinate boundary can therefore throw. There is no
wraparound topology. Invalid CubeHex S values reject without summing untrusted
64-bit values.

Rounding begins with `Floor(component + 0.5)` and repairs the cube component with
the largest error. Exact error ties repair Q before R before S. A point on a
shared boundary has a deterministic owner, though floating-point error near
boundaries can change the chosen cell. At very large origins with tiny cell
sizes, Double precision cannot distinguish adjacent centers. Use appropriately
scaled local coordinates when picking; the numeric bounds prevent overflow, not
loss of precision in extreme layouts.

## Verification and example

Maintainers run the private validation suite before release. See the repository README for public build instructions.

See the Canvas example (not included in this repository).
For pointer selection that survives an invalid pick, see the [getting started recovery example](../resources/buoy-docs/getting-started.md#handle-invalid-inputs).
The local archive is `packages/hexgridkit-0.1.0.buipkg`; no remote publication
has been performed. [Provenance and upstream differences](../PROVENANCE.md).
