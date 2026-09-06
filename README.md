# AmberMD-Scripting

`AmberMD-Scripting` is a small collection of Bash helpers for preparing and running staged AMBER molecular dynamics workflows. The repository is aimed at practical command-line usage rather than a general-purpose software package.

## Repository contents
### `generate_amber_inputs.sh`
Generates a directory tree and AMBER input files for a staged membrane-oriented workflow that includes:
- minimization
- restrained heating
- restrained equilibration
- production dynamics

The script builds numbered directories such as `001.min`, `002.heat`, and trajectory-specific folders like `Traj1/003.equil` and `Traj1/004.prod`.

Example:

```bash
bash generate_amber_inputs.sh 101 120 3
```

This generates inputs for 3 trajectories with ligand or residue restraints applied over residues 101 to 120.

A cleanup mode is also available:

```bash
bash generate_amber_inputs.sh cleanup 3
```

### `run_md_simulations.sh`
Runs the generated AMBER workflow in either preproduction or production mode.

Example preproduction run:

```bash
bash run_md_simulations.sh system_name 16 0
```

Example production run:

```bash
bash run_md_simulations.sh system_name 16 1 0 0 5 1
```

This corresponds to:
- `system_name` = AMBER topology/restart basename
- `16` = number of CPU cores
- `1` = production mode
- `0` = GPU index
- `0` = starting production segment
- `5` = final production segment
- `1` = trajectory number

## Workflow assumptions
These scripts assume:
- an AMBER installation with `pmemd.MPI` and `pmemd.cuda`
- an MPI launcher available as `mpirun`
- a membrane-style workflow using the directory structure created by `generate_amber_inputs.sh`
- topology and coordinate files such as `system_name.parm7` and `system_name.rst7`

## Scope and limitations
This repository is best viewed as a reusable lab-style scripting helper rather than a polished framework. The workflow reflects specific simulation assumptions, including staged restrained equilibration and membrane-oriented restraint setup, so users should review the generated input files before adopting them in a different context.

## Contributing
Focused pull requests are preferred. The most useful contributions are bug fixes, clearer usage notes, portability improvements, and workflow clarifications that preserve the repository’s lightweight scripting focus.

## Citation
If this repository contributes to published work, please cite the repository and the version used.

## License
This project is released under the MIT License. See [`LICENSE`](LICENSE) for details.

## Contact
For questions or adaptation to related workflows, see the [repository owner profile](https://github.com/senal-liyanage).
