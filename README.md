## xatlas

[![Travis CI Build Status](https://travis-ci.org/jpcy/xatlas.svg?branch=master)](https://travis-ci.org/jpcy/xatlas) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A cleaned up version of [thekla_atlas](https://github.com/Thekla/thekla_atlas).

Mesh charting, parameterization and atlas packing. Suitable for generating unique texture coordinates for baking lightmaps.

[![](https://user-images.githubusercontent.com/3744372/43034067-5c09c1da-8d18-11e8-8490-25770f05e8e0.png)](https://user-images.githubusercontent.com/3744372/43034066-53a62dee-8d18-11e8-9767-0b38ed3fa2d3.png)

## Changes from thekla_atlas
* Smaller code size - from about 18 KLOC to 8 KLOC
* Easier to integrate and build - a single source/header file pair instead of around 120 files and 10 directories.
* Atlas resolution option.
* Can output multiple atlases.
* Flexible data description API for input meshes.
* Better tolerance of bad input geometry. Zero length edges and zero area faces are ignored.

## How to use

1. Create an atlas with `xatlas::Create`.
2. Add one or more meshes with `xatlas::AddMesh`. Mesh geometry should be manifold.
3. Call `xatlas::GenerateCharts`. Meshes are segmented into disk-shaped charts, then flattened into 2D parameterizations.
4. Call `xatlas::PackCharts`. Charts are packed into one or more atlases. You can call `xatlas::PackCharts` multiple times to tweak options like unit to texel scale and resolution.
5. The `xatlas::Atlas` instance created in the first step now contains the result, namely meshes with a new UV channel that cross-reference input meshes. The number of vertices has likely increased compared to the input meshes, as the new UV channel duplicates some vertices that were previously shared between triangles. The number and coherence of indices remain unchanged, some are changed to reference vertices that were duplicated.
6. Cleanup with `xatlas::Destroy`.

## TODO

* Fix issues with chart boundaries
* Use multithreading to improve performance
* API to use custom parameterization. Use it to integrate [BFF](https://github.com/GeometryCollective/boundary-first-flattening) in the viewer.
* glTF support in the viewer

## Links
[Ignacio Castaño's blog post on thekla_atlas](http://the-witness.net/news/2010/03/graphics-tech-texture-parameterization/)

[Microsoft's UVAtlas](https://github.com/Microsoft/UVAtlas)

[Ministry of Flat](http://www.quelsolaar.com/ministry_of_flat/) - Commercial automated UV unwrapper.

[Lightmapper](https://github.com/ands/lightmapper) - Hemicube based lightmap baking. The example model texture coordinates were generated by [thekla_atlas](https://github.com/Thekla/thekla_atlas).

[aobaker](https://github.com/prideout/aobaker) - Ambient occlusion baking. Uses [thekla_atlas](https://github.com/Thekla/thekla_atlas).

[Gazebo model](https://opengameart.org/content/gazebo-0) by Teh_Bucket

[Tunnel scene](https://lmhpoly.com/unity-tutorial-volumetric-lighting/) by LMHPoly
