# Workflow version history

| Snapshot | Git tag | Purpose |
| --- | --- | --- |
| Supplied source baseline | [before-swat62-update](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/before-swat62-update) | Original R and R Markdown scripts copied from the supplied archive |
| Initial revision 62 overlay | [swat62-workflow-v1](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v1) | Initial compatibility snapshot; superseded because it bundled model-specific deposition values |
| Reusable revision 62 overlay | [swat62-workflow-v2](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v2) | Current setup, scenario, and indicator workflow with explicit catchment-specific deposition configuration |

[Open the old-to-updated comparison](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/compare/before-swat62-update...swat62-workflow-v2?w=1) to review each changed line.

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
