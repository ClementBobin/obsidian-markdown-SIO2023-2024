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
			systemctl start display-manager
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
			- Used for larger boot drives and dual booting with windows
				```bash
				# Default UEFI setup
				boot.loader.systemd-boot.enable = true;
				boot.loader.efi.canTouchEfiVariables = true;
				# Dual booting using grub
				boot.loader = {
					efi = {
						canTouchEfiVariables = true;
						efiSysMountPoint = "/boot/efi"; # /boot will probably work too 
					};
					grub = { # Using grub means first 2 lines can be removed
						enable = true;
						#device = ["nodev"];     # Generate boot menu but not actually installed
						devices = ["nodev"];     # Install grub
						efiSupport = true;
						useOSProber = true;      # Or use extraEntries like seen with legacy
					};  # OSProber will probably not find windows partition on first install
				};
				```
		- Extras
			```bash
			{ pkgs, ... }:
			
			{
				boot = {
					kernelPackages = pkgs.linuxPackages_latest; # Get latest kernel
					initrd.kernelModules = ["amdgpu"]; # More on this later on (setting it for xserver)
					loader = {
						#efi = {
							#canTouchEfiVariables = true;
							#efiSysMountPoint = "/boot/efi";
						#};
						grub = {
							#enable = true;
							#devices = ["nodev"];
							#efiSupport = true;
							#useOSProber = true;
							configurationLimit = 5; #Limit stored system "backup configuration".
						}; #Also exists for systemd-boot
						timeout = 5; #Work for grub and efi boot, time before auto-boot
					};
				};
			}
			```
	- Networking
		- Uncomment: networking.hostName="nixos";
			- networking.hostName="nixos";
			- networking.wireless.enable = true; or networking.networkmanager.enable = true;               // for laptop or wireless chose one 
		- Network card details 
		
		//could.be.moved.to.hardware-configuration.nix
		- Deprecated but keep: networking.useDHCP = false;
		- Just internet via ethernet: networking.interfaces.<networkcard-id%>.useDHCP = true;
		
		- Extra
			- Can be transfer in Configuration.nix
			```bash
			networking = {
				#hostName = "nixos";
				#networkmanager.enable = true;
				#wireless.enable = true;
				interfaces = {
					<networkcard-id%> = {
						#useDHCP = true;
						#ipv4.addresses = [ { # Ofcourse not compatible with networkmanager 
							#address = "192.168.0.50";
							#prefixLength = 24;
						#}];
					};
				};
				defaultGateway = "192.168.0.1";
				nameservers = [ "1.1.1.1" ];
			};
			```
	- Internationalisation
		*Where am i? How do i work*
		```bash
		# Clock
		time.timeZone = "Europe/Paris";
		# Locale
		i18n.defaultLocale = "en_US.UTF-8";
		i18n.extraLocaleSettings = {
			LC_TIME = "nl_FR.UTF-8";
			LC_MONETARY = "nl_FR.UTF-8";
		};
		# TTY layout
		console = {
			font = "...";
			keymap = "azerty"; # us / fr /azerty /etc... 
		};
		# XServer layout (possibly also sets console now)
		services.xserver.layout = "azerty" # us / fr /azerty /etc...
		# Extra keyboard settings:
		services.xserver.xkbOptions = "eurosign:e"; # For exemple adds €
		```
	- Display Managers/desktop Environments/Window Managers
		- *Default*
			```bash
			services.xserver.enable = true;
			services.xserver.displayManager.sddm.enable = true;
			services.xserver.desktopManager.plasma5.enable = true;
			```
		- *Customized*
			```bash
			services = {
				xserver = { 
					enable = true;
					displayManager = {
						lightdm.enable = true; # Whether to enable lightdm as the display manager.
						defaultSession = "none+bspwm"; # Graphical session to pre-select in the session chooser "desktopManager + windowManager" or if don't want a backend desktop manager "none + windowManager"
					};
					desktopManager.xcfe.enable = true; # xcfe desktop environement
					windowManager.bspwm.enable = true; # enable bspwm.
				};
			};
			```
	- Hardware
		- Audio & Bluetooth
			- PulseAudio Wiki
			- Bluetooth Wifi (+ configuring it with PulseAudio)
			
			- Example
				```bash
				{ pkgs, ... }:
				
				{
					sound = {
						enable = true;
						mediaKeys.enable = true;
					};
					hardware.bluetooth = {
						enable = true;
						hsphfpd.enable = true; # HSP  HFS daemon
						settings = {
							General = {
								Enable = "Source,Sink,Media,Socket";
							};
						};
					};
				}
				```
		- Touchpad
			- Libinput Options
			```bash
			services.xserver.libinput = {
				enable = true;
				#tapping = true;
				#naturalScrolling = true;
				# ...
			}
			```
	- Users
		```bash
		users.users.<name> = {
			isNormalUser = true;
			extraGroups = [ "wheel" "video" "audio" "networkmanager" "lp" "scanner" ]
			#initialPassword = "password"; #not recomanded
			#shell = pkgs.zsh;
		}
		```
	- Packages
		```bash
		environment.systemPackages = with pkgs; [
			vim
			wget
			git
			#pkgs.firefox
			firefox
		];
		```
	- StateVersion
		- No need to touch this.
		- Nothing to do with the version of the system.
		- Just tells the version of state/config
		- Can be updates to a stable version if you are really sure.
- Hardware-configuration.nix
	- Generate
		- Also get automatically generated with:
			`# nixos-generate-config --root /mnt`
		- Should detect mounted drives, device parts, kernelModules, etc... that are needed
		- Can be deleted and regenerated with:
			`# nixos-generate-config`
		- Reproduction
			- This represent the root
			```bash
			fileSystems."/" =
			{ device = "/dev/disk/by-label/name"; # change name by the name of your drive
			  fsType = "ext4";
			};
			```
	- File System
		- 
## Installation
- System
	- For initial installation:
		```bash
		nixos-install
		```
	- After applying changes to the config:
		```bash
		nixos-rebuild switch
		```
	- Lastly: set a root password
- Login
	- initialPasword
		- Log in with give password of  `users.users.<users>.initialPassword`
		- then change password
			```bash
			sudo passwd <user>
			```
	- via TTY
		- Ctrl + Alt + F1 -> log in via root
		```bash
		passwd <user>
		```
		- Ctrl + Alt + F7 -> log in via user
## Declaring packages, services, settings, etc
- Options
	- Individually via Nix Package Manager ( not permanent )
		Install: 
		```bash
		nix-env -iA nixos.firefox
		```
		List:
		```bash
		nix-env -q
		```
		Uninstall:
		```bash
		nix-env --uninstall firefox
		```
	- Configuration file: 
		- [[NixOS#Initial configuration]]
- Links
	- [Packages](https://search.nixos.org/packages?channel=unstable&size=50&sort=relevance&type=packages)
	- [Options](https://search.nixos.org/options?channel=unstable&size=50&sort=relevance&type=packages)
	```bash
	man configuration.nix
	```
- Declaring Packages
	*Installed Systemwide*
	```bash
	environment = {
		systemPackages = with pkgs; [
			plex
			superTux
		];
	};
	
	nixpkgs.config.allowUnfree = true;
	```
- Declaring Option
	*Some packages will also have options to configure it further*
	```bash
	services = {
		plex = {
			enable = true;
			openFirewall = true;
		};
	};
	```
- Variables
	*Values that can change often or you want to use multiple times*
	```nix
	let
		rofi-theme = {
			"*" = {
				bg = "#FFFFFF";
			};
		};
	in
	{
		programs.rofi = {
			enable = true;
			theme = rofi-theme;
		};
	};
	```
- Overlays
	*Change packages or add new packages to existing in nix*
	- [Overlays wiki](https://nixos.wiki/wiki/Overlays)
	```bash
	nixpkgs.overlays = [
		(self: super: {
			sl = super.sl.overrideAttrs (old: {
				src = super.fetchFromGitHub {
					owner = 'mtoyoda';
					repo = "sl";
					rev = "923e7d7ebc5c1f009755bdeb789ac25658ccce03";
					sha256 = "0000000000000000000000000000000000000000000000000000"; # if use flakes
				};
			});
		})
	
		(self: super: {
			discord = super.discord.overrideAttrs (
				_: { src = builtins.fetchTarball {
					url = "https: //discord.com/api/download?platform=linux&format=tar.gz";
					sha256 = "0000000000000000000000000000000000000000000000000000"; # if use flakes
				}; }
			);
		})
	];
	# Should be the same for home-manager
	```
- Applying
	```bash
	sudo nixos-rebuild switch
	```
## Extras
- Updating & Upgrading
	- Nix-channel
		A. 
		```bash
		nix-channel --add https://nixos.org/channels/nixos-21.11
		```
		OR
		B.
		```bash
		nix-channel --update
		```
		2. Next rebuild, use the --upgrade flag:
		```bash
		sudo nixos-rebuild --upgrade
		```
		
		D. Installed through nix-env:
		```bash
		nix-env -u '*'
		```
	- Configuration.nix
		```nix
		system.autoUpgrade = {
			enable = true;
			channel = "https://nixos.org/channels/nixos-unstable";
			dates = "weekly";
		};
		```
- Garbage Collection
	- Command line
		- Remove undeclared packaged, dependencies and symlinks:
			```bash
			nix-collect-garbage
			```
		- Remove above of older generations:
			```bash
			nix-collect-garbage --delete-olg
			```
			List Generations
			```bash
			nix-env --list-generations
			```
		- Remove specific generations or older than ... days:
			```bash
			nix-env --delete-generations 14d
			```
			```bash
			nix-env --delete-generations 10 11
			```
			Optimize store:
			```bash
			nix-store --gc
			```
		- All in one:
			```bash
			nix-collect-garbage -d
			```
	- Configuration.nix
		```nix
		nix = {
			settings.auto-optimise-store = true;
			gc = {
				automatic = true;
				dates = "monthly";
				options = "--delete-older-than 7d";
			};
		};
		```
# NixOS Server 
## Introduction 
NixOS is a modern, open-source operating system that provides a declarative and purely functional approach to system configuration and package management. This guide will walk you through setting up a NixOS server. 
## Getting Started 
Before you begin with the installation and configuration, make sure you have the necessary hardware and a basic understanding of Linux concepts and server management. 
![[NixOS#NixOS#Initial configuration]]]
## Initial Configuration 
Ensure that you have a clear understanding of the system requirements and the specific configuration you want to achieve for your NixOS server. Decide on the necessary hardware specifications, network settings, and other relevant parameters. 
## Installation 
Follow these steps to install NixOS on your server: 
![[NixOS#NixOS#Installation]]]
## Extras 
Explore additional features and optimizations for your NixOS server: 
- Setting Up Services 
	Configure and manage services on your NixOS server, such as web servers, databases, and more. 
- Customizing Packages 
	Learn how to customize packages and manage dependencies using the Nix package manager. 
- Security Measures 
	Implement security best practices to protect your NixOS server from potential threats. 
-  Monitoring and Logging Set up monitoring tools and log management to keep track of server performance and activities. 
# Home-Manager
## Introduction
- It's like configuration.nix, but for the user environment.
- Plenty more option to declare packages
- Also a better way to manage dotfiles
- "sudo" nix but home-manager "its not a sudo so only for the user and more option"
## Getting Started
- Home-Manager Website
	- [Github](https://github.com/nix-community/home-manager/)
	- [Manual](https://nix-community.github.io/home-manager/)
	- [Appendix A](https://nix-community.github.io/home-manager/options.html)
	- [Appendix B](https://nix-community.github.io/home-manager/nixos-options.html)
- Setup
	- Initial
		*As a user*
		- Add the channel: *need  to be run with root privileges if you want to use the NixOS Module*
			Unstable version
			```bash
			nix-channel --add https://github.com/nix-community/home-manager/archive/master.tar.gz home-manager
			```
			or LTS
			```bash
			nix-channel --add https://github.com/nix-community/home-manager/archive/release-21.11.tar.gz home-manager
			```
		- `nix-channel --update`
		- just to be sure, relog
	- NixOS Module
		*Add to configuration.nix*
		```nix
		let
		in
		{
			import = [ <home-manager/nixos> ];
			
			users.users.<name> = {
				isNormalUser = true;
			}
			
			home-manager.users.<name> = { pkgs, ... }: {
				# declared packages. for example:
				home.packages = with pkgs; [ 
					atool 
					httpie 
				];
			};
		}
		```
	- Standalone
		- Installation
			```bash
			nix-shell '<home-manager>' -A install
			```
		- Configuration file:
			```bash
			cd ~/.config/nixpkgs/home.nix
			```
		- Rebuild home-manager
			```bash
			home-manager switch
			```
## Configuration
- Links
	- [Home-Manager Options]
	```bash
	man home-configuration.nix
	```
- Declare user packages
	```nix
	home.packages = with pkgs; [
		firefox
	];
	
	services.dunst = { # if you use a services, you need to manually enble them
		enable = true;
	};
	```
- Applying
	```bash
	home-manager switch
	```
## Dotfiles
- Copy/Symlink
	- Existing config files
		*For exemple, randomly nicked files used by other (who don't use NixOS)*
		```nix
		home.file = {
			".config/alacritty/alacritty.yml".text =  ''
				{"font":{"bold":{"style":"bold"}}}
			'';
		};
		```
		can be done in Home-Manager or in a Nix Modules
		>If not declared and for exeple alacrity gets a big update and the way they set up their yaml file is different or they use another way of configuring this will break
		
	- Stored files (also with no link to NixOS)
		```nix
		home.file.".domm.d" = {
			source ./doom.d; # Where is it
			recurcive = true; # Link any original file or link
			onChange = buildins.readFile ./doom.sh; # if change 
		};
		home.file.".config/polybar/script/mic.sh" = {
			source = ./mic.sh;
			executable = true;
		};
		```
- Declared
	```nix
	{
		xsession = {
			windowManager = {
				baspwm = {
					enable = true;
					rules = {
						"Emacs" = {
							desktop = "3";
							follow = true;
							state = "tiled";
						};
						".blueman-manager-wrapped" = {
							state = "floating";
							sticky = true;
						};
					};
				};
			};
		};
	}
	```
# Flakes
## Introduction
- Flakes is an "upcoming feature" of the Nix package manager.
- Specify code dependencies declaratively (will be stored in flake.lock) // save all core dependencies
	- For exemple: home-manager
- Rebuilding and updating whole system made easy
- Very useful tool to build your own config
	- Multiple configs in one
	- People with github dotfiles will feel right at home
## Getting Started
- [Flakes Wiki]()
- Setup
	- Configuration.nix
		```nix
		nix = {
			package = pkgs.nixFlakes;
			extraOptions = "experimental-features = nix-command flakes"
		};
		```
	- Generate 
		*This command will generate a flake.nix and flake.lock file*
		- pick a location to store in your system `mkdir flake`
		```bash
		nix flake init
		```
	- Inputs and Outputs
		- Inputs
			*attribute set of all the dependecies used in the flake*
			```nix
			inputs = {
				nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
			};
			```
		- Outputs
			*function of an argument that uses the inputs for reference*
			- Configure what you imported 
			- Can be pretty much anything: Packages / configurations /modules / etc...
## Configuration
- NixOS
	- Flake.nix
		```nix	
		inputs = {
			nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
			#nixpkgs-unstable.url = "github:nixos/nixpkgs/nixospkgs-unstable";
		};
		outputs = { nixpkgs, home-manager, ... }:
			let
				system = "x86_64-linux";
				pkgs = import nixpkgs {
					inherit system;
					config.allowUnfree = true;
				};
				
				lib = nixpkgs.lib;
			in {
				nixosConfigurations = {
					<user> = lib.nixosSystem {
						inherit system;
						modules = [ ./configuration.nix ];
					};
					#<second user> = lib.nixosSystem {
						#inherit system;
						#modules = [ ./configuration.nix ];
					#};
				};
			}
		```
	- Build
		*a ".(#)" will just build host found in location*
		*specify host with ".#<host%>" appended*
		- *optional* `cp /etc/nixos/* <flake location>`
		```bash
		nixos-rebuild build --flake .#
		```
		or
		```bash
		nixos-rebuild switch --flake .#
		```
		
		```bash
		sudo nixos-rebuild switch --flake .#
		```
	- sha256
		```nix
		nixpkgs.overlays = [
			(self: super: {
				discord = super.discord.overrideAttrs (
					_: { src = builtins.fetchTarball {
						url = "https: //discord.com/api/download?platform=linux&format=tar.gz";
						sha256 = "0000000000000000000000000000000000000000000000000000"; # if use flakes 52.0
					}; }
				);
			})
		];
		```
		after rebuild
		```bash
		sudo nixos-rebuild switch --flake .#
		```
		it will display the correct sha256 and should be replace by the 52 0
- Home-Manager
	- Flake.nix
		- Seperate
			```nix
			{
				inputs = {
					...
					home-manager = {
						url = github:nix-community/home-manager;
						inputs.nixpkgs.follows = "nixpkgs";
					};
				};
				outputs = { self, nixpkgs, home-manager, ... }:
					let
						...
					in {
						hmConfig = {
							home-manager.lib.homeManagerConfiguration {
								inherit system pkgs;
								username = "<user>";
								homeDirectory = "/home/<user>";
								#stateVersion = "22.05"; # If there is any complaining about stateVersions, specifically state here.
								configuration = {
									imports = [
										/home/<user>/.config/home/home.nix
									];
								};
							};
						};
					};
			}
			```
		- Inside nixosConfigurations
			```nix
			{
				inputs = {
					...
					home-manager = {
						url = github:nix-community/home-manager;
						inputs.nixpkgs.follows = "nixpkgs";
					};
				};
				outputs = { self, nixpkgs, home-manager, ... }:
					let
						...
					in {
						nixosConfigurations = {
							<user> = lib.nixosSystem {
								inherit system pkgs;
								modules = [
									./configuration.nix
									
									home-manager.nixosModules.home-manager {
										home-manager.useGlobalPkgs = true;
										home-manager.useUserPackages = true;
										home-manager.user.<user> = {
											imports = [ ./home.nix ];
										}; 
									};
								];
							};
						};
					};
			}
			```
	- build
		```bash
		nix build .#hmConfig.<user>.activationPackage
		```
		```bash
		./result/activate
		```
## Updating
*this will update the flake.lock file*
```bash
nix flake update #--recreate-lock-file
```
Now rebuild and switch
## Flake on fresh install
- Boot into ISO
```bash
sudo su
nix-env -iA nixos.git
git clone <repo url> /mnt/<path>
nixos-install --flake .#<host>
reboot
/* login */
sudo rm -r /etc/nixos/configuration.nix
/* move build to desired location */
```
# Personal Config
[Exemple Flake](https://github.com/MatthiasBenaets/nixos-config)
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
- Best install
![Link Setup guide](https://www.youtube.com/watch?v=AGVXJ-TIv3Y)
- Normal install
![NixOS First Installation](https://www.youtube.com/watch?v=_Z32SYFbxpw)
