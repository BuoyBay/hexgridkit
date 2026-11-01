# Compute axial hex geometry, neighbors and pixel picking

Pure Buoy geometry for pointy-top hexagonal grids. `Import hexgridkit` works
from the source package or sealed archive. There are no native dependencies;
the Canvas demo is a separate consumer.

`AxialHex` has Integer Q/R fields, `CubeHex` Integer Q/R/S, and `HexPixel`
Double X/Y. Size means center-to-corner radius, not cell height. Pixel coordinates
and geometry are logical units; a caller supplies any zoom or display scale.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add hexgridkit --git https://github.com/BuoyBay/hexgridkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```buoy
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

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer hexgridkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

The generated agent files and editor settings stay local and are ignored by Git.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
