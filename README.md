# SWAT-Workflow-R: SWAT+ revision 62 update

This repository preserves the supplied workflow scripts before the update and the tested source overlay for SWAT+ revision 62.

| Snapshot | Browse source |
| --- | --- |
| Supplied workflow before the update | [before-swat62-update](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/before-swat62-update) |
| Tested revision 62 workflow | [swat62-workflow-v6](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v6) |

**[Compare the old and updated workflow on GitHub](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/compare/before-swat62-update...swat62-workflow-v6?w=1)**. GitHub shows removed lines in red and additions in green. The link hides whitespace-only changes. [Compare v5 to v6](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/compare/swat62-workflow-v5...swat62-workflow-v6?w=1) to review the plant-table correction.

The repository is a source overlay. Model inputs, GIS data, observations, executable files, generated results, and bundled R libraries remain in the original workspace. The original upstream project is [biopsichas/SWAT-Workflow-R](https://github.com/biopsichas/SWAT-Workflow-R).

## Use the updated workflow

Install the tested package versions from the `MR-Eini/*-swat62` repositories, place this `_Workflow` directory over the supplied workspace, and point `SWAT_EXE` to the Intel revision 62 executable:

```r
Sys.setenv(SWAT_EXE = "C:/path/to/swatplus-62-ifo-win_amd64-Rel.exe")
Sys.setenv(SWAT_PACKAGE_LIBRARY = "C:/path/to/R/library")
source("_Workflow/swat62.R")
swat62_require()
```

Atmospheric deposition uses the verified online EMEP 2025 Reporting source by default. No environment setting is needed for model years 1990-2024. To configure a catchment-specific file instead:

```r
Sys.setenv(SWAT_ATMO_DEP_MODE = "file",
           SWAT_ATMO_DEP_FILE = "C:/my-catchment/atmo_dep.csv")
```

To disable atmospheric deposition, set `SWAT_ATMO_DEP_MODE=none`. SWATprepR 1.0.16 uses the verified official EMEP 2025 Reporting resolver for years 1990-2024 when the variable is unset. `SWAT_ATMO_DEP_NETCDF` can override it with another template containing `{year}` and optionally `{timestep}`. No deposition values are embedded in this repository.

The setup and NBS entry scripts source this helper themselves. It verifies package versions and executable size, migrates the limited non-carbon input family used here, checks SWAT+ exit status, completion message, and unresolved plant diagnostics, and runs each scenario in a fresh directory. See [the plant-table migration report](PLANTS-SWAT62.md) for the corrected `agrc` substitution.

## Updated packages

| Package | Tested version | Repository |
| --- | ---: | --- |
| SWATreadR | 0.1.0.9014 | [MR-Eini/SWATreadR-swat62](https://github.com/MR-Eini/SWATreadR-swat62) |
| SWATrunR | 1.1.0.9019 | [MR-Eini/SWATrunR-swat62](https://github.com/MR-Eini/SWATrunR-swat62) |
| SWATtunR | 0.3.15 | [MR-Eini/SWATtunR-swat62](https://github.com/MR-Eini/SWATtunR-swat62) |
| SWATdoctR | 0.1.30 | [MR-Eini/SWATdoctR-swat62](https://github.com/MR-Eini/SWATdoctR-swat62) |
| SWATfarmR | 4.0.5 | [MR-Eini/SWATfarmR-swat62](https://github.com/MR-Eini/SWATfarmR-swat62) |
| SWATprepR | 1.0.16 | [MR-Eini/SWATprepR-swat62](https://github.com/MR-Eini/SWATprepR-swat62) |
| SWATmeasR | 0.9.4 | [MR-Eini/SWATmeasR-swat62](https://github.com/MR-Eini/SWATmeasR-swat62) |

See [VERSION-HISTORY.md](VERSION-HISTORY.md) for the workflow changes and [COMPATIBILITY.md](COMPATIBILITY.md) for the execution evidence and limits.
