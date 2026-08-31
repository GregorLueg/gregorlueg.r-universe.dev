# gregorlueg.r-universe.dev

Registry for <https://gregorlueg.r-universe.dev>. One file, `packages.json`,
listing the git repos r-universe should build.

The point of this is binaries. `bixverse` links a Rust static library that pulls
in a cmake build of HDF5, so a source install is a long wait. r-universe builds
macOS arm64 and x86_64 binaries for r-release and r-oldrel, so an install is a
download instead of a compile.

```r
install.packages(
  "bixverse",
  repos = c("https://gregorlueg.r-universe.dev", "https://cloud.r-project.org")
)

manifoldsR is here because it is a hard Imports: of bixverse and is not on
CRAN, so bixverse cannot resolve its dependencies without it.

All three track *release. Those repos auto-tag on a DESCRIPTION version bump
gated behind a green R-CMD-check, so the universe only moves when a version
has passed CI.

r-universe's Linux binaries are ubuntu:latest for r-release and r-devel only.
Off that combination you get a source build from here. Linux binaries with a
lower glibc floor live separately, see the bixverse README.

Rebuilds happen on a commit to the tracked ref, or every 30 days. To force one,
commit anything here. Build logs: https://github.com/r-universe/GregorLueg/actions
