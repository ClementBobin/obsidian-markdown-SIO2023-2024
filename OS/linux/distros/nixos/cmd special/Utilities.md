# General
## Common options:
![[NixOS Commun store cmd#[Common Options](https //nixos.org/manual/nix/unstable/command-ref/nix-store/add-fixed common-options)]]
## Common environment variables
![[NixOS Commun store cmd#[Common Environment Variables](https //nixos.org/manual/nix/unstable/command-ref/nix-store/add-fixed common-environment-variables)]]
## XDG Base Directories:
![[NixOS Commun store cmd#[XDG Base Directories](https //nixos.org/manual/nix/unstable/command-ref/nix-store/add xdg-base-directories)]]
![]()
# nix-channel
## [Name](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#name)

`nix-channel` - manage Nix channels

## [Synopsis](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#synopsis)

```bash
nix-channel {--add url [_name_] | --remove _name_ | --list | --update [_names…_] | --list-generations | --rollback [_generation_] }
```

## [Description](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#description)

Channels are a mechanism for referencing remote Nix expressions and conveniently retrieving their latest version.

The moving parts of channels are:

- The official channels listed at [https://nixos.org/channels](https://nixos.org/channels)
- The user-specific list of [subscribed channels](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#subscribed-channels)
- The [downloaded channel contents](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#channels)
- The [Nix expression search path](https://nixos.org/manual/nix/unstable/command-ref/conf-file#conf-nix-path), set with the [`-I` option](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#opt-i) or the [`NIX_PATH` environment variable](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#env-NIX_PATH)

> **Note**
> 
> The state of a subscribed channel is external to the Nix expressions relying on it. This may limit reproducibility.
> 
> Dependencies on other Nix expressions can be declared explicitly with:
> 
> - [`fetchurl`](https://nixos.org/manual/nix/unstable/language/builtins#builtins-fetchurl), [`fetchTarball`](https://nixos.org/manual/nix/unstable/language/builtins#builtins-fetchTarball), or [`fetchGit`](https://nixos.org/manual/nix/unstable/language/builtins#builtins-fetchGit) in Nix expressions
> - the [`-I` option](https://nixos.org/manual/nix/unstable/command-ref/opt-common#opt-I) in command line invocations

This command has the following operations:

- `--add` _url_ [_name_]  
    Add a channel _name_ located at _url_ to the list of subscribed channels. If _name_ is omitted, default to the last component of _url_, with the suffixes `-stable` or `-unstable` removed.
    
    > **Note**
    > 
    > `--add` does not automatically perform an update. Use `--update` explicitly.
    
    A channel URL must point to a directory containing a file `nixexprs.tar.gz`. At the top level, that tarball must contain a single directory with a `default.nix` file that serves as the channel’s entry point.
    
- `--remove` _name_  
    Remove the channel _name_ from the list of subscribed channels.
    
- `--list`  
    Print the names and URLs of all subscribed channels on standard output.
    
- `--update` [_names_…]  
    Download the Nix expressions of subscribed channels and create a new generation. Update all channels if none is specified, and only those included in _names_ otherwise.
    
- `--list-generations`  
    Prints a list of all the current existing generations for the channel profile.
    
    Works the same way as
    
    ```bash
    nix-env --profile /nix/var/nix/profiles/per-user/$USER/channels --list-generations
    ```
    
- `--rollback` [_generation_]  
    Revert channels to the state before the last call to `nix-channel --update`. Optionally, you can specify a specific channel _generation_ number to restore.
## [Files](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#files)

`nix-channel` operates on the following files.

### [Channels](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#channels)

A directory containing symlinks to Nix channels, managed by [`nix-channel`](https://nixos.org/manual/nix/unstable/command-ref/nix-channel):

- `$XDG_STATE_HOME/nix/profiles/channels` for regular users
- `$NIX_STATE_DIR/profiles/per-user/root/channels` for `root`

[`nix-channel`](https://nixos.org/manual/nix/unstable/command-ref/nix-channel) uses a [profile](https://nixos.org/manual/nix/unstable/command-ref/files/profiles) to store channels. This profile contains symlinks to the contents of those channels.

### [Subscribed channels](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#subscribed-channels)

The list of subscribed channels is stored in

- `~/.nix-channels`
- `$XDG_STATE_HOME/nix/channels` if [`use-xdg-base-directories`](https://nixos.org/manual/nix/unstable/command-ref/conf-file#conf-use-xdg-base-directories) is set to `true`

in the following format:

```bash
<url> <name> 
...
```

## [Examples](https://nixos.org/manual/nix/unstable/command-ref/nix-channel#examples)

Subscribe to the Nixpkgs channel and run `hello` from the GNU Hello package:

```bash
$ nix-channel --add https://nixos.org/channels/nixpkgs-unstable 
$ nix-channel --list 
nixpkgs https://nixos.org/channels/nixpkgs 
$ nix-channel --update 
$ nix-shell -p hello --run hello 
hello
```

Revert channel updates using `--rollback`:

```bash
$ nix-instantiate --eval '<nixpkgs>' --attr lib.version 
"22.11pre296212.530a53dcbc9" 

$ nix-channel --rollback 
switching from generation 483 to 482 

$ nix-instantiate --eval '<nixpkgs>' --attr 
lib.version "22.11pre281526.d0419badfad"
```

Remove a channel:

```bash
$ nix-channel --remove nixpkgs 
$ nix-channel --list
```
# nix-collect-garbage
## [Name](https://nixos.org/manual/nix/unstable/command-ref/nix-collect-garbage#name)

`nix-collect-garbage` - delete unreachable [store objects](https://nixos.org/manual/nix/unstable/glossary#gloss-store-object)

## [Synopsis](https://nixos.org/manual/nix/unstable/command-ref/nix-collect-garbage#synopsis)

```bash
nix-collect-garbage [--delete-old] [-d] [--delete-older-than _period_] [--max-freed _bytes_] [--dry-run]
```
## [Description](https://nixos.org/manual/nix/unstable/command-ref/nix-collect-garbage#description)

The command `nix-collect-garbage` is mostly an alias of [`nix-store --gc`](https://nixos.org/manual/nix/unstable/command-ref/nix-store/gc). That is, it deletes all unreachable [store objects](https://nixos.org/manual/nix/unstable/glossary#gloss-store-object) in the Nix store to clean up your system.

However, it provides two additional options, [`--delete-old`](https://nixos.org/manual/nix/unstable/command-ref/nix-collect-garbage#opt-delete-old) and [`--delete-older-than`](https://nixos.org/manual/nix/unstable/command-ref/nix-collect-garbage#opt-delete-older-than), which also delete old [profiles](https://nixos.org/manual/nix/unstable/command-ref/files/profiles), allowing potentially more [store objects](https://nixos.org/manual/nix/unstable/glossary#gloss-store-object) to be deleted because profiles are also garbage collection roots. These options are the equivalent of running [`nix-env --delete-generations`](https://nixos.org/manual/nix/unstable/command-ref/nix-env/delete-generations) with various augments on multiple profiles, prior to running `nix-collect-garbage` (or just `nix-store --gc`) without any flags.

> **Note**
> 
> Deleting previous configurations makes rollbacks to them impossible.

These flags should be used with care, because they potentially delete generations of profiles used by other users on the system.

### [Locations searched for profiles](https://nixos.org/manual/nix/unstable/command-ref/nix-collect-garbage#locations-searched-for-profiles)

`nix-collect-garbage` cannot know about all profiles; that information doesn't exist. Instead, it looks in a few locations, and acts on all profiles it finds there:

1. The default profile locations as specified in the [profiles](https://nixos.org/manual/nix/unstable/command-ref/files/profiles) section of the manual.
    
2. > **NOTE**
    > 
    > Not stable; subject to change
    > 
    > Do not rely on this functionality; it just exists for migration purposes and is may change in the future. These deprecated paths remain a private implementation detail of Nix.
    
    `$NIX_STATE_DIR/profiles` and `$NIX_STATE_DIR/profiles/per-user`.
    
    With the exception of `$NIX_STATE_DIR/profiles/per-user/root` and `$NIX_STATE_DIR/profiles/default`, these directories are no longer used by other commands. `nix-collect-garbage` looks there anyways in order to clean up profiles from older versions of Nix.
    

## [Options](https://nixos.org/manual/nix/unstable/command-ref/nix-collect-garbage#options)

These options are for deleting old [profiles](https://nixos.org/manual/nix/unstable/command-ref/files/profiles) prior to deleting unreachable [store objects](https://nixos.org/manual/nix/unstable/glossary#gloss-store-object).

- [`--delete-old`](https://nixos.org/manual/nix/unstable/command-ref/nix-collect-garbage#opt-delete-old) / `-d`  
    Delete all old generations of profiles.
    
    This is the equivalent of invoking `nix-env --delete-generations old` on each found profile.
    
- [`--delete-older-than`](https://nixos.org/manual/nix/unstable/command-ref/nix-collect-garbage#opt-delete-older-than) _period_  
    Delete all generations of profiles older than the specified amount (except for the generations that were active at that point in time). _period_ is a value such as `30d`, which would mean 30 days.
    
    This is the equivalent of invoking [`nix-env --delete-generations <period>`](https://nixos.org/manual/nix/unstable/command-ref/nix-env/delete-generations#generations-time) on each found profile. See the documentation of that command for additional information about the _period_ argument.
## [Example](https://nixos.org/manual/nix/unstable/command-ref/nix-collect-garbage#example)

To delete from the Nix store everything that is not used by the current generations of each profile, do

```bash
$ nix-collect-garbage -d
```w