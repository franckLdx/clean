# fs-cli
 A deno tool to handle directories a files. Inspired by [rimraf](https://www.npmjs.com/package/rimraf) and mkdirp [mkdirp](https://www.npmjs.com/package/mkdirp), fs-cli aims to write build scripts that can run under any shells.

 Current release implements [rm](#rm) and [mkdir](#mkdirp) commands, but more will come soon:
  * add Empty dir commands
  * add Copy commands
  * add Move commands
  * add Rename commands
  * add messages at the end of execution (total number of deletion:copy...)
  * add follow Symlinks options to glob search

# Installation

```sh
$ deno install --allow-read --allow-write --allow-env --allow-run -n fs_cli https://deno.land/x/fs_cli@v0.1.0/cli.ts
```mkdirp
The above command will always install the latest version. If you're updating from an older version you might need to run the command with the `-f` flag.

### To install a specific version
To install a specific version, run the install command with a specific version tag:

```sh
$ deno install --allow-read --allow-write --allow-env --allow-run -n fs_cli https://deno.land/x/fs_cli@<version>/cli.ts
```
For more information see [Deno's installer manual](https://deno.land/manual/tools/script_installer)

# Command
## rm
Syntax:
```
fs-cli rm <path or glob 1> <path or glob 2> ... <path or glob N> [--glob-root <path>] [--no-glob-dirs] [--no-glob-files]
```
Perform an rm -rf on each given directory and file. Globs are also supported.
If a path does not exist, fs-cli ignores it and processes the next one.

**With glob, don't forget to use quote to avoid glob being interpreted by sheel use quote: <code>'\*\*/*.tmp'</code> rahter than <code>\*\*/*.tmp**</code>

### Options
#### glob-root
root search for glob
```
fs-cli rm <path or glob 1>...<path or glob N> --glob-root <path>
```

#### no-glob-dirs
Directories are ignored when applying a glob
```
fs-cli rm <path or glob 1>...<path or glob N> --no-glob-dirs
```

#### no-glob-files
files are ignored when applying a glob
```
fs-cli rm <path or glob 1>...<path or glob N> --no-glob-files
```
## mkdirp
Syntax:
```
fs-cli mkdirp <path1> <path2> <path3>
```
Perform an mkdir -p on each given directory.

# Global options
## quiet mode
Output can be disable using -q/--quiet option:
```
fs-cli rm <path1> <path2> ... <pathN> -q
```
In case of failure, error message is always displayed, even in quiet mode.

### dry run mode
-d, --dry: Output the behavior, but does nothing
```
fs-cli rm <path1> <path2> ... <pathN> -d
```
