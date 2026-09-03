# Workflow version history

| Snapshot | Git tag | Purpose |
| --- | --- | --- |
| Supplied source baseline | [before-swat62-update](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/before-swat62-update) | Original R and R Markdown scripts copied from the supplied archive |
| Revision 62 source overlay | [swat62-workflow-v1](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/tree/swat62-workflow-v1) | Tested setup, scenario, and indicator workflow |

[Open the old-to-updated comparison](https://github.com/MR-Eini/SWAT-Workflow-R-swat62/compare/before-swat62-update...swat62-workflow-v1?w=1) to review each changed line.

## Revision 62 source overlay

- Adds `_Workflow/swat62.R`, which validates the seven package versions, locates the configured Intel revision 62 executable, checks each run, and applies the model-specific input migration.
- Stops replacing tested packages with arbitrary current GitHub versions during a workflow run.
- Updates the setup database without recreating the `project_config` table and uses header-aware SWAT input readers and writers.
- Uses a checked local atmospheric-deposition input when the obsolete EMEP endpoint is unavailable.
- Removes obsolete umbrella-package assumptions from setup and FarmR scripts and uses the packages that the scripts actually call.
- Runs NBS scenarios in independent model directories and copies only completed results.
- Corrects the supplied outlet from channel 6 to channel 5 and normalizes channel identifiers such as `5` and `cha5` during indicator calculation.

The workflow repository contains source and compact test evidence. Large model data, GIS layers, generated results, WhiteboxTools, and SWAT+ executables remain outside Git.
