# Seagate FireCuda Forge — Open Source Software Release

This repository is the **open-source license-compliance distribution** for the
firmware running on the Seagate FireCuda Forge product.

The firmware is built with the [Yocto Project](https://www.yoctoproject.org/)
(`scarthgap` release series). It contains software licensed under the GNU
General Public License (GPL), the GNU Lesser General Public License (LGPL) and
other open-source licenses. In accordance with those licenses, the
corresponding source code of every copyleft component shipped in a released
firmware image is published here.

---

## What this repository contains

For every published firmware release you will find:

| File | Description |
| --- | --- |
| `forge-source-archive-<RELEASE>.tar.zst` | Complete *patched* source code of all open-source components shipped in the image, exactly as built (upstream sources + the patches applied by the build). |
| `SHA256SUM` | SHA-256 checksum of the file above. |

## What this repository does **not** contain

* Seagate proprietary application code, and third-party components distributed
  under closed or proprietary licenses. These are not covered by any copyleft
  obligation and are deliberately excluded from the source archive.
* Signing keys, device certificates, or any other secret material.
* Vendor binary-only firmware blobs.

This repository is a **compliance publication, not a development project**. It
is not a place to report product problems and it does not track the internal
development history.

---

## Extracting the archives

The archives are Zstandard-compressed tarballs. GNU tar 1.31+ handles them
directly:

```sh
sha256sum -c SHA256SUM
tar --zstd -xf forge-source-archive-<RELEASE>.tar.zst
```

If your `tar` has no built-in Zstandard support:

```sh
zstd -d forge-source-archive-<RELEASE>.tar.zst -c | tar -xf -
```

## Layout of the source archive

The source archive is produced by the Yocto `archiver` class in `patched` mode.
After extraction you get:

```
sources/
  <package-architecture>/
    <recipe>-<version>-<revision>/
      <recipe>-<version>-<revision>-patched.tar.gz   # source tree as compiled
      *.bb, *.bbappend, *.inc                        # recipe metadata (when present)
```

Each `*-patched.tar.gz` is the source tree **after** all build-system patches
have been applied — i.e. the exact code that was compiled into the released
image. Upstream provenance (original download URL, upstream version, applied
patches) is recorded in the recipe metadata and in the SBOM.

## Licenses

Each extracted component carries its own license text in its source tree. The
authoritative, per-package license list for a given release is the SBOM.
The main copyleft components include, among others, the Linux kernel, U-Boot,
BusyBox, glibc and systemd.

Trademarks, product names and logos are the property of their respective
owners and are not licensed under the terms of the GPL or any other license
referenced here.

## Support

Issues and pull requests are **not** monitored on this repository. It exists
solely to satisfy open-source license obligations. For product support, please
use the official Seagate support channels.
