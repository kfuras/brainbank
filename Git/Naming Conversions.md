## Quick Ref: Conventional Commit Format

```bash
<type>(<scope>): <short summary>
```

### Examples:

| Type       | When to use it                                 | Example commit message                          |
| ---------- | ---------------------------------------------- | ----------------------------------------------- |
| `feat`     | New feature or script                          | `feat: add devcontainer automation script`      |
| `fix`      | Bug fix or broken logic                        | `fix: correct image filename formatting`        |
| `chore`    | Non-code updates (config, deps, .gitignore)    | `chore: update .gitignore to ignore output dir` |
| `refactor` | Code change not fixing a bug or adding feature | `refactor: clean up wrapper logic in script`    |
| `docs`     | Documentation changes                          | `docs: add README for devcontainer aliases`     |
| `style`    | Code style (spacing, linting, formatting)      | `style: format python file with black`          |
| `test`     | Adding or fixing tests                         | `test: add test for title wrap logic`           |
