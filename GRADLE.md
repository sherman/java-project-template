## Gradle dependency management

* Use the version catalog (`gradle/libs.versions.toml`) and reuse existing aliases.
  Do not put inline external dependency coordinates or versions in module builds,
  including annotation processors and external plugins.
* Prefer BOMs already added to the version catalog. Keep dependencies versionless in
  the catalog when their version is supplied by a BOM applied to the consuming
  configuration. For unmanaged dependencies, use `version.ref` and share one version
  key across related artifacts.
* Check convention plugins before adding dependencies. `java-conventions` already
  supplies BOMs, JetBrains annotations, common test libraries, and fixture platforms.
  Avoid redundant declarations; retain declarations needed for the correct scope.
* Add dependencies to the minimal required scope. Use `implementation` for internal
  dependencies and `api` for dependency types exposed to consumers. Use `compileOnly`
  for compile-time-only dependencies, `compileOnlyApi` when consumers also need them
  at compile time, and `runtimeOnly` for runtime-only dependencies. Use the corresponding
  test and test-fixture configurations for dependencies needed only by those sources,
  and annotation-processor configurations for annotation processors.
* Declare dependencies used directly instead of relying on incidental transitive
  dependencies. Reference local modules with `project(':module')` and consume shared
  test helpers through `testFixtures(project(':module'))`.
* Use `platform(...)` for BOM imports. Avoid `enforcedPlatform(...)` in published
  libraries because its forced versions propagate to consumers.
* Explain version overrides, exclusions, and `transitive = false` with a short comment.
  Include a removal condition for temporary overrides. Keep exclusions scoped to the
  affected dependency.
* Group dependency declarations: project dependencies, external dependencies, then
  fixture and test dependencies.
* When changing versions, BOMs, exclusions, or scopes, use module-scoped `dependencies`
  or `dependencyInsight` reports to verify the affected compile and runtime classpaths.
