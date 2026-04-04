# mkosi-built Images for systemd-machined

Minimal OS container images built with [**mkosi**](https://github.com/systemd/mkosi) for **systemd-machined**.

## Available images

| Image             | Architectures |
|-------------------|---------------|
| `centos-10`       | x86-64, arm64 |
| `centos-9`        | x86-64, arm64 |
| `debian-forky`    | x86-64, arm64 |
| `debian-sid`      | x86-64, arm64 |
| `debian-trixie`   | x86-64, arm64 |
| `fedora-43`       | x86-64, arm64 |
| `fedora-rawhide`  | x86-64, arm64 |
| `rhel-ubi-10`     | x86-64, arm64 |
| `rhel-ubi-9`      | x86-64, arm64 |
| `ubuntu-noble`    | x86-64, arm64 |
| `ubuntu-resolute` | x86-64, arm64 |

## Usage

### Import an image

Import one of the images listed in the table above, optionally giving the container a name:

```sh
importctl pull-tar -mN --verify=checksum \
  https://github.com/albertescanes/machined-images/releases/download/latest/<image>_$(systemctl show -P Architecture).tar.xz [ctname]
```

### Start and enter the container

```sh
machinectl start <ctname>
machinectl shell <ctname>
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
machinectl reboot <ctname>
```

## License

This work is licensed under [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/), which effectively puts it in the public domain.
