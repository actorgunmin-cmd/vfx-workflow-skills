# VFX skill distribution entry point

This repository distributes 30 independent instruction skills as ZIP archives. It is not a rendering engine or a copy of an Instagram creator's internal skills. Read README.md for the catalog and THIRD_PARTY_NOTICES.md for provenance.

For a VFX request:

1. Select the relevant skill from the README catalog instead of reading all 30.
2. Extract that skill's `<skill-name>.zip` into a temporary working directory, then read `<skill-name>/SKILL.md` before execution. Its scripts are relative to that extracted skill folder.
3. For source review, installation, or package maintenance, extract `hyun2ai-vfx-skills.zip`. It contains readable `skills/`, project-installable `.agents/skills/`, `tools/`, source manifests, individual ZIPs and the original package README.
4. Verify ZIP digests against SHA256SUMS when checking the published distribution. Repository ZIPs are at the root; the full archive's own download index uses its nested `individual/` layout.

The four user-requested additions are `vfx-ai-source-match`, `vfx-source-color-match`, `vfx-precision-roto`, and `vfx-original-restore`. Their Python helpers align a corresponding still pair, fit/apply a fixed SDR sRGB gain/offset, report alpha QC statistics, and perform linear-light over compositing. These helpers do not run an entire video generation or GPU matting pipeline.

Check installed tools, source timestamps, color encoding and alpha conventions before executing a chosen workflow. MatAnyone 2's inspected `fgr` output is a green-background preview, not clean straight foreground RGB. Do not composite it as if the old background had been removed from edge RGB.

Validation status is recorded in validation.json and REVIEW.md: 30 structures, 11 helper test groups and 31 ZIP archives passed local checks. Production-plate rendering, full-video temporal alignment, COLMAP/Blender/AE/FFmpeg runs, MatAnyone GPU inference and AI generation were not tested. Report actual executions and remaining limits accurately.
