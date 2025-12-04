# bun-strap

Use [Bun](https://bun.sh) in your project without installing globally.

## Why

[Bun](https://bun.sh) is a fast all-in-one JavaScript runtime, package manager, and bundler. For many projects, it is important to ensure that all developers (and production) use the same version of the runtime to avoid inconsistencies and bugs. This can also lead to conflicts between different projects on the same machine requiring different versions. This script provides a simple solution.

This also enables bootstrapping truly zero-dependency development environments, that work regardless of globally installed runtimes.

## How it works

The script checks if bun is installed in a local `download` directory. If not, it downloads and installs the specified version of bun there. Finally, it runs bun with any provided arguments. The result is a transparent proxy to the desired version of bun.

## Usage

1. Copy the `bun` script to your project directory
2. Ensure it is executable: `chmod +x bun`
3. Run bun commands using `./bun <command>`, e.g., `./bun install`

## Use a specific bun version

The default behavior is to install the current latest version of bun. For most projects, we recommend pinning to a specific version by editing the `version` variable in the script or setting the `BUN_VERSION` environment variable before running the script.

Example using the environment variable:

```bash
BUN_VERSION="bun-v1.3.1" ./bun --version
# 1.3.1
```

## Optional alias

To simplify usage, you can create a function in your shell configuration (e.g., `.bashrc`, `.zshrc`). This falls back to using the globally installed bun if no local version is defined.

```bash
bun() {
  if [ -x ./bun ]; then
    ./bun "$@"
  else
    command bun "$@"
  fi
}
```
