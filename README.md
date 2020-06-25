# fs-cli
 A deno tool to handle directories a files. Inspired by [rimraf](https://www.npmjs.com/package/rimraf) and mkdirp [mkdirp](https://www.npmjs.com/package/mkdirp), fs-cli aims to write build scripts that can run under any shells.

 Current release implements [rm](#rm), [mkdirp](#mkdirp) and [copy](#cp) commands, but more will come soon:
  * add Empty dir commands
  * add Move commands
  * add Rename commands
  * add messages at the end of execution (total number of deletion:copy...)
  * add follow Symlinks options to glob search

# Installation

```sh
$ deno install --unstable --allow-read --allow-write --allow-env --allow-run -n fs_cli https://deno.land/x/fs_cli@v0.5.1/cli.ts
```
The above command will always install the latest version. If you're updating from an older version you might need to run the command with the `-f` flag.

### To upgrade to latest version
To install a specific version, run the install command with a specific version tag:

```sh
$ deno install --unstable --allow-read --allow-write --allow-env --allow-run -n fs_cli https://deno.land/x/fs_cli@<version>/cli.ts
```


### To install a specific version
To install a specific version, run the install command with a specific version tag:

```sh
$ deno install --unstable --allow-read --allow-write --allow-env --allow-run -n fs_cli https://deno.land/x/fs_cli@<version>/cli.ts
```
For more information see [Deno's installer manual](https://deno.land/manual/tools/script_installer)

# Commands
## rm
Syntax:
```
fs-cli rm <path or glob 1> <path or glob 2> ... <path or glob N>
```
Perform an rm -rf on each given directory and file. Globs are also supported.
If a path does not exist, fs-cli ignores it and processes the next one.

### Options
rm supports [glob options](#glob-options)

## mkdirp
Syntax:
```
fs-cli mkdirp <path1> <path2> <path3>
```
Perform an mkdir -p on each given directory.

## cp
Syntax:
```
fs-cli cp <source path1 or glob1>...<source pathN glob1> <dest>
```
Perform a cp -r. If <dest> includes directories, thos directories are created if they does not exists.

* To copy a file to anoter file:
```
fs-cli cp <source file> <dest dile>
```
* To copy a file to a directory (keeping the same file name), add an OS separator (/ under unix, \ under windows) at the end of dest:
```
fs-cli cp <source file> <dest dir>/ or fs-cli cp <source file> <dest dir>\ 
```
* To copy a file to directory (with another name) :
```
fs-cli cp <source file> <dest dir>/<dest file> or fs-cli cp <source file> <dest dir>\<dest file> 
 ```
 * To copy files to directory (with another name) :
```
fs-cli cp <source file1> ... <source filen> <dest dir>
 ```
* To copy a directory to another directory:
```
fs-cli cp <source dir path> <dest dir path>
```

### Options
cp supports [glob options](#glob-options)

# force mode: -f/--force
Be default the command failed if a file has to be over written. -f/--force option allow to over write existing file
# preserve timestamps: -p/--preserve
if use, set last modification and access times to the ones of the original source files. When not use, timestamp behavior is OS-dependent.

# Glob Options
Following are used for [rm](#rm) and [cp](#cp)

**To use glob intergated search rather than shell glob interpollation, don't forget to use quote to avoid glob being interpreted by sheel use quote: <code>'\*\*/*.tmp'</code> rahter than <code>\*\*/*.tmp**</code>

## glob-root
root search for glob
```
fs-cli <command> <path or glob 1>...<path or glob N> --glob-root <path>
```

## no-glob-dirs
Directories are ignored when applying a glob
```
fs-cli <command> <path or glob 1>...<path or glob N> --no-glob-dirs
```

## no-glob-files
files are ignored when applying a glob
```
fs-cli <command> <path or glob 1>...<path or glob N> --no-glob-files
```

# Global options
## quiet mode: -q/--quiet
Output can be disable using -q/--quiet option:
```
fs-cli rm <path1> <path2> ... <pathN> -q
```
In case of failure, error message is always displayed, even in quiet mode.

### dry run mode: -d/--dry
-d/--dry: Output the behavior, but does nothing
```
fs-cli rm <path1> <path2> ... <pathN> -d
```

# What's new
## 0.6.0
  * cp command now supports glob options

## 0.5.1
  * cp command

## 0.4.0
  * mkdirp command