# FDS code and inputs for a laterally oscillating PMMA slab

Modified Fire Dynamics Simulator (FDS) source files and input decks for the study of downward flame spread over a laterally oscillating finite-width PMMA slab.

## Contents

| Path | Contents |
| --- | --- |
| `Source/` | The 36 Fortran source files in the recorded production-build source set. |
| `patches/` | Consolidated customization patch and conservative-restart revision patch. |
| `inputs/primary_cards/` | Primary configurations, diagnostic continuations and development variants. |
| `inputs/verification_suite/cards/` | Translating-frame, grid and narrow-edge verification/sensitivity configurations. |
| `inputs/macfp_umd_pmma_spec/` | Four reference material-mapping fragments derived from the MaCFP database. These fragments have no runnable case geometry and are not substitutes for the full production decks. |
| `SHA256SUMS.txt` | SHA-256 digests of every repository file except the checksum file itself. |

There are 197 `.fds` files in total. Original input identifiers are retained: `d0`, `k3` and `k4` correspond to the article's cases A0, A75 and A25 (oscillation amplitudes 0, 75 and 25 mm at 0.25 Hz). Filenames also preserve historical, screening and diagnostic variants. Inclusion here does not mean that every variant is a successful or validated production case; the article identifies the comparisons used for its conclusions.

## Solver provenance

The source derives from [NIST FDS commit `ff928dbf68a2623ced3a007be75391c6dc6c9f90`](https://github.com/firemodels/fds/tree/ff928dbf68a2623ced3a007be75391c6dc6c9f90), in the FDS 6.11.1 source family. NIST is acknowledged as the upstream software source.

The 2026 modifications implement translating-frame forcing and matching open-boundary conditions, conservative restart continuity, and surface radiative-split diagnostics. The assembled `Source/` set combines the 35 predecessor source modules with the later conservative-restart revision of `dump.f90`. Its files were checked against the recorded production source manifest before publication. The recorded production executable SHA-256 is:

```text
4d06e039cc4797c90243e4be2435b5420ff3a3074ead57118baa80c356d2c87d
```

This is the production Fortran source-file set, not a complete upstream build repository. Obtain the build infrastructure and dependencies for the upstream commit separately. The original build used Intel oneAPI MPI/ifx, MKL, HYPRE 3.0.0 and SUNDIALS 7.5.0. A bitwise rebuild is not claimed.

The patches support inspection or reconstruction against the upstream source. Do not apply them again over the already assembled `Source/` files.

## Using the inputs

Use the modified solver with the selected full `.fds` deck. Some decks are restart continuations and require matching checkpoints, which are not included. Reference material fragments and screening variants are documented by their file comments and need their associated full configuration.

The repository does not include solver binaries, build dependencies, restart files, raw or reduced simulation results, post-processing products, or the manuscript. Other supporting data and required checkpoints are available from the corresponding authors upon request.

## Material-data attribution and licenses

Material parameters derive from the [MaCFP condensed-phase material database, commit `14b73ea959d3e6a74966a044ba5965aef0a38952`](https://github.com/MaCFP/matl-db/tree/14b73ea959d3e6a74966a044ba5965aef0a38952), [DOI: 10.18434/mds2-2586](https://doi.org/10.18434/mds2-2586). Source JSON hashes remain in the material-fragment comments.

The upstream NIST notice is retained in [LICENSE.txt](LICENSE.txt). The MaCFP MIT license is retained in [LICENSE-MaCFP.txt](LICENSE-MaCFP.txt). Existing in-source third-party copyright notices are preserved; see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). No single blanket replacement license is asserted over third-party components.

When reusing these files, acknowledge FDS and MaCFP, cite the associated article when available, and identify this repository version. The initial publication is tagged `v1.0.0`.
