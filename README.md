# machined-images
Minimal container image builds for **systemd-machined**.

## Usage
Import the image of the desired distribution as a machine (see [Available images](#available-images) below):

```sh
importctl pull-tar -mN --verify=checksum \
https://github.com/albertescanes/machined-images/releases/download/latest/{image}.$(arch).tar.xz [ctname]
```

Edit and apply the nspawn container settings file:

```sh
run0 machinectl edit {ctname}
```

This installs the settings file to `/etc/systemd/nspawn/{ctname}.nspawn`.  
Default settings:

- `[Exec] Ephemeral=no`: If set to `yes`, the container is run with a temporary snapshot of its file system that is removed immediately when the container terminates.
- `[Network] VirtualEthernet=no`: Makes the container use host networking instead of creating a virtual Ethernet connection between host and the container.

For full details on available options, see the [man page](https://www.freedesktop.org/software/systemd/man/latest/systemd.nspawn.html).

Start and access the container machine:

```sh
machinectl start {ctname}
machinectl shell {ctname}
```

## Available images
The following images are available: `centos`, `debian`, `fedora`, and `rhel-ubi`.

All images are built for both `x86_64` and `aarch64`.
