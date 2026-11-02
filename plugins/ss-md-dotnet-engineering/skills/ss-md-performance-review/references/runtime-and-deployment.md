## 1. Runtime, JIT, and AOT

Runtime and publish choices affect startup, memory, throughput, compatibility, and deployment. Consider them when those are explicit constraints; do not rewrite source code based on assumed JIT behavior.

- Target a supported runtime and keep servicing updates current. Check the official support policy and the project's target before version-specific decisions.
- Benchmark the deployed target framework, architecture, build configuration, and publish mode when runtime configuration is relevant. JIT, tiered compilation, dynamic PGO, ReadyToRun, and Native AOT can have different cold-start and steady-state behavior.
- Consider Native AOT when startup, memory footprint, restricted environments, or deployment economics justify it. Check trimming/reflection and dynamic-code requirements, library compatibility, diagnostics, platform-specific publishing, and build costs.
- Change runtime knobs only when measurements identify a relevant issue. Re-test runtime-specific workarounds after upgrades; a newer runtime may make them unnecessary or counterproductive.
- Prefer clear source code; do not rely on undocumented JIT behavior or assume a source-level rewrite produces faster machine code.
