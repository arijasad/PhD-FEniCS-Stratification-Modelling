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

The two-dimensional results are archived separately with the thesis appendix
plots, saved fields, profiles, meshes, run settings and scalar budgets.

| Dataset | Thesis material | DOI |
| --- | --- | --- |
| Cartesian plume simulations | Appendices B and D | [10.5281/zenodo.23540946](https://doi.org/10.5281/zenodo.23540946) |
| Axisymmetric plume simulations | Appendices C and D | [10.5281/zenodo.23541035](https://doi.org/10.5281/zenodo.23541035) |

Each record includes a data guide and resolution comparisons. The three-dimensional
dataset is planned as a separate record.

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
(version `thesis-code-2026-09-27`).
Zenodo. [doi:10.5281/zenodo.23540374](https://doi.org/10.5281/zenodo.23540374).

[Original GitHub release](https://github.com/arijasad/PhD-FEniCS-Stratification-Modelling/releases/tag/thesis-code-2026-09-27).

[CITATION.cff](CITATION.cff) identifies the September source snapshot,
commit `709c85596109fa5700c16ddb7e8c454d5f2d5900`.

## Related experimental methods and acknowledgements

The companion [PLIF experimental analysis](https://github.com/arijasad/PhD-Stratified-Plume-Experimental-Analysis)
adapts the reconstruction method in Horne-Jones et al. (2026), Section 3.2,
equations (16)–(18):

Horne-Jones, J. T., Glinnan, D. J., Lawrie, A. G. W. and Williams, R. J. R. (2026).
*Controlled accelerations for Rayleigh–Taylor instability*. **Experiments in Fluids**,
67, 96. [doi:10.1007/s00348-026-04249-4](https://doi.org/10.1007/s00348-026-04249-4).

Arij Asad developed this numerical software. Andrew G. W. Lawrie and
Stuart J. Thomson supervised the research; Yaojue Xiong helped with the initial
use of FEniCS. The research was supported by a Radioactive Waste Management
studentship, now within Nuclear Waste Services.

## Licence

[MIT](LICENSE), copyright 2026 Arij Asad. This licence also applies to the
`thesis-code-2026-09-27` source snapshot. External libraries retain their own licences.
