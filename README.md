# mkosi-built Images for systemd-machined

Minimal OS container images built with [**mkosi**](https://github.com/systemd/mkosi) for **systemd-machined**.

## Available images

| Image            | Architectures |
|------------------|---------------|
| `centos-10`      | x86-64, arm64 |
| `fedora-44`      | x86-64, arm64 |
| `fedora-rawhide` | x86-64, arm64 |
| `rhel-ubi-10`    | x86-64, arm64 |

## Usage

### Import an image

Import one of the images listed in the table above, optionally giving the container a name:

```sh
run0 importctl pull-tar -mN --verify=checksum \
  https://github.com/albertescanes/machined-images/releases/download/latest/<image>_$(systemctl show -P Architecture).tar.xz [ctname]
```

### Start and enter the container

```sh
run0 machinectl start <ctname>
run0 machinectl shell <ctname>
```

### Use host networking

To disable private networking and make the container use host networking instead, create a `.nspawn` settings file for the container:

```sh
run0 machinectl edit <ctname>
```

This opens an editor for `/etc/systemd/nspawn/<ctname>.nspawn`. Add the following:

```ini
[Network]
VirtualEthernet=no
```

Then restart the container machine for the change to take effect:

```sh
run0 machinectl reboot <ctname>
```
