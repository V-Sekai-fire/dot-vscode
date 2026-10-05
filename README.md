# dot-vscode

The code editor's configuration for the weftspun workspace, checked out at `.vscode/` in the workspace root.

## What it is for

It holds the build tasks, launch configurations, settings and recommended extensions for an editor opened at the workspace root, so one build task reaches every engine checkout on the entities side. The engine checkouts each ignore `.vscode/`, so a task kept inside one would be untracked; here a change arrives as a reviewed diff. The tasks run scons through the workspace's pixi environment.

## Use

```sh
repo sync .vscode
```

## Licence

MIT; see `LICENSE`.
