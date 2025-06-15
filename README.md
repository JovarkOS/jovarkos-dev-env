# JovarkOS Development Environment
*Clone only one git repo to start development quickly*

## Install dependancies

*This assumes you have a solid installation of Arch Linux. We use the default Arch image that Linode provides on their VPS'.*
```bash
sudo pacman -Sy make git nano wget curl archiso
```

## Get Started
```bash
git clone --recurse-submodules -j$(nproc) https://github.com/jovarkos/jovarkos-dev-env.git
cd jovarkos-dev-env
```

(Recursively get submodules and use as many cores as possible to speed up the cloning process)

### Install jbuild

```bash
cd jovarkos-jbuild
make
```

### Copy the "releng" image profile

```bash
cd ../jovarkos-config
jbuild -p releng
```

(Copy the releng profile from the `/usr/share/archiso/configs/` directory. We do not modify this profile as it will be overwritten as `archiso` is updated.)
For more information, please check out the [Arch Wiki: Archiso #Prepare_a_custom_profile](https://wiki.archlinux.org/title/Archiso#Prepare_a_custom_profile) and [GitLab ArchLinux: archiso/docs/README.profile.rst](https://gitlab.archlinux.org/archlinux/archiso/-/blob/master/docs/README.profile.rst) pages.

Our customizations will go into `jovarkos-dev-env/jovarkos-config/jovarkos-archlive`, then get merged into the releng `jovarkos-dev-env/jovarkos-config/archlive` folder in the build process. Customize as needed, then do

```bash
cd ..
# We are now in the jovarkos-dev-env/ directory
jbuild -b
```

The script will run, pausing to allow you to configure the system before zipping into an ISO file. Requires sudo access (see issue #1). 


