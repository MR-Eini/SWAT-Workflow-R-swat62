# Workflow version history

| Snapshot | Git tag | Purpose |
| --- | --- | --- |
| Supplied source baseline | [before-swat62-update](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/before-swat62-update) | Original R and R Markdown scripts copied from the supplied archive |
| Initial revision 62 overlay | [swat62-workflow-v1](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v1) | Initial compatibility snapshot; superseded because it bundled model-specific deposition values |
| Reusable revision 62 overlay | [swat62-workflow-v2](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v2) | First reusable setup, scenario, and indicator workflow with explicit catchment-specific deposition configuration |
| Deposition routing correction | [swat62-workflow-v3](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v3) | Keeps data acquisition and `add_atmo_dep()` in one tested function so all three modes follow the correct path |
| Current online EMEP source | [swat62-workflow-v4](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v4) | Uses the verified official EMEP 2025 Reporting source automatically when users select `emep` mode |
| Online EMEP default | [swat62-workflow-v5](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v5) | Selects the tested EMEP source by default while retaining `file`, `none`, and custom-source options |
| Plant schema correction | [swat62-workflow-v6](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v6) | Expands legacy plant rows for revision 62 and rejects unresolved crop diagnostics |
| Portable executable and cleanup | [swat62-workflow-v7](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v7) | Stages the tested executable in `clean_setup` and removes temporary Doctor runs by default |

[Open the old-to-updated comparison](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/compare/before-swat62-update...swat62-workflow-v7?w=1) to review each changed line.

## Revision 62 source overlay v7

- Copies exactly one tested Intel revision 62 executable into the generated `clean_setup` for calibration, validation, verification and scenario steps.
- Uses SWATdoctR 0.1.31, which removes temporary verification runs and the empty `.run_verify` parent on success or error unless a user explicitly keeps them for debugging.
- Adds focused checks for executable staging and cleanup.

## Revision 62 source overlay v6

- Migrates every legacy `plants.plt` row from 53 to 56 fields while preserving all custom and calibrated crops.
- Checks `diagnostics.out` after each executable run and fails if SWAT+ could not resolve a plant name.
- Uses SWATreadR 0.1.0.9014 and SWATdoctR 0.1.30.

## Revision 62 source overlay v5

- Makes the tested EMEP 2025 Reporting source the default atmospheric-deposition mode.
- Retains `file` and `none` modes plus `SWAT_ATMO_DEP_NETCDF` for a custom reporting source.

## Revision 62 source overlay v4

- Uses SWATprepR 1.0.16 and its official EMEP 2025 Reporting resolver when `emep` mode is selected without an override.
- Covers EMEP meteorological years 1990-2024; users can still provide another template or source list through `SWAT_ATMO_DEP_NETCDF`.

## Revision 62 source overlay v3

- Moves acquisition and writing into `configure_atmo_dep()` so `none` never reads or writes, while both `file` and `emep` write their selected data exactly once.
- Adds a regression test for all three modes and for missing/invalid configuration.

## Revision 62 source overlay v2

- Removes the bundled atmospheric-deposition CSV because those values belong only to the supplied catchment.
- Adds explicit `none`, `file`, and `emep` modes. File inputs are validated; EMEP extraction requires a current local or OPeNDAP source for every requested year.
- Updates the required SWATprepR version to 1.0.15.

## Revision 62 source overlay

- Adds `_Workflow/swat62.R`, which validates the seven package versions, locates the configured Intel revision 62 executable, checks each run, and applies the model-specific input migration.
- Stops replacing tested packages with arbitrary current GitHub versions during a workflow run.
- Updates the setup database without recreating the `project_config` table and uses header-aware SWAT input readers and writers.
- Leaves atmospheric deposition disabled until the user selects a catchment-specific file or current EMEP NetCDF sources.
- Removes obsolete umbrella-package assumptions from setup and FarmR scripts and uses the packages that the scripts actually call.
- Runs NBS scenarios in independent model directories and copies only completed results.
- Corrects the supplied outlet from channel 6 to channel 5 and normalizes channel identifiers such as `5` and `cha5` during indicator calculation.

The workflow repository contains source and compact test evidence. Large model data, GIS layers, generated results, WhiteboxTools, and SWAT+ executables remain outside Git.
