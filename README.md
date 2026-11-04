# mezura badge

A badge of your repository's line counts for its README, drawn by
[mezura](https://github.com/subamanis/mezura) in a GitHub workflow.

The SVG is pushed to a separate branch, `mezura-badge`, which always holds a single commit.
Your own branches get no commits.

## Usage

A workflow:

```yaml
name: badge

on:
  push:
    branches: [main]

permissions:
  contents: write

jobs:
  badge:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: subamanis/mezura-badge@v3
```

And the image in the README, with your owner and repository in the URL:

```markdown
[![mezura](https://raw.githubusercontent.com/OWNER/REPO/mezura-badge/badge.svg)](https://github.com/subamanis/mezura)
```

## Inputs

| Input | Default | |
|---|---|---|
| `args` | `--badge` | the mezura command line, passed whole |
| `file` | `badge.svg` | the file name on the `mezura-badge` branch |

`args` takes any flag of mezura. Quotes group words, as in a shell.

## The project's settings

If the repository has a `.mezura/config.txt`, the badge counts with its settings.

## Several badges

Each step writes its own file and keeps the files of the others.

```yaml
      - uses: subamanis/mezura-badge@v3
        with:
          args: --badge code tests languages
      - uses: subamanis/mezura-badge@v3
        with:
          args: --badge card --top 4
          file: card.svg
```

## Versions

Each release of the action runs the mezura release of the same number. `@v3` follows the latest 3.x.

## Notes

- The action runs on Linux X64 runners, such as `ubuntu-latest`.
- When mezura fails, the step fails and nothing is pushed.
- A badge identical to the one on the branch is left as it is.

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or https://www.apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or https://opensource.org/licenses/MIT)

at your option.
