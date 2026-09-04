# SWAT+ revision 62 compatibility evidence

Tests used the Windows Intel revision 62 executable `swatplus-62-ifo-win_amd64-Rel.exe` and the supplied 314-HRU model.

| Area | Result |
| --- | --- |
| Package source tests | All seven package test directories passed, 83 expectations total |
| Setup rebuild | GIS/database/text-input stages completed; 314 HRUs scheduled; final 2004-2023 SWAT+ run completed; a 260-file `clean_setup` was produced |
| SWATfarmR | Status quo, cover crop, and crop rotation projects ran through revision 62 |
| SWATprepR | Atmospheric deposition, point sources, and generated climate inputs ran through revision 62 |
| SWATmeasR | Afforestation and pond measures ran through revision 62 |
| NBS workflow | Status quo, cover crop, crop rotation, afforestation, pond, and combined scenarios all completed and produced indicators |
| Calibration and verification | The supplied discharge calibration/validation, sensitivity, crop, water-yield, and SWATdoctR verification exercises produced outputs |

Machine-readable scenario and indicator summaries are in [`compatibility/workflow-summary.json`](compatibility/workflow-summary.json) and [`compatibility/indicator-summary.json`](compatibility/indicator-summary.json).

The setup execution used the supplied catchment's atmospheric-deposition data as an external test fixture. Those values are not distributed in the reusable workflow. Public users must explicitly disable deposition, provide their own validated CSV, or configure current EMEP NetCDF sources.

The v3 deposition routing was tested separately for all three modes. A file-mode integration check called the real SWATprepR `add_atmo_dep()` on a temporary copy of the supplied clean setup; the Intel revision 62 executable then completed the updated model. Mocked routing checks verify that `none` never writes and that both `file` and `emep` write exactly once.

The official EMEP 2025 Reporting OPeNDAP source was opened online for all 20 years from 2004 through 2023. SWATprepR extracted finite catchment values, wrote `atmodep.cli`, and the Intel revision 62 executable completed the resulting model. This exercises both filename forms in the current catalog.

This evidence covers the supplied model and its configured processes. The migration helper deliberately refuses carbon-enabled inputs because no scientifically justified carbon defaults were available. The Windows GNU revision 62 build stopped during weather initialization for this model; the Intel revision 62 build is the tested executable. Successful execution shows software compatibility, while calibration quality and scientific acceptance require a separate model assessment.
