# NixOS
## Introduction

NixOS is a modern, open-source operating system built on the Nix package manager. It is designed to provide a declarative and purely functional approach to system configuration and package management. NixOS stands out from other Linux distributions due to its unique features and philosophies.

### Key Features

### 1. **Declarative System Configuration**

NixOS employs a declarative configuration model. System configuration is described in a configuration file, typically `/etc/nixos/configuration.nix`. This approach allows users to define the desired state of the system explicitly, making it easy to understand and reproduce configurations.

### 2. **Immutable Packages and Rollbacks**

Nix, the package manager used by NixOS, manages packages in an immutable fashion. This immutability ensures that packages do not change after installation, promoting consistency and stability. Additionally, NixOS supports easy rollbacks, enabling users to revert to a previous system configuration if needed.

### 3. **Atomic Upgrades**

NixOS supports atomic upgrades, meaning system updates are performed as a single, atomic transaction. This ensures that either all updates are applied successfully, or none of them are, preventing potential system inconsistencies.

### 4. **Functional Package Management**

Packages in NixOS are built using a functional approach. Each package is isolated and built in its own environment, with all dependencies specified explicitly. This eliminates dependency conflicts and allows for reproducible builds.

### 5. **Nix Expression Language**

The Nix package manager and NixOS use a unique functional programming language for configuration called the Nix Expression Language (Nix). Nix provides a powerful and flexible way to describe packages and system configurations.

### Use Cases

- **Development Environments**: NixOS is well-suited for creating consistent and isolated development environments, making it easier for developers to manage dependencies.
    
- **Server Environments**: Its declarative configuration and atomic upgrades make NixOS a strong choice for server setups where reliability and maintainability are crucial.
    
- **Reproducible Systems**: NixOS is ideal for creating reproducible systems, ensuring that a system's state can be replicated across different machines.
    
### Point of use
1. Linux distribution based on Nix Package manager
2. Supports declarative reproducible system configuration
3. "Unbreakable"
	- Boot to specific configuration generations. (as mentioned above -> reproducible)
4. nix-store: no /lib & /usr/lib. almost non-existant /bin & /usr/bin -> /nix/store
5. nix-env: install packages at user level without having to change system state

### Conclusion

NixOS provides a unique and powerful approach to operating system configuration and package management. Its declarative model, immutable packages, and functional design make it a compelling choice for those seeking reliability, consistency, and ease of management in their computing environments. Whether for development or production use, NixOS offers a fresh perspective on how we interact with and manage operating systems.

## Getting Started
- NixOS Website
	- [NixOS](https://nixos.org/)
	- [Manual](https://nixos.org/manual/nixos/stable/) Downloads -> NixOS -> More -> Manual
	- [Unstable](https://releases.nixos.org/?prefix=nixos/unstable/) Downloads -> NixOS -> More -> also available
- Burn ISO
- Partitioning
	- GUI: gparted
		- install gparted
			```shell 
			nix-env -iA nixos.gparted
			```
		- Device -> Create partition table -> msdos (legacy boot) (old computer / one partition / not dual boot)
										->gpt (uefi boot) (pc>2TO)
		- Add new partition -> fileSystem: ext4/linux-swap
		- Manage flags -> boot for ext4 (possible not necessary)
		- label partitions (useful later)
	- Terminal: Parted
		These step are for a fresh installation. Not dual boot
		```shell
		parted /dev/sda -- mklabel msdos (gpt for uefi)
		```
		```shell
		parted /dev/sda -- mkpart primary 1MIB 100% (512MIB -8GIB for uefi)
		```
		```shell
		parted /dev/sda -- mkpart primary linux-swap -8GIB 100%
		```
		Extra for UEFI
		```shell
		parted /dev/sda -- mkpart ESP fat32 1Mib 512MIB
		```
		```shell
		parted /dev/sda -- set 3 esp on
		```

		```shell
		mkfs.ext4 -L nixos /dev/sda1
		```
		```shell
		mkswap -L swap /dev/sda2
		```
		Extra for UEFI
		```shell
		mkfs.fat -F 32 -n boot /dev/sda3
		```
	- Mounting
		```shell
		mount /dev/disk/by-label/nixos /mnt
		```
		Extra for UEFI
		```shell
		mkdir -p /mnt/boot
		```
		```shell
		mount /dev/disk/by-label/boot /mnt/boot
		```

		```shell
		swapon /dev/sda2
		```
		If you don't know the name of your disk:
		```shell
		lsblk -f
		```
## Initial configuration
- Generate
	- Generate default configuration:
		```shell
		nixos-generate-config --root /mnt
		```
	- Location:
		```shell
		cd /mnt/etc/nixos/
		```
- Configuration.nix
	- General
		- Argument on how to evaluate config:
			\[config, pkgs, ...]:
		- Pull in other files used within the config:
			import = \[./hardware-configuration.nix]:
	- Boot
		- Legacy
			- Only viable if dualbooting linux distributions
			```shell
			# Default Grub setup
			boot.loader.grub.enable = true;
			boot.loader.grub.version = 2;
			boot.loader.grub.device = "/dev/vda": # if virtual machine
			# Dual booting made easy (Optional)
			boot.loader.grub.userOSProber = true;
			# Dual booting made a bit harder (Extra Optional)
			boot.loader.grub.extraEntries = ''
				menuentry "Windows 10" {
					chainloader (hd0,1)+1
				}
			'';
			```
			OR
			```shell
			boot.loader.grub = {
				enable = true;
				version = 2;
			};
			```
		- UEFI
		- Extras
	- Networking
	- Internationalisation
	- Display Managers/desktop Environments/Window Managers
	- Hardware
	- Users
	- Packages
	- StateVersion
- Hardware-configuration.nix
## Installation
## Declaring packages, services, settings, etc
## Extras
# Home-Manager
## Introduction
## Getting Started
## Configuration
## Dotfiles
# Flakes
## Introduction
## Getting Started
## Configuration
## Updating
## Flake on fresh install

# Personal Config
# Resources
## Documentation
1. [NixOS Website](https://nixos.org/)
2. [NixOS Learn](https://nixos.org/learn)
3. [NixOS Manual](https://nixos.org/manual/nixos/stable/)
4. [NixOS Wiki](https://nixos.wiki/wiki/Main_Page)
5. [Nix Pills](https://nixos.org/guides/nix-pills/)
6. [Home-Manager Github](https://github.com/nix-community/home-manager/)
7. [Home-Manager Manual](https://nix-community.github.io/home-manager/)
8. [Home-Manager Appendix A](https://nix-community.github.io/home-manager/options.html)
9. [Home-Manager Appendix B](https://nix-community.github.io/home-manager/nixos-options.html)
10. [List of reference configuration](https://nixos.wiki/wiki/Configuration_Collection)
11. [Exemple Flake](https://github.com/MatthiasBenaets/nixos-config)
## Video
![Link Setup guide](https://www.youtube.com/watch?v=AGVXJ-TIv3Y)
![NixOS First Installation](https://www.youtube.com/watch?v=_Z32SYFbxpw)