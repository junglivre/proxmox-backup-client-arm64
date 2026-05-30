# proxmox-backup-client-arm64

English | [Português Brasileiro](./README.pt-BR.md)

Little collection of `proxmox-backup-client` ARM64 binaries for different Linux distros.

This repo exists because Linux portability is messy af: `glibc`, `openssl`, and `libfuse` versions can break a binary between distros, and because it's quite hard to find the single binary of the backup client for arm64. I myself needed it while trying to backup files from a Unifi UNAS Pro to my PBS, so I had to compile this bad boy for Debian 11 arm64.

And you shall also get prebuilt variants per distro, with clear runtime deps. I chose the most popular ones that came to mind while thinking what distro most embedded systems/solutions use.

## Also check out the Go client builds (ARM64 in this repo)

This repo also includes ARM64 builds based on `proxmoxbackupclient_go`.
Jump to [Go Client (ARM64 builds in this repo)](#go-client-arm64-builds-in-this-repo).

## Available Distros

- Debian 11: [proxmox-backup-client_arm64-debian11](./proxmox-backup-client_arm64-debian11)
- Debian 12: [proxmox-backup-client_arm64-debian12](./proxmox-backup-client_arm64-debian12)
- Debian 13: [proxmox-backup-client_arm64-debian13](./proxmox-backup-client_arm64-debian13)
- Ubuntu 20.04: [proxmox-backup-client_arm64-ubuntu20](./proxmox-backup-client_arm64-ubuntu20)
- Ubuntu 22.04: [proxmox-backup-client_arm64-ubuntu22](./proxmox-backup-client_arm64-ubuntu22)
- Ubuntu 24.04: [proxmox-backup-client_arm64-ubuntu24](./proxmox-backup-client_arm64-ubuntu24)

## Quick Install by Distro

### Debian 11

```bash
apt update
apt install -y libfuse3-3 libsystemd0 libacl1 libuuid1 libssl1.1 zlib1g liblzma5 libzstd1 liblz4-1 libcap2 libgcrypt20 libgpg-error0
chmod +x ./proxmox-backup-client_arm64-debian11
./proxmox-backup-client_arm64-debian11 version
```

### Debian 12

```bash
apt update
apt install -y libfuse3-3 libsystemd0 libacl1 libuuid1 libssl3 zlib1g liblzma5 libzstd1 liblz4-1 libcap2 libgcrypt20 libgpg-error0
chmod +x ./proxmox-backup-client_arm64-debian12
./proxmox-backup-client_arm64-debian12 version
```

### Debian 13

```bash
apt update
apt install -y libfuse3-4 libsystemd0 libacl1 libuuid1 libssl3 zlib1g liblzma5 libzstd1 liblz4-1 libcap2 libgcrypt20 libgpg-error0
chmod +x ./proxmox-backup-client_arm64-debian13
./proxmox-backup-client_arm64-debian13 version
```

### Ubuntu 20.04

```bash
apt update
apt install -y libfuse3-3 libsystemd0 libacl1 libuuid1 libssl1.1 zlib1g liblzma5 libzstd1 liblz4-1 libcap2 libgcrypt20 libgpg-error0
chmod +x ./proxmox-backup-client_arm64-ubuntu20
./proxmox-backup-client_arm64-ubuntu20 version
```

### Ubuntu 22.04

```bash
apt update
apt install -y libfuse3-3 libsystemd0 libacl1 libuuid1 libssl3 zlib1g liblzma5 libzstd1 liblz4-1 libcap2 libgcrypt20 libgpg-error0
chmod +x ./proxmox-backup-client_arm64-ubuntu22
./proxmox-backup-client_arm64-ubuntu22 version
```

### Ubuntu 24.04

```bash
apt update
apt install -y libfuse3-3 libsystemd0 libacl1 libuuid1 libssl3 zlib1g liblzma5 libzstd1 liblz4-1 libcap2 libgcrypt20 libgpg-error0
chmod +x ./proxmox-backup-client_arm64-ubuntu24
./proxmox-backup-client_arm64-ubuntu24 version
```

## Choose the Right Binary

- Debian 11: use `...-debian11`
- Debian 12: use `...-debian12`
- Debian 13: use `...-debian13`
- Ubuntu 20.04: use `...-ubuntu20`
- Ubuntu 22.04: use `...-ubuntu22`
- Ubuntu 24.04: use `...-ubuntu24`

If you use a newer distro, start with `debian13` or `ubuntu24` and run:

```bash
ldd ./proxmox-backup-client_arm64-<variant>
```

## Troubleshooting

### `error while loading shared libraries`

Run `ldd` on the binary and install missing libs.

```bash
ldd ./proxmox-backup-client_arm64-debian13
```

### `GLIBC_x.y not found`

Your target system is older than the build target.
Use a binary built for an older distro (for example `debian11` on old hosts).

### `libfuse3.so.3/4 not found`

Install the matching runtime package:

- Debian 11/12 and Ubuntu 20/22/24: `libfuse3-3`
- Debian 13: `libfuse3-4`

## Why not one static binary for all distros?

Basically, native portability hell.

`proxmox-backup-client` depends on system-level libs (`fuse`, `systemd`, `openssl`, `glibc` ABI behavior).
A fully static, universal Linux build is not reliable here without heavy patching and trade-offs.

## Go Client (ARM64 builds in this repo)

Reference upstream project:

- [tizbac/proxmoxbackupclient_go](https://github.com/tizbac/proxmoxbackupclient_go)

Important context: upstream does not provide ready-to-use ARM64 binaries for Linux.  
Because of that, this repo also includes manually compiled ARM64 Go client binaries.

The Go client side is split into multiple executables (toolbox style), such as:

- `directorybackup` for directory/stream backup flows
- `machinebackup` for full-machine live backup workflows
- `nbd` for restore/mount-related NBD workflows

So the practical model is: easier cross-platform distribution, but separated tools depending on the workflow.


## Credits

- [Proxmox Backup Server](https://git.proxmox.com/?p=proxmox-backup.git)
- [tizbac/proxmoxbackupclient_go](https://github.com/tizbac/proxmoxbackupclient_go)
- Community users testing ARM64 distro compatibility

