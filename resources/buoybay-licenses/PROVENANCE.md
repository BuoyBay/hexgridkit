# Source study and scope

The user supplied Xojo's [open-source catalog](https://documentation.xojo.com/resources/extras/open_source_projects.html),
which links [Eugene Dakin's HexagonalGridXojo](https://github.com/eugenedakin/HexagonalGridXojo).
Inspected master commit `e669da68b4a8d6ecc54e83aff782051f3e1179fd`, its README,
LICENSE and `HexagonXojo.xojo_xml_project`.

The fetched master ZIP SHA-256 was
`9bf81c947a0647518c113b1bc0c8e92d2ed298f0dcba6f5d48346117967852f8`.
Upstream LICENSE is MIT, copyright 2020 eugenedakin. The README credits Rod
Stephens' C# hexagonal-grid article and points to a newer upstream version.
No upstream source, screenshot or binary project is redistributed here; the
Buoy code is an independent implementation of standard axial/cube geometry.

The inspected upstream project draws a flat-top grid using row/column coordinates
with odd columns vertically offset. `HexToPoints` returns polygon coordinates;
`HexWidth` derives width from height; `PointToHex` picks a row/column and MouseDown
updates a label and selected polygons. The Buoy demo preserves the draw/pick/
highlight technique with an explicit pointy-top axial layout. It does not claim
coordinate compatibility with that older offset API.

HexGridKit adds reusable validated cube conversion, neighbors and step distance,
which are useful foundations for the prior scrolling-world examples. Missing
higher-level features include offset-coordinate compatibility helpers, obstacle
maps, pathfinding, rings/spirals, line-of-sight, sprite integration, pan/zoom and
map serialization. Basic drawing and pointer picking require no compiler or
runtime change: Canvas paths and MouseDown already provide the necessary surface.
