# 00-proj-cfg — project config stage

The family's entry point: project configuration (new project, or a derived / modified existing project).

- **`proj-cfg`** (landed): interviews the user (product domain / chip / chip datasheet path / partitions [flash / RAM / stack / no-init / boundary overlap] / driver library / scheduling model / toolchain / coding standard / log placement), and generates `.spike-engineer-flow/context.md` for every other skill to read.

The other stage skills never re-ask for project facts; they only read this context file.
