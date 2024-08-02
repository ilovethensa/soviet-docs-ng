---
weight: 1
bookFlatSection: true
title: "Using CCCP"
---
# cccp Command-Line Tool Documentation

## Overview

The `cccp` command-line tool is used for managing packages on your system. This document provides detailed information about the various options and commands
 available with `cccp`.

## Command Usage


### Available Options

#### General Information

- `v, --version`: Displays the version of the `cccp` tool.
- `h, --help`: Displays the help message with a summary of available options.

#### Package Management

- `i, --install <package>`: Installs a package from our repository..
- `--no-checksum`: Bypasses the checksum verification for package installations.
- `r, --remove <package>`: Removes a package from the system.
- `l, --list`: Lists all packages currently installed on the system.
- `s, --search <package>`: Searches for packages that match the name provided.
- `--update`: Checks for updates to installed packages.
- `--upgrade`: Upgrades all outdated packages to their latest versions.
- `pkg, --package <path/to/package.ecmp>`: Installs a package from a specified file.
- `ow, --overwrite`: Allows overwriting of already installed packages.

#### Debugging and Verbose Output

- `dbg, --debug <level 0-4>`: Prints debug information at the specified level (0-4). Higher levels provide more detailed debug output.
- `--clean`: Cleans up the cache directory to free up space and remove obsolete files.
- `--verbose`: Switches the output to verbose mode, providing more detailed information during execution.

#### Example Commands

Here are a few examples of how to use the `cccp` tool with various options:

- Install vim: `cccp --install vim`
- Remove capitalism(the package): `cccp --remove capitalism`
- List installed packages: `cccp --list`
- Search for a package: `cccp --search example-package`
- Update all packages: `cccp --update`
- Upgrade all outdated packages: `cccp --upgrade`
- Install a package from a file: `cccp --package /path/to/package.ecmp`
- Enable verbose output: `cccp --verbose`
- Set debug level: `cccp --debug 2`