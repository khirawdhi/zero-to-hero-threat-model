# Assumptions

- Dependencies are installed in both local dev and CI environments.
- The project uses a dependency manifest and may use a lockfile.
- CI runners have network access to registries.
- Some dependencies may be transitive and not explicitly reviewed.
- Private registries may proxy public registries.
- Developers may occasionally bypass controls to “unblock builds”.
