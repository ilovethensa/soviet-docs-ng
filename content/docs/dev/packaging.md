---
weight: 1
bookFlatSection: true
title: "Creating packages"
---
# Creating Packages

## Overview

.ecmp files are used to create packages for installation using [CCCP](http://github.com/Soviet-Linux/CCCP) and [libspm](https://github.com/Soviet-Linux/libspm). The format includes new features to handle various package types and configurations.

## File Structure

.ecmp files use a [TOML](https://toml.io)-like syntax. Below is an example `.ecmp` file with detailed explanations for each section:

```toml
[info]
name = example
version = 1.0.0
type = src
license = Example
url = https://example.com
environment = example_environment

[exports]
MY_EXAMPLE_PREFIX=/usr/example/

[description]
Example package

[dependencies]
example-dependency-1

[optional]
example-dependency-2

[inputs]
this is a question, users input will be stored in $INPUT_n
this is a second question, users input will be stored in $INPUT_1
this is a third question, users input will be stored in $INPUT_2

[files]
IMG_9524.png https://example.com/IMG_9524.png d181ac6256...(sha256)
$NAME-$VERSION.tar.gz https://example.com/$NAME-$VERSION.tar.gz bc968e5286...(sha256)

[download]
tar -xzf $NAME-$VERSION.tar.gz

[install]
make
make DESTDIR=$BUILD_ROOT install

[special]
echo "This is SPECIAL"
```

## `[info]` Section

The `[info]` section contains metadata about the package. 

- **`name`** (Required): The name of the package. This should match the filename of the package.
- **`version`** (Required): The version number of the package.
- **`type`** (Required): Specifies the type of package. Options include:
  - `src`: Source package that needs to be compiled.
  - `bin`: Binary package.
  - `con`: Bundle for grouping dependencies and executing scripts.
- **`license`** (Optional): The license under which the package is distributed.
- **`url`** (Required): The URL from which the package can be downloaded.
- **`environment`** (Optional): Specifies an environment variable for additional configuration, useful for complex projects.

## `[exports]` Section

The `[exports]` section defines environment variables that are exported during installation.

- **Environment Variables**: Variables defined in this section are written to the default configuration directory and can be used by other packages.
  - Example:
    ```toml
    MY_EXAMPLE_PREFIX=/usr/example/
    ```
  - To use these variables in other packages, include `environment = example` in their `.ecmp` files.

## `[description]` Section

The `[description]` section provides a description of the package.

- **Description**: This section can include a textual description or markdown content to detail what the package does.

## `[dependencies]` Section

The `[dependencies]` section lists mandatory dependencies that the package needs to function.

- **Dependencies**: Each line specifies a required dependency.

## `[optional]` Section

The `[optional]` section lists optional dependencies that the package might need.

- **Optional Dependencies**: These are not required for the package to function but are needed for additional features or enhanced functionality.

## `[inputs]` Section

The `[inputs]` section is used to prompt the user for input during the installation process.

- **User Inputs**: Each line presents a question to the user. The responses are stored in environment variables (e.g., `$INPUT_n`, `$INPUT_1`, `$INPUT_2`).
  - Example:
    ```toml
    this is a question, users input will be stored in $INPUT_n
    this is a second question, users input will be stored in $INPUT_1
    ```

## `[files]` Section

The `[files]` section specifies files to be downloaded and their checksums.

- **File Entries**: Each line provides the filename, URL, and SHA-256 checksum of the file.
  - Example:
    ```toml
    IMG_9524.png https://example.com/IMG_9524.png d181ac6256...(sha256)
    $NAME-$VERSION.tar.gz https://example.com/$NAME-$VERSION.tar.gz bc968e5286...(sha256)
    ```

## `[download]` Section

The `[download]` section contains commands for downloading and extracting files.

- **Download Commands**: Commands in this section handle the extraction of the archive, ensuring the files are properly prepared.
  - Example:
    ```bash
    tar -xzf $NAME-$VERSION.tar.gz
    ```

## `[install]` Section

The `[install]` section includes commands to install the package.

- **Installation Commands**: This is essentially a bash script to build and install the package. It typically involves compiling the package and installing it to the `$BUILD_ROOT` directory.
  - Example:
    ```bash
    make
    make DESTDIR=$BUILD_ROOT install
    ```

## `[special]` Section

The `[special]` section allows you to run additional commands after the package installation.

- **Post-install Commands**: Commands in this section run after the main installation process. They are useful for finalizing installation tasks or performing additional configuration.
  - Example:
    ```bash
    echo "This is SPECIAL"
    ```

## Environment Variables

Before executing any scripts, the following environment variables are set based on the `[info]` section:

- **`$NAME`**: The package name.
- **`$VERSION`**: The package version.
- **`$TYPE`**: The package type.
- **`$URL`**: The package URL.
- **`$LICENSE`**: The package license.

These variables facilitate the package creation and installation process by providing necessary package-specific information.

## Important Notes

- Ensure that each section of the `.ecmp` file is correctly filled out to avoid issues during package creation and installation.
- The `.ecmp` file format has been updated to include more features for handling different package types and configurations.

For further examples and details, refer to the [OUR Repo](https://github.com/Soviet-Linux/OUR).