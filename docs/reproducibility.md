# Reproducibility notes

## Checks performed on 21 October 2026

The audited source is `thesis-code-2026-09-27`, commit
`709c85596109fa5700c16ddb7e8c454d5f2d5900`.

- Syntax checks passed for 66 Python files and 23 Bash files.
- Required bundles and source/provenance hashes passed the layout checks.
- All 13 numerical self-test programs and the axisymmetric underflow regression passed.
- The full check command stopped during mocked Cartesian launcher packaging on
  macOS: BSD `tee` rejects `--output-error`, and the sandbox blocked a process
  substitution path. Later launcher checks were not reached.

The audit used macOS arm64, Python 3.12.14, NumPy 2.3.5, SciPy 1.18.1,
Shapely 2.2.0, h5py 3.16.0 and Matplotlib 3.11.2. These versions describe the
check environment; the historical FEniCS solver environment is not fully pinned.
The checks exercised repository structure and numerical kernels, without running
coupled FEniCS/MPI simulations or MATLAB analysis.

## Working with saved results

Retain each run's configuration, source/helper hashes, mesh, units, coordinate
conventions, accepted output times and scalar budgets. Keep all parts of
XDMF/HDF5 pairs together. Restart checkpoints need the matching source and
configuration; source-hash checks enforce that match. A paused launcher exit
code of 75 indicates a review stop rather than completion to the nominal end time.

Earlier clipped transport and revised conservative methods coexist in the
repository. Identify the method and exact source for each dataset. Record the
comparison grids, slab definitions and error normalisation used in analysis.
Simulation data are not included in the September software release.

## Interpreting the numerical comparisons

The thesis comparisons show unresolved mesh sensitivity. Integrated budgets or
coarse averages can agree while local concentration fields differ. Cartesian
slot and axisymmetric cylinder geometries also differ from the rectangular
experimental enclosure.

The 3D full-step and half-step cases share a simulated history through 6.979 s;
their comparison therefore concerns the subsequent evolution. Conservation,
boundedness and kernel tests address specific numerical properties; establishing
mesh independence requires convergence of the quantities being interpreted.
