# gregorlueg.r-universe.dev

Registry for <https://gregorlueg.r-universe.dev>. One file, `packages.json`,
listing the git repos r-universe should build.

The point of this is binaries. Most of these packages link a Rust static
library, and `bixverse` also pulls in a cmake build of HDF5, so a source install
is a long wait. r-universe builds macOS arm64 and x86_64 binaries for r-release
and r-oldrel, so an install is a download instead of a compile.

```r
install.packages(
  "bixverse",
  repos = c("https://gregorlueg.r-universe.dev", "https://cloud.r-project.org")
)
```

## Packages

| Package | What it is | Tracks |
|---|---|---|
| [bixverse](https://github.com/GregorLueg/bixverse) | Rust-accelerated bioinformatics and computational biology workflows | `main` |
| [bixverse.plots](https://github.com/GregorLueg/bixverse.plots) | Plotting functions for bixverse | `*release` |
| [bixverse.gpu](https://github.com/GregorLueg/bixverse.gpu) | GPU methods via cubecl and WGPU: k-means, correlations and single cell acceleration | `main` |
| [manifoldsR](https://github.com/GregorLueg/manifoldsR) | Fast low-dimensional embeddings and clustering via Rust | `*release` |
| [annsearchR](https://github.com/GregorLueg/annsearchR) | Fast approximate nearest neighbour search | `*release` |
| [genewalkR](https://github.com/GregorLueg/genewalkR) | Graph algorithms: diffusions and small neural networks like node2vec | `main` |
| [devforge](https://github.com/GregorLueg/devforge) | Development tooling for the bixverse family | `main` |

manifoldsR is a hard Imports: of bixverse and bixverse.gpu, and isn't on CRAN,
so neither resolves its dependencies without this universe. bixverse.plots and
bixverse.gpu both import bixverse.

The `*release` repos auto-tag on a DESCRIPTION version bump gated behind a green
R-CMD-check, so those packages only move when a version has passed CI. The
`main` ones move on every commit to `main`.

r-universe's Linux binaries are ubuntu:latest for r-release and r-devel only.
Off that combination you get a source build from here. Linux binaries with a
lower glibc floor live separately, see the bixverse README.

Rebuilds happen on a commit to the tracked ref, or every 30 days. To force one,
commit anything here. Build logs: https://github.com/r-universe/GregorLueg/actions
