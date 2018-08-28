---
title: Rebase helper integration
subsection: maintain
order: 3
---

# Integrating rebase-helper with an upstream monitoring service

This chapter demonstrates how to include rebase-helper in your upstream monitoring service. 
If you would like to integrate rebase-helper into your upstream monitoring services, this chapter is for you.
Rebase-helper provides an API which you can use either directly from Python, or directly from the command line.

## Patch new upstream version and start scratch builds
Example of patching new sources and starting scratch builds with fedpkg.
This returns task_ids. The bash equivalents are included for comparison:
 
### Python API

```python3
from rebasehelper.application import Application
cli = CLI(['--non-interactive', '--builds-nowait', '--buildtool', 'fedpkg', 'upstream_version'])
rh = Application(cli)
rh.set_upstream_monitoring() # Switch rebase-helper to upstream release monitoring mode.
rh.run()
```

### BASH

```sh
rebase-helper --non-interactive --builds-nowait --buildtool fedpkg upstream_version
```

## Download logs and RPMs and compare with tools like ``abipkgdiff``

### Python API

```python3
cli = CLI(['--non-interactive', '--builds-nowait', '--buildtool', 'fedpkg', '--build-tasks', 'old_id,new_id'])
rh.run() # Downloads RPMs, logs and runs checkers and provides logs.
rh.get_rebasehelper_data() # Get all information about the results
```

### BASH

```sh
rebase-helper --non-interactive --builds-nowait --buildtool fedpkg --build-tasks old_id,new_id
```

