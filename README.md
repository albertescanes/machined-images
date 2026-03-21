# machined-images
Minimal container image builds for **systemd-machined**.

## Usage
Import the image of the desired distribution as a machine (see [Available images](#available-images) below).  
The example uses `fedora-rawhide` and names the machine `my-fedora`:

```sh
importctl pull-tar -mN --verify=checksum \
  https://github.com/albertescanes/machined-images/releases/download/latest/fedora-rawhide_$(systemctl show -P Architecture).tar.xz my-fedora
```

Edit and apply the nspawn container settings file:

```sh
run0 machinectl edit my-fedora
```

This installs the settings file to `/etc/systemd/nspawn/my-fedora.nspawn`.  
Default settings:

- `[Exec] Ephemeral=no`: If set to `yes`, the container is run with a temporary snapshot of its file system that is removed immediately when the container terminates.
- `[Network] VirtualEthernet=no`: Makes the container use host networking instead of creating a virtual Ethernet connection between host and the container.

For full details on available options, see the [man page](https://www.freedesktop.org/software/systemd/man/latest/systemd.nspawn.html).

Start and access the container machine:

```sh
machinectl start my-fedora
machinectl shell my-fedora
```

## Available images
The following images are available:

- `centos-10`
- `centos-9`
- `debian-forky`
- `debian-sid`
- `debian-trixie`
- `fedora-43`
- `fedora-rawhide`
- `rhel-ubi-10`
- `rhel-ubi-9`

All images are built for both `x86-64` and `arm64`.
