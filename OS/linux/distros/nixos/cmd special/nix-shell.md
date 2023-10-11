[nix-shell documentation stable version](https://nixos.org/manual/nix/stable/command-ref/nix-shell)
[nix-shell documentation unstable version](https://nixos.org/manual/nix/unstable/command-ref/nix-shell)
# [Name](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#name)

`nix-shell` - start an interactive shell based on a Nix expression

# [Synopsis](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#synopsis)

`nix-shell` [`--arg` _name_ _value_] [`--argstr` _name_ _value_] [{`--attr` | `-A`} _attrPath_] [`--command` _cmd_] [`--run` _cmd_] [`--exclude` _regexp_] [`--pure`] [`--keep` _name_] {{`--packages` | `-p`} {_packages_ | _expressions_} … | [_path_]}

# [Disambiguation](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#disambiguation)

This man page describes the command `nix-shell`, which is distinct from `nix shell`. For documentation on the latter, run `nix shell --help` or see `man nix3-shell`.

# [Description](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#description)

The command `nix-shell` will build the dependencies of the specified derivation, but not the derivation itself. It will then start an interactive shell in which all environment variables defined by the derivation _path_ have been set to their corresponding values, and the script `$stdenv/setup` has been sourced. This is useful for reproducing the environment of a derivation for development.

If _path_ is not given, `nix-shell` defaults to `shell.nix` if it exists, and `default.nix` otherwise.

If _path_ starts with `http://` or `https://`, it is interpreted as the URL of a tarball that will be downloaded and unpacked to a temporary location. The tarball must include a single top-level directory containing at least a file named `default.nix`.

If the derivation defines the variable `shellHook`, it will be run after `$stdenv/setup` has been sourced. Since this hook is not executed by regular Nix builds, it allows you to perform initialisation specific to `nix-shell`. For example, the derivation attribute

```bash
shellHook =   ''     
	echo "Hello shell"     
	export SOME_API_TOKEN="$(cat ~/.config/some-app/api-token)"   
'';
```

will cause `nix-shell` to print `Hello shell` and set the `SOME_API_TOKEN` environment variable to a user-configured value.

# [Options](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#options)

All options not listed here are passed to `nix-store --realise`, except for `--arg` and `--attr` / `-A` which are passed to `nix-instantiate`.

- `--command` _cmd_  
    In the environment of the derivation, run the shell command _cmd_. This command is executed in an interactive shell. (Use `--run` to use a non-interactive shell instead.) However, a call to `exit` is implicitly added to the command, so the shell will exit after running the command. To prevent this, add `return` at the end; e.g. `--command "echo Hello; return"` will print `Hello` and then drop you into the interactive shell. This can be useful for doing any additional initialisation.
    
- `--run` _cmd_  
    Like `--command`, but executes the command in a non-interactive shell. This means (among other things) that if you hit Ctrl-C while the command is running, the shell exits.
    
- `--exclude` _regexp_  
    Do not build any dependencies whose store path matches the regular expression _regexp_. This option may be specified multiple times.
    
- `--pure`  
    If this flag is specified, the environment is almost entirely cleared before the interactive shell is started, so you get an environment that more closely corresponds to the “real” Nix build. A few variables, in particular `HOME`, `USER` and `DISPLAY`, are retained.
    
- `--packages` / `-p` _packages_…  
    Set up an environment in which the specified packages are present. The command line arguments are interpreted as attribute names inside the Nix Packages collection. Thus, `nix-shell --packages libjpeg openjdk` will start a shell in which the packages denoted by the attribute names `libjpeg` and `openjdk` are present.
    
- `-i` _interpreter_  
    The chained script interpreter to be invoked by `nix-shell`. Only applicable in `#!`-scripts (described below).
    
- `--keep` _name_  
    When a `--pure` shell is started, keep the listed environment variables.
    

# [Common Options](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#common-options)

Most Nix commands accept the following command-line options:

- [`--help`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-help)
    
    Prints out a summary of the command syntax and exits.
    
- [`--version`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-version)
    
    Prints out the Nix version number on standard output and exits.
    
- [`--verbose`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-verbose) / `-v`
    
    Increases the level of verbosity of diagnostic messages printed on standard error. For each Nix operation, the information printed on standard output is well-defined; any diagnostic information is printed on standard error, never on standard output.
    
    This option may be specified repeatedly. Currently, the following verbosity levels exist:
    
    - `0` “Errors only”
        
        Only print messages explaining why the Nix invocation failed.
        
    - `1` “Informational”
        
        Print _useful_ messages about what Nix is doing. This is the default.
        
    - `2` “Talkative”
        
        Print more informational messages.
        
    - `3` “Chatty”
        
        Print even more informational messages.
        
    - `4` “Debug”
        
        Print debug information.
        
    - `5` “Vomit”
        
        Print vast amounts of debug information.
        
- [`--quiet`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-quiet)
    
    Decreases the level of verbosity of diagnostic messages printed on standard error. This is the inverse option to `-v` / `--verbose`.
    
    This option may be specified repeatedly. See the previous verbosity levels list.
    
- [`--log-format`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-log-format) _format_
    
    This option can be used to change the output of the log format, with _format_ being one of:
    
    - `raw`
        
        This is the raw format, as outputted by nix-build.
        
    - `internal-json`
        
        Outputs the logs in a structured manner.
        
        > **Warning**
        > 
        > While the schema itself is relatively stable, the format of the error-messages (namely of the `msg`-field) can change between releases.
        
    - `bar`
        
        Only display a progress bar during the builds.
        
    - `bar-with-logs`
        
        Display the raw logs, with the progress bar at the bottom.
        
- [`--no-build-output`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-no-build-output) / `-Q`
    
    By default, output written by builders to standard output and standard error is echoed to the Nix command's standard error. This option suppresses this behaviour. Note that the builder's standard output and error are always written to a log file in `prefix/nix/var/log/nix`.
    
- [`--max-jobs`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-max-jobs) / `-j` _number_
    
    Sets the maximum number of build jobs that Nix will perform in parallel to the specified number. Specify `auto` to use the number of CPUs in the system. The default is specified by the `max-jobs` configuration setting, which itself defaults to `1`. A higher value is useful on SMP systems or to exploit I/O latency.
    
    Setting it to `0` disallows building on the local machine, which is useful when you want builds to happen only on remote builders.
    
- [`--cores`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-cores)
    
    Sets the value of the `NIX_BUILD_CORES` environment variable in the invocation of builders. Builders can use this variable at their discretion to control the maximum amount of parallelism. For instance, in Nixpkgs, if the derivation attribute `enableParallelBuilding` is set to `true`, the builder passes the `-jN` flag to GNU Make. It defaults to the value of the `cores` configuration setting, if set, or `1` otherwise. The value `0` means that the builder should use all available CPU cores in the system.
    
- [`--max-silent-time`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-max-silent-time)
    
    Sets the maximum number of seconds that a builder can go without producing any data on standard output or standard error. The default is specified by the `max-silent-time` configuration setting. `0` means no time-out.
    
- [`--timeout`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-timeout)
    
    Sets the maximum number of seconds that a builder can run. The default is specified by the `timeout` configuration setting. `0` means no timeout.
    
- [`--keep-going`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-keep-going) / `-k`
    
    Keep going in case of failed builds, to the greatest extent possible. That is, if building an input of some derivation fails, Nix will still build the other inputs, but not the derivation itself. Without this option, Nix stops if any build fails (except for builds of substitutes), possibly killing builds in progress (in case of parallel or distributed builds).
    
- [`--keep-failed`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-keep-failed) / `-K`
    
    Specifies that in case of a build failure, the temporary directory (usually in `/tmp`) in which the build takes place should not be deleted. The path of the build directory is printed as an informational message.
    
- [`--fallback`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-fallback)
    
    Whenever Nix attempts to build a derivation for which substitutes are known for each output path, but realising the output paths through the substitutes fails, fall back on building the derivation.
    
    The most common scenario in which this is useful is when we have registered substitutes in order to perform binary distribution from, say, a network repository. If the repository is down, the realisation of the derivation will fail. When this option is specified, Nix will build the derivation instead. Thus, installation from binaries falls back on installation from source. This option is not the default since it is generally not desirable for a transient failure in obtaining the substitutes to lead to a full build from source (with the related consumption of resources).
    
- [`--readonly-mode`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-readonly-mode)
    
    When this option is used, no attempt is made to open the Nix database. Most Nix operations do need database access, so those operations will fail.
    
- [`--arg`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-arg) _name_ _value_
    
    This option is accepted by `nix-env`, `nix-instantiate`, `nix-shell` and `nix-build`. When evaluating Nix expressions, the expression evaluator will automatically try to call functions that it encounters. It can automatically call functions for which every argument has a [default value](https://nixos.org/manual/nix/unstable/language/constructs#functions) (e.g., `{ argName ? defaultValue }: ...`).
    
    With `--arg`, you can also call functions that have arguments without a default value (or override a default value). That is, if the evaluator encounters a function with an argument named _name_, it will call it with value _value_.
    
    For instance, the top-level `default.nix` in Nixpkgs is actually a function:
    
    ``{ # The system (e.g., `i686-linux') for which to build the packages.   system ? builtins.currentSystem   ... }: ...``
    
    So if you call this Nix expression (e.g., when you do `nix-env --install --attr pkgname`), the function will be called automatically using the value [`builtins.currentSystem`](https://nixos.org/manual/nix/unstable/language/builtins) for the `system` argument. You can override this using `--arg`, e.g., `nix-env --install --attr pkgname --arg system \"i686-freebsd\"`. (Note that since the argument is a Nix string literal, you have to escape the quotes.)
    
- [`--argstr`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-argstr) _name_ _value_
    
    This option is like `--arg`, only the value is not a Nix expression but a string. So instead of `--arg system \"i686-linux\"` (the outer quotes are to keep the shell happy) you can say `--argstr system i686-linux`.
    
- [`--attr`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-attr) / `-A` _attrPath_
    
    Select an attribute from the top-level Nix expression being evaluated. (`nix-env`, `nix-instantiate`, `nix-build` and `nix-shell` only.) The _attribute path_ _attrPath_ is a sequence of attribute names separated by dots. For instance, given a top-level Nix expression _e_, the attribute path `xorg.xorgserver` would cause the expression `e.xorg.xorgserver` to be used. See [`nix-env --install`](https://nixos.org/manual/nix/unstable/command-ref/nix-env/install) for some concrete examples.
    
    In addition to attribute names, you can also specify array indices. For instance, the attribute path `foo.3.bar` selects the `bar` attribute of the fourth element of the array in the `foo` attribute of the top-level expression.
    
- [`--expr`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-expr) / `-E`
    
    Interpret the command line arguments as a list of Nix expressions to be parsed and evaluated, rather than as a list of file names of Nix expressions. (`nix-instantiate`, `nix-build` and `nix-shell` only.)
    
    For `nix-shell`, this option is commonly used to give you a shell in which you can build the packages returned by the expression. If you want to get a shell which contain the _built_ packages ready for use, give your expression to the `nix-shell --packages` convenience flag instead.
    
- [`-I`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-I) _path_
    
    Add an entry to the [Nix expression search path](https://nixos.org/manual/nix/unstable/command-ref/conf-file#conf-nix-path). This option may be given multiple times. Paths added through `-I` take precedence over [`NIX_PATH`](https://nixos.org/manual/nix/unstable/command-ref/env-common#env-NIX_PATH).
    
- [`--option`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-option) _name_ _value_
    
    Set the Nix configuration option _name_ to _value_. This overrides settings in the Nix configuration file (see nix.conf5).
    
- [`--repair`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#opt-repair)
    
    Fix corrupted or missing store paths by redownloading or rebuilding them. Note that this is slow because it requires computing a cryptographic hash of the contents of every path in the closure of the build. Also note the warning under `nix-store --repair-path`.
    

> **Note**
> 
> See [`man nix.conf`](https://nixos.org/manual/nix/unstable/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.

# [Environment variables](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#environment-variables)

- `NIX_BUILD_SHELL`  
    Shell used to start the interactive environment. Defaults to the `bash` found in `<nixpkgs>`, falling back to the `bash` found in `PATH` if not found.

# [Common Environment Variables](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#common-environment-variables)

Most Nix commands interpret the following environment variables:

- [`IN_NIX_SHELL`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-IN_NIX_SHELL)
    
    Indicator that tells if the current environment was set up by `nix-shell`. It can have the values `pure` or `impure`.
    
- [`NIX_PATH`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_PATH)
    
    A colon-separated list of directories used to look up the location of Nix expressions using [paths](https://nixos.org/manual/nix/unstable/language/values#type-path) enclosed in angle brackets (i.e., `<path>`), e.g. `/home/eelco/Dev:/etc/nixos`. It can be extended using the [`-I` option](https://nixos.org/manual/nix/unstable/command-ref/opt-common#opt-I).
    
    If `NIX_PATH` is not set at all, Nix will fall back to the following list in [impure](https://nixos.org/manual/nix/unstable/command-ref/conf-file#conf-pure-eval) and [unrestricted](https://nixos.org/manual/nix/unstable/command-ref/conf-file#conf-restrict-eval) evaluation mode:
    
    1. `$HOME/.nix-defexpr/channels`
    2. `nixpkgs=/nix/var/nix/profiles/per-user/root/channels/nixpkgs`
    3. `/nix/var/nix/profiles/per-user/root/channels`
    
    If `NIX_PATH` is set to an empty string, resolving search paths will always fail. For example, attempting to use `<nixpkgs>` will produce:
    
    ```bash
	error: file 'nixpkgs' was not found in the Nix search path
	```
    
- [`NIX_IGNORE_SYMLINK_STORE`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_IGNORE_SYMLINK_STORE)
    
    Normally, the Nix store directory (typically `/nix/store`) is not allowed to contain any symlink components. This is to prevent “impure” builds. Builders sometimes “canonicalise” paths by resolving all symlink components. Thus, builds on different machines (with `/nix/store` resolving to different locations) could yield different results. This is generally not a problem, except when builds are deployed to machines where `/nix/store` resolves differently. If you are sure that you’re not going to do that, you can set `NIX_IGNORE_SYMLINK_STORE` to `1`.
    
    Note that if you’re symlinking the Nix store so that you can put it on another file system than the root file system, on Linux you’re better off using `bind` mount points, e.g.,
    
    ```bash 
    mkdir /nix 
    mount -o bind /mnt/otherdisk/nix /nix```
    
    Consult the mount 8 manual page for details.
    
- [`NIX_STORE_DIR`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_STORE_DIR)
    
    Overrides the location of the Nix store (default `prefix/store`).
    
- [`NIX_DATA_DIR`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_DATA_DIR)
    
    Overrides the location of the Nix static data directory (default `prefix/share`).
    
- [`NIX_LOG_DIR`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_LOG_DIR)
    
    Overrides the location of the Nix log directory (default `prefix/var/log/nix`).
    
- [`NIX_STATE_DIR`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_STATE_DIR)
    
    Overrides the location of the Nix state directory (default `prefix/var/nix`).
    
- [`NIX_CONF_DIR`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_CONF_DIR)
    
    Overrides the location of the system Nix configuration directory (default `prefix/etc/nix`).
    
- [`NIX_CONFIG`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_CONFIG)
    
    Applies settings from Nix configuration from the environment. The content is treated as if it was read from a Nix configuration file. Settings are separated by the newline character.
    
- [`NIX_USER_CONF_FILES`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_USER_CONF_FILES)
    
    Overrides the location of the Nix user configuration files to load from.
    
    The default are the locations according to the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html). See the [XDG Base Directories](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#xdg-base-directories) sub-section for details.
    
    The variable is treated as a list separated by the `:` token.
    
- [`TMPDIR`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-TMPDIR)
    
    Use the specified directory to store temporary files. In particular, this includes temporary build directories; these can take up substantial amounts of disk space. The default is `/tmp`.
    
- [`NIX_REMOTE`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_REMOTE)
    
    This variable should be set to `daemon` if you want to use the Nix daemon to execute Nix operations. This is necessary in [multi-user Nix installations](https://nixos.org/manual/nix/unstable/installation/multi-user). If the Nix daemon's Unix socket is at some non-standard path, this variable should be set to `unix://path/to/socket`. Otherwise, it should be left unset.
    
- [`NIX_SHOW_STATS`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_SHOW_STATS)
    
    If set to `1`, Nix will print some evaluation statistics, such as the number of values allocated.
    
- [`NIX_COUNT_CALLS`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-NIX_COUNT_CALLS)
    
    If set to `1`, Nix will print how often functions were called during Nix expression evaluation. This is useful for profiling your Nix expressions.
    
- [`GC_INITIAL_HEAP_SIZE`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-GC_INITIAL_HEAP_SIZE)
    
    If Nix has been configured to use the Boehm garbage collector, this variable sets the initial size of the heap in bytes. It defaults to 384 MiB. Setting it to a low value reduces memory consumption, but will increase runtime due to the overhead of garbage collection.
    

## [XDG Base Directories](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#xdg-base-directories)

Nix follows the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).

For backwards compatibility, Nix commands will follow the standard only when [`use-xdg-base-directories`](https://nixos.org/manual/nix/unstable/command-ref/conf-file#conf-use-xdg-base-directories) is enabled. [New Nix commands](https://nixos.org/manual/nix/unstable/command-ref/new-cli/nix) (experimental) conform to the standard by default.

The following environment variables are used to determine locations of various state and configuration files:

- [`XDG_CONFIG_HOME`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-XDG_CONFIG_HOME) (default `~/.config`)
- [`XDG_STATE_HOME`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-XDG_STATE_HOME) (default `~/.local/state`)
- [`XDG_CACHE_HOME`](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#env-XDG_CACHE_HOME) (default `~/.cache`)

# [Examples](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#examples)

To build the dependencies of the package Pan, and start an interactive shell in which to build it:

```shell
nix-shell '<nixpkgs>' --attr pan 
[nix-shell]$ eval ${unpackPhase:-unpackPhase} 
[nix-shell]$ cd $sourceRoot 
[nix-shell]$ eval ${patchPhase:-patchPhase} 
[nix-shell]$ eval ${configurePhase:-configurePhase} 
[nix-shell]$ eval ${buildPhase:-buildPhase} 
[nix-shell]$ ./pan/gui/pan
```

The reason we use form `eval ${configurePhase:-configurePhase}` here is because those packages that override these phases do so by exporting the overridden values in the environment variable of the same name. Here bash is being told to either evaluate the contents of 'configurePhase', if it exists as a variable, otherwise evaluate the configurePhase function.

To clear the environment first, and do some additional automatic initialisation of the interactive shell:

```bash
$ nix-shell '<nixpkgs>' --attr pan --pure \     
--command 'export NIX_DEBUG=1; export NIX_CORES=8; return'
```

Nix expressions can also be given on the command line using the `-E` and `-p` flags. For instance, the following starts a shell containing the packages `sqlite` and `libX11`:

```bash
$ nix-shell --expr 'with import <nixpkgs> { }; runCommand "dummy" { buildInputs = [ sqlite xorg.libX11 ]; } ""'
```

A shorter way to do the same is:

```bash
$ nix-shell --packages sqlite xorg.libX11 
[nix-shell]$ echo $NIX_LDFLAGS 
… -L/nix/store/j1zg5v…-sqlite-3.8.0.2/lib -L/nix/store/0gmcz9…-libX11-1.6.1/lib …
```

Note that `-p` accepts multiple full nix expressions that are valid in the `buildInputs = [ ... ]` shown above, not only package names. So the following is also legal:

```bash
$ nix-shell --packages sqlite 'git.override { withManual = false; }'
```

The `-p` flag looks up Nixpkgs in the Nix search path. You can override it by passing `-I` or setting `NIX_PATH`. For example, the following gives you a shell containing the Pan package from a specific revision of Nixpkgs:

```bash
$ nix-shell --packages pan -I nixpkgs=https://github.com/NixOS/nixpkgs/archive/8a3eea054838b55aca962c3fbde9c83c102b8bf2.tar.gz  

[nix-shell:~]$ pan --version 
Pan 0.139
```

# [Use as a `#!`-interpreter](https://nixos.org/manual/nix/unstable/command-ref/nix-shell#use-as-a--interpreter)

You can use `nix-shell` as a script interpreter to allow scripts written in arbitrary languages to obtain their own dependencies via Nix. This is done by starting the script with the following lines:

```shell
#! /usr/bin/env nix-shell 
#! nix-shell -i real-interpreter --packages packages
```

where _real-interpreter_ is the “real” script interpreter that will be invoked by `nix-shell` after it has obtained the dependencies and initialised the environment, and _packages_ are the attribute names of the dependencies in Nixpkgs.

The lines starting with `#! nix-shell` specify `nix-shell` options (see above). Note that you cannot write `#! /usr/bin/env nix-shell -i ...` because many operating systems only allow one argument in `#!` lines.

For example, here is a Python script that depends on Python and the `prettytable` package:

```python
#! /usr/bin/env nix-shell 
#! nix-shell -i python --packages python pythonPackages.prettytable  

import prettytable  
# Print a simple table. 
t = prettytable.PrettyTable(["N", "N^2"]) 
for n in range(1, 10): t.add_row([n, n * n]) 
print t
```

Similarly, the following is a Perl script that specifies that it requires Perl and the `HTML::TokeParser::Simple` and `LWP` packages:

```perl
#! /usr/bin/env nix-shell 
#! nix-shell -i perl --packages perl perlPackages.HTMLTokeParserSimple perlPackages.LWP  

use HTML::TokeParser::Simple;  
# Fetch nixos.org and print all hrefs. my 
$p = HTML::TokeParser::Simple->new(url => 'http://nixos.org/');  
while (my $token = $p->get_tag("a")) {     
	my $href = $token->get_attr("href");     
	print "$href\n" if $href; 
}
```

Sometimes you need to pass a simple Nix expression to customize a package like Terraform:

```bash
#! /usr/bin/env nix-shell 
#! nix-shell -i bash --packages "terraform.withPlugins (plugins: [ plugins.openstack ])"  

terraform apply
```

> **Note**
> 
> You must use double quotes (`"`) when passing a simple Nix expression in a nix-shell shebang.

Finally, using the merging of multiple nix-shell shebangs the following Haskell script uses a specific branch of Nixpkgs/NixOS (the 20.03 stable branch):

```shell
#! /usr/bin/env nix-shell 
#! nix-shell -i runghc --packages "haskellPackages.ghcWithPackages (ps: [ps.download-curl ps.tagsoup])" 
#! nix-shell -I nixpkgs=https://github.com/NixOS/nixpkgs/archive/nixos-20.03.tar.gz  

import Network.Curl.Download 
import Text.HTML.TagSoup 
import Data.Either 
import Data.ByteString.Char8 (unpack)  

-- Fetch nixos.org and print all hrefs. 
main = do   
	resp <- openURI "https://nixos.org/"   
	let tags = filter (isTagOpenName "a") $ parseTags $ unpack $ fromRight undefined resp   
	let tags' = map (fromAttrib "href") tags   
	mapM_ putStrLn $ filter (/= "") tags'
```

If you want to be even more precise, you can specify a specific revision of Nixpkgs:

```bash
nix-shell -I nixpkgs=https://github.com/NixOS/nixpkgs/archive/0672315759b3e15e2121365f067c1c8c56bb4722.tar.gz
```

The examples above all used `-p` to get dependencies from Nixpkgs. You can also use a Nix expression to build your own dependencies. For example, the Python example could have been written as:

```bash
#! /usr/bin/env nix-shell 
#! nix-shell deps.nix -i python
```

where the file `deps.nix` in the same directory as the `#!`-script contains:

```nix
with import <nixpkgs> {};  
runCommand "dummy" { 
	buildInputs = [ python pythonPackages.prettytable ]; 
} ""
```
