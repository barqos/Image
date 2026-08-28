# Barq

Barq is a KDE Plasma desktop image: privacy-respecting, fast, and stable. This repository builds and publishes the container images.

Images are published to [`ghcr.io/barqos`](https://github.com/orgs/barqos/packages).

- `ghcr.io/barqos/barq`
- `ghcr.io/barqos/barq-dx`
- `ghcr.io/barqos/barq-nvidia-open`
- `ghcr.io/barqos/barq-dx-nvidia-open`

[![Stable Images](https://github.com/barqos/Image/actions/workflows/build-image-stable.yml/badge.svg)](https://github.com/barqos/Image/actions/workflows/build-image-stable.yml) [![Latest Images](https://github.com/barqos/Image/actions/workflows/build-image-latest-main.yml/badge.svg)](https://github.com/barqos/Image/actions/workflows/build-image-latest-main.yml)

## Documentation

1. [Issues](https://github.com/barqos/Image/issues)
2. [Contributing Guide](./CONTRIBUTING.md)

### Secure Boot

Secure Boot is supported by default. After the first installation, you will be prompted to enroll the secure boot key in the BIOS.

Enter the password `universalblue` when prompted to enroll the key.

If this step is not completed during the initial setup, you can manually enroll the key by running:

```
ujust enroll-secure-boot-key
```

The public key is in the akmods repository [here](https://github.com/ublue-os/akmods/raw/main/certs/public_key.der).
If you'd like to enroll this key prior to installation or rebase, download the key and run:

```bash
sudo mokutil --timeout -1
sudo mokutil --import public_key.der
```

### Image signing (Cosign)

Published images are signed with Cosign. The public key is [`cosign.pub`](./cosign.pub).

Verify an image:

```bash
cosign verify --key cosign.pub ghcr.io/barqos/barq:stable
```

The private key is stored as the GitHub Actions secret `SIGNING_SECRET`. Do not commit `cosign.key`.
