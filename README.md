# .vscode

The editor configuration for the weftspun workspace, as a repository. Checked out at `.vscode/`
at the workspace root, which is where an editor opening that root looks, so one build task
reaches every Godot checkout on the entities side.

```sh
repo sync .vscode
```

| | |
|---|---|
| `tasks.json` | the scons builds, one task across every `4-entities/godot-*` checkout |
| `launch.json` | run or attach to the editor binary a build just produced |
| `settings.json` | the workspace's editor settings: tracked, shared, reviewed |
| `extensions.json` | the extensions the tasks and launches need to work |

## Why a repository

The same argument `dot-claude` carries. A `linkfile` is invisible to every check here —
`repo status` cannot see drift in it and nothing gates it — while a repository is ordinary:
a change to the build flags arrives in a diff somebody approved, with a commit behind it.
The manifest entry is `name="dot-vscode" path=".vscode"`. The path is fixed by the editor,
which reads that name and nothing else, so the repository name gave way.

## Why not inside a Godot checkout

Every `4-entities/godot-*` checkout gitignores `.vscode/`, so a task written inside one is
untracked on the desk that wrote it and absent on the next. There are nine of them against
one upstream, and a build task that lives in the workspace root is written once rather than
nine times and then drifting.

## Windows toolchain

The build task sources `vcvars64.bat` before invoking scons, because the compiler is found
through the environment that script sets and nothing else. `scons` itself comes from the
`build` pixi environment the workspace already declares, so the task shells out to
`pixi run -e build` rather than expecting a scons on `PATH`.
