- Red Hat has divided Linux into 3 different parts:
  - Kernel
    - lowest layer
    - manage hardware and interactions with everything
    - It has 'boot'
    - on machine startup, computer 'boots' up in either:
      - the BIOS (Basic Input/Output System) or
      - UEFI (universal Extensible firmware interface)
    - these run a bootloader which is called GRUB2 in linux.
    - this bootloader loads the kernal image
    - the kernel initializes and starts up everything required to run (drivers, software)
    - its called an image, but it is a compressed file which gets decompressed into memory and run 
  - System User Space/ Administrative layer:
    - configuration and software installation happened in this layer
    - includes shell or command interpreter
    - includes daemons
      - Daemons run in the background to manage things
      - Example: Network Daemons, which monitors networking and controls interactions with physical or virtual network cards
      - Daemons watch over their own pieces of the system and run without interactions form users
      - They are invisible to users, but are vital
  - Applications:
    - apps are main use of linux
    - apps allow to perform task
    - apps can be anything from graphical interface, editors, web servers, DB servers

- Distributions:
  - Linux has diffeent Distributions or Distro, which is versions packaged up with assciated software, usually from different companies or groups.
  - example: Ubuntu, Debian, Red Hat, SUSE
  - Distro packaged everything required to run that version of Linux together and distribute it.
  - All software that comes with that OS can be installed at the same time.
  - Distros can be different, but they all have in common is the kernel itself.

### To check server kernal age, or for how long the system has been up: ```uptime -p```

- Package Manager or methods to install new software, changed depending on the distro.
- Software is released in packages:
  - Software pckgs available for distro, managed by vendor, consist of multiple files combined into one package for installation using a Package Manager.
    - To install software in Red Hat, use ```yum``` or ```dnf``` commands.
    - In Ubuntu or Debian, use ```apt``` command.
  - Kernel ties it all together.
    - Commong components are supporting system software and libraries.
      - library is a collection of software that is used by computer programs.

- Android OS is modified versions of the linux kernel.
- Mobian: a version of Debian Linux for mobiles.
- Ubuntu Touch: mobile OS by Canonical

- Bloatware: a software a mobile phone provider adds to the phone that most people never use, which slows down the phone and make is less secure.

- Hypervisor: There are 2 types of Virtualization:
  - Type 1: physical computer running hypervisor which talks directly to computer's hardware.
            takes place of host OS
            dedicated machine to run VMs.
            example AWS EC2 and other cloud providers use this method
  - Type 2: Hosted Hypervisor
            Installed software (VMware, Parallels) on an OS that allows to run VM to computer,
            which is running other tasks, such as web surfing, emailcheck, using docs, etc and has its own OS.
            Example: Windows laptop runnign Ubuntu inside VMware.

- Computer providing the hypervisor is called the host.
- VMs that run on the host are called guests.

- Linux can be run on an IBM mainframe.
- Linux is also use with IoT devices.
- Linux is used on Network routers, gateways, switches, Firewalls.
- Linux is used in Smart TVs.


- Root User:
  - High Level of access
  - has the most access of any user
  - can run any command or update any file
  - The best practice is to not use the root user directly
    - this can be resolved by using ```sudo```
    - sudo command allows temporarily to raise the normal user permission to root user access
    - so to update, we use sudo to run updates
