# proxmox-backup-client-arm64

[English](./README.md) | Português Brasileiro

Coleção de binários ARM64 do `proxmox-backup-client` para diferentes distros Linux.

Este repo existe porque a portabilidade em Linux pode ser caótica: versões de `glibc`, `openssl` e `libfuse` podem quebrar um binário entre distros. Também é difícil achar binário pronto do backup client para ARM64. Eu precisei disso para fazer backup de arquivos de um Unifi UNAS Pro para meu PBS e tive que compilar manualmente para Debian 11 ARM64.

Aqui você encontra variantes précompiladas por distro, com dependências de runtime bem claras.

## Vejá tambem as builds do client em Go (ARM64 neste repo)

Este repo também inclui builds ARM64 do projeto `proxmoxbackupclient_go`.
Vá para [Cliente Go (builds ARM64 neste repo)](#cliente-go-builds-arm64-neste-repo).

Ou baixe diretamente:

- [directorybackup](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmoxbackupclient_go/directorybackup)
- [machinebackup](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmoxbackupclient_go/machinebackup)
- [nbd](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmoxbackupclient_go/nbd)

## Distros Disponíveis

- Debian 11: [proxmox-backup-client_arm64-debian11](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmox-backup-client_arm64-debian11)
- Debian 12: [proxmox-backup-client_arm64-debian12](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmox-backup-client_arm64-debian12)
- Debian 13: [proxmox-backup-client_arm64-debian13](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmox-backup-client_arm64-debian13)
- Ubuntu 20.04: [proxmox-backup-client_arm64-ubuntu20](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmox-backup-client_arm64-ubuntu20)
- Ubuntu 22.04: [proxmox-backup-client_arm64-ubuntu22](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmox-backup-client_arm64-ubuntu22)
- Ubuntu 24.04: [proxmox-backup-client_arm64-ubuntu24](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmox-backup-client_arm64-ubuntu24)

## Instalação Rápida por Distro

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

## Qual Binário Usar

- Debian 11: use `...-debian11`
- Debian 12: use `...-debian12`
- Debian 13: use `...-debian13`
- Ubuntu 20.04: use `...-ubuntu20`
- Ubuntu 22.04: use `...-ubuntu22`
- Ubuntu 24.04: use `...-ubuntu24`

Se estiver numa distro mais nova, começe testando `debian13` ou `ubuntu24` e rode:

```bash
ldd ./proxmox-backup-client_arm64-<variante>
```

## Troubleshooting

### `error while loading shared libraries`

Rode `ldd` no binário e instale as libs que faltarem.

```bash
ldd ./proxmox-backup-client_arm64-<variante>
```

### `GLIBC_x.y not found`

Seu sistema de destino é mais antigo que o sistema onde o binário foi compilado.
Use um binário de distro mais antiga (por exemplo `debian11`).

### `libfuse3.so.3/4 not found`

Instale o pacote de runtime correto:

- Debian 11/12 e Ubuntu 20/22/24: `libfuse3-3`
- Debian 13: `libfuse3-4`

## Por que não um binário estático único para todas as distros?

Basicamente, inferno de portabilidade nativa.

O `proxmox-backup-client` depende de bibliotecas de sistema (`fuse`, `systemd`, `openssl`, comportamento de ABI do `glibc`).
Um build estático realmente universal não é confiável aqui sem patch pesado e trade-offs.

## Cliente Go (builds ARM64 neste repo)

Projeto de referência:

- [tizbac/proxmoxbackupclient_go](https://github.com/tizbac/proxmoxbackupclient_go)

Arquivos compilados:

- [/proxmoxbackupclient_go/](./proxmoxbackupclient_go/)


Contexto importante: o upstream não fornece binários ARM64 prontos para Linux.
Por isso, este repo também inclui binários ARM64 do cliente Go compilados manualmente.

No caso do cliente Go, ele é dividido em múltiplos executáveis (modelo toolbox), sendo eles:

- [`directorybackup`](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmoxbackupclient_go/directorybackup) para backup de diretório/stream
- [`machinebackup`](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmoxbackupclient_go/machinebackup) para backup full-machine em modo live
- [`nbd`](https://github.com/junglivre/proxmox-backup-client-arm64/raw/master/proxmoxbackupclient_go/nbd) para fluxos de restore/mount via NBD

Na prática: distribuição cross-platform mais simples, mas com ferramentas separadas dependendo do tipo de operação.

## Créditos

- [Proxmox Backup Server](https://git.proxmox.com/?p=proxmox-backup.git)
- [tizbac/proxmoxbackupclient_go](https://github.com/tizbac/proxmoxbackupclient_go)
- Comunidade que testa compatibilidade ARM64 em várias distros

