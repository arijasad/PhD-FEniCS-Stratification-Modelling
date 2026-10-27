# FEniCS stratification modelling

Source code for buoyant plume and stratification simulations developed for Arij Asad's
PhD research, *Mixing behaviour of plumes*, at the University of Bristol.

## Contents

| Folder | Purpose |
| --- | --- |
| `models/cartesian/` | Cartesian solvers and verification cases; Appendices B and D |
| `models/axisymmetric/` | Axisymmetric solvers and verification cases; Appendices C and D |
| `models/rectangular_3d_earlier/` | Reduced-height and trial 3D models; Appendix E |
| `models/rectangular_3d_quantitative/` | Full-height rectangular 3D model; Chapter 6 and Appendix E |
| `postprocessing/` | Python and MATLAB analysis |
| `archive/` | Earlier sources retained for provenance and checkpoint compatibility |
| `tests/` | Repository, numerical-kernel and mocked launcher checks |

This repository contains software. Saved simulation fields and checkpoints belong
in the corresponding numerical datasets.

## Numerical datasets

The numerical results are archived in three separate datasets with thesis
figures, saved fields, profiles, meshes, run settings and scalar budgets.

| Dataset | Thesis material | DOI |
| --- | --- | --- |
| Cartesian plume simulations | Appendices B and D | [10.5281/zenodo.23540946](https://doi.org/10.5281/zenodo.23540946) |
| Axisymmetric plume simulations | Appendices C and D | [10.5281/zenodo.23541035](https://doi.org/10.5281/zenodo.23541035) |
| Three-dimensional rectangular plume simulations | Chapter 6 and Appendix E | [10.5281/zenodo.23702682](https://doi.org/10.5281/zenodo.23702682) |

Each record includes a data guide and resolution comparisons. The 3D dataset
contains the long reference calculation, controlled reference and refined runs,
time-step comparisons, and the reduced-height fields used in Appendix E.

## Requirements and use

Simulations use **legacy FEniCS 2019.1.0**, PETSc/petsc4py and MPI/mpi4py.
Python analysis uses NumPy, SciPy, h5py and Matplotlib; axisymmetric overlap
calculations also use Shapely 2 or later. MATLAB scripts require MATLAB.

Follow the README in the relevant model folder. Cluster launchers use Linux,
Bash, GNU command-line tools and Slurm. Set your account, partition, modules and
working paths before submission. The 2D verification launchers use one MPI rank;
the 3D launchers request 24. The axisymmetric extra-fine quarter-step launcher
currently stops for review at 5 s, despite its historical `50s` filename.

## Checks and numerical scope

Run the repository checks from the root:

```sh
python tests/check_repository.py
```

The `layout` and `kernels` groups can also be run separately with `--group`.
The October 2026 audit passed syntax checks for 66 Python and 23 shell files,
all 13 numerical self-test programs, and the axisymmetric underflow regression.
The full launcher checks require Linux/GNU tools; the macOS run stopped during
mocked Cartesian packaging. See [reproducibility notes](docs/reproducibility.md)
for the environment and scope of these checks.

Mesh sensitivity remains unresolved in the thesis comparisons, and mesh
independence has not been established. The 2D geometries are approximations to
the experimental enclosure. Keep saved results with their mesh, configuration,
source hashes and accepted output times; retain XDMF/HDF5 files together.

## Citation

Asad, A. (2026). *FEniCS stratification modelling: Thesis code*
(version `thesis-code-2026-10-27`). Zenodo.
[doi:10.5281/zenodo.23702110](https://doi.org/10.5281/zenodo.23702110).

[GitHub release](https://github.com/arijasad/PhD-FEniCS-Stratification-Modelling/releases/tag/thesis-code-2026-10-27).

[CITATION.cff](CITATION.cff) identifies this archived version.

## Acknowledgements

Arij Asad developed this numerical software. Andrew G. W. Lawrie and
Stuart J. Thomson supervised the research; Yaojue Xiong helped with the initial
use of FEniCS. The research was supported by a Radioactive Waste Management
studentship, now within Nuclear Waste Services.

## Licence

[MIT](LICENSE), copyright 2026 Arij Asad. This licence also applies to the
`thesis-code-2026-09-27` source snapshot. External libraries retain their own licences.
