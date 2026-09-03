# SWAT+ revision 62 compatibility evidence

Tests used the Windows Intel revision 62 executable `swatplus-62-ifo-win_amd64-Rel.exe` and the supplied 314-HRU model.

| Area | Result |
| --- | --- |
| Package source tests | All seven package test directories passed, 78 expectations total |
| Setup rebuild | GIS/database/text-input stages completed; 314 HRUs scheduled; final 2004-2023 SWAT+ run completed; a 260-file `clean_setup` was produced |
| SWATfarmR | Status quo, cover crop, and crop rotation projects ran through revision 62 |
| SWATprepR | Atmospheric deposition, point sources, and generated climate inputs ran through revision 62 |
| SWATmeasR | Afforestation and pond measures ran through revision 62 |
| NBS workflow | Status quo, cover crop, crop rotation, afforestation, pond, and combined scenarios all completed and produced indicators |
| Calibration and verification | The supplied discharge calibration/validation, sensitivity, crop, water-yield, and SWATdoctR verification exercises produced outputs |

Machine-readable scenario and indicator summaries are in [`compatibility/workflow-summary.json`](compatibility/workflow-summary.json) and [`compatibility/indicator-summary.json`](compatibility/indicator-summary.json).

This evidence covers the supplied model and its configured processes. The migration helper deliberately refuses carbon-enabled inputs because no scientifically justified carbon defaults were available. The Windows GNU revision 62 build stopped during weather initialization for this model; the Intel revision 62 build is the tested executable. Successful execution shows software compatibility, while calibration quality and scientific acceptance require a separate model assessment.
