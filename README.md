<h1 align="center">
  Fast Node Manager (<code>fnm</code>)
  <img alt="Amount of downloads" src="https://img.shields.io/github/downloads/vanaware/fnm-alpine/total.svg?style=flat" />
  <a href="https://github.com/vanaware/fnm-alpine/actions"><img src="https://img.shields.io/github/workflow/status/vanaware/fnm-alpine/Alpine/master?label=workflow" alt="GitHub Actions workflow status" /></a>
</h1>

> Alpine Build for " :rocket: Fast and simple Node.js version manager, built in Rust"

<div align="center">
  <img src="./docs/fnm.svg" alt="Blazing fast!">
</div>

## Features

:earth_americas: Alpine Linux support

:sparkles: Single file, easy installation, instant startup

:rocket: Built with speed in mind

:open_file_folder: Works with `.node-version` and `.nvmrc` files

## Installation

### Alpine Node dependencies

For better experience first install these packages into alpine.    

```sh
apk add libstdc++ libgcc curl unzip
export SHELL="/bin/ash"
```

### Using a script (macOS/Linux)

For `ash`, `bash`, `zsh` and `fish` shells, there's an [automatic installation script](./.ci/install.sh).

First ensure that `curl` and `unzip` are already installed on you operating system. Then execute:

```sh
curl -fsSL https://vanaware.github.io/fnm-alpine/install.sh | sh
```

#### Upgrade

Upgrading `fnm` is almost the same as installing it. To prevent duplication in your shell config file add `--skip-shell` to install command.

#### Parameters

`--install-dir`

Set a custom directory for fnm to be installed. The default is `$HOME/.fnm`.

`--skip-shell`

Skip appending shell specific loader to shell config file, based on the current user shell, defined in `$SHELL`. e.g. for Bash, `$HOME/.bashrc`. `$HOME/.zshrc` for Zsh. For Fish - `$HOME/.config/fish/conf.d/fnm.fish`

Example:

```sh
curl -fsSL https://vanaware.github.io/fnm-alpine/install.sh | sh -s -- --install-dir "./.fnm" --skip-shell
```

### Manually

- Download the [latest release binary](https://github.com/vanaware/fnm-alpine/releases)
- Make it available globally on `PATH` environment variable
- [Set up your shell for fnm](#shell-setup)

### Removing

To remove fnm (😢), just delete the `.fnm` folder in your home directory. You should also edit your shell configuration to remove any references to fnm (ie. read [Shell Setup](#shell-setup), and do the opposite).

## Completions

fnm ships its completions with the binary:

```sh
fnm completions --shell <SHELL>
```

Where `<SHELL>` can be one of the supported shells:

- `bash`
- `ash`
- `zsh`
- `fish`

Please follow your shell instructions to install them.

### Shell Setup

Environment variables need to be setup before you can start using fnm.
This is done by evaluating the output of `fnm env`.
To automatically run `fnm use` when a directory contains a `.node-version` or `.nvmrc` file, add the `--use-on-cd` option to your shell setup.

Adding a `.node-version` to your project is as simple as:

```bash
$ node --version
v14.18.3
$ node --version > .node-version
```

Check out the following guides for the shell you use:

#### Bash

Add the following to your `.bashrc` profile:

```bash
eval "$(fnm env --use-on-cd)"
```

#### Zsh

Add the following to your `.zshrc` profile:

```zsh
eval "$(fnm env --use-on-cd)"
```

#### Fish shell

Create `~/.config/fish/conf.d/fnm.fish` add this line to it:

```fish
fnm env --use-on-cd | source
```

#### PowerShell

Add the following to the end of your profile file:

```powershell
fnm env --use-on-cd | Out-String | Invoke-Expression
```

- Profile is located at `~/.config/powershell/Microsoft.PowerShell_profile.ps1`

## [Usage](./docs/commands.md)

[See the available commands for an extended usage documentation](./docs/commands.md)

## Contributing

PRs welcome :tada:

### Developing:

```sh
# Install Rust
git clone https://github.com/vanaware/fnm-alpine.git
cd fnm-alpine/
cargo build
```

### Running Binary:

```sh
cargo run -- --help # Will behave like `fnm --help`
```

### Running Tests:

```sh
cargo test
```
