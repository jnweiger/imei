<div align=center>

# IMEI - ImageMagick Easy Install
#### Automated ImageMagick compilation from sources for Debian/Ubuntu including advanced delegate support.

[![Build](https://img.shields.io/github/actions/workflow/status/SoftCreatR/imei/.github/workflows/main.yml?branch=main&style=flat-square)](https://github.com/SoftCreatR/imei/actions/workflows/main.yml)

[![Commits](https://img.shields.io/github/last-commit/SoftCreatR/imei?style=flat-square)](https://github.com/SoftCreatR/imei/commits/main) [![GitHub release](https://img.shields.io/github/release/SoftCreatR/imei?style=flat-square)](https://github.com/SoftCreatR/imei/releases) [![GitHub license](https://img.shields.io/github/license/SoftCreatR/imei?style=flat-square&color=lightgray)](LICENSE.md) [![Plant Tree](https://img.shields.io/badge/dynamic/json?color=brightgreen&label=Plant%20Tree&query=%24.total&url=https%3A%2F%2Fpublic.offset.earth%2Fusers%2Fsoftcreatr%2Ftrees&style=flat-square)](https://ecologi.com/softcreatr?r=61212ab3fc69b8eb8a2014f4)  [![Installs](https://img.shields.io/badge/dynamic/json?style=flat-square&color=blue&label=installs&query=value&url=https://dist.1-2.dev/imei.php?cnt)](https://github.com/SoftCreatR/imei#one-step-automated-install) [![GitHub file size in bytes](https://img.shields.io/github/size/SoftCreatR/imei/imei.sh?style=flat-square)](https://github.com/SoftCreatR/imei/blob/main/imei.sh)

[![Codacy grade](https://img.shields.io/codacy/grade/db0b2b5f22454f4280e4623de9f7075f?style=flat-square&label=codacy%20grade)](https://app.codacy.com/gh/SoftCreatR/imei/dashboard) [![CodeFactor Grade](https://img.shields.io/codefactor/grade/github/SoftCreatR/imei?style=flat-square&label=codefactor%20rating)](https://www.codefactor.io/repository/github/softcreatr/imei)

</div>

---

<div align="center">

<a href="#features"> Features<a> •
<a href="#compatibility"> Compatibility</a> •
<a href="#usage"> Usage</a> •
<a href="#contributing"> Contributing</a> •
<a href="#license"> License</a>

![Screenshot](screenshot.png)

</div>

---

## Features

* Compiles the latest ImageMagick release
* Installs ImageMagick or updates ImageMagick package previously installed (via IMEI)
* Additional HEIF/HEIC/HEIX support
* Additional AVIF support
* Additional JPEG XL support

---

## Compatibility

The compatibility of every IMEI build is automatically tested using GitHub Actions against the latest Ubuntu LTS version. However, manual testing is conducted to ensure compatibility with other operating systems, such as Debian 10 or Ubuntu 21.04.

### Operating System

#### Recommended

* Ubuntu 22.04 (__Jammy__ Jellyfish)
* Debian 11 (__Bullseye__)

#### Also compatible

* Ubuntu 23.04 (__Lunar__ Lobster)
* Ubuntu 22.10 (__Kinetic__ Kudu)
* Ubuntu 21.10 (__Impish__ Indri)
* Ubuntu 21.04 (__Hirsute__ Hippo)
* Ubuntu 20.10 (__Groovy__ Gorilla)
* Ubuntu 20.04 (__Focal__ Fossa)
* Ubuntu 19.10 (__Eoan__ Ermine)
* Ubuntu 19.04 (__Disco__ Dingo)
* Ubuntu 18.10 (__Cosmic__ Cuttlefish)
* Ubuntu 18.04 (__Bionic__ Beaver)
* Ubuntu 17.10 (__Artful__ Aardvark)
* Ubuntu 17.04 (__Zesty__ Zapus)
* Ubuntu 16.10 (__Yakkety__ Yak)
* Ubuntu 16.04 (__Xenial__ Xerus)
* Debian 12 (__Bookworm__)
* Debian 10 (__Buster__)
* Debian 9 (__Stretch__)

#### Known issues

- To compile JPEG XL, CMake 3.10 or a newer version is required. On older systems like Debian 9, the version provided by maintainers is not adequate. In such cases, the compilation of JPEG XL will be skipped.
- For libaom, a minimum CMake version of 3.6 is necessary. On older systems, the version provided by maintainers might not be sufficient. In these instances, the compilation of libaom will be skipped. Consequently, libheif will also be skipped since it depends on libaom.
- When using GitHub actions for building, `heic` is not reported as a built-in delegate. Although it was reported in the past, it suddenly stopped. Therefore, it is advisable to avoid using it as an assertion for tests.

---

## Usage

### One-Step Automated Install

```bash
t=$(mktemp) && \
wget 'https://dist.1-2.dev/imei.sh' -qO "$t" && \
bash "$t" && \
rm "$t"
```

### Alternative Install Method

```bash
git clone https://github.com/SoftCreatR/imei && \
cd imei && \
chmod +x imei.sh && \
./imei.sh
```

### Verify installer integrity

Though the installer performs a self check upon startup, you can also perform it manually.
To do so, `openssl` is required:

```bash
wget https://dist.1-2.dev/imei.sh && \                                  # Download IMEI
wget https://dist.1-2.dev/imei.sh.sig && \                              # Download signature file
wget https://dist.1-2.dev/imei.sh.pem && \                              # Download public key
openssl dgst -sha512 -verify imei.sh.pem -signature imei.sh.sig imei.sh # Verify
```

### Alternative integrity check

```bash
git clone https://github.com/SoftCreatR/imei && \
cd imei && \
openssl dgst -sha512 -verify imei.sh.pem -signature imei.sh.sig imei.sh
```

#### Options available

Currently available build options are

* `--skip-dependencies` / `--skip-deps` : Skip installation of dependencies
* `--imagemagick-version` / `--im-version` : Build the given ImageMagick version (e.g. `7.0.10-28`)
* `--force-imagemagick` / `--force-im` : Force building of ImageMagick only, even if it's are already installed in a newer or the latest version
* `--imagemagick-quantum-depth` / `--im-q` : ImageMagick Quantum Depth (8, 16 or 32)
* `--imagemagick-opencl` / `--im-ocl` : Install ImageMagick with OpenCL support
* `--aom-version` : Build the given aom version (e.g. `2.0.0`)
* `--skip-aom` : Skip building aom
* `--libheif-version` / `--heif-version` : Build the given libheif version (e.g. `1.8.0`)
* `--skip-libheif` / `--skip-heif` : Skip building libheif
* `--jpeg-xl-version` / `--jxl-version` : Build the given JPEG XL version (e.g. `0.3.3`)
* `--skip-jpeg-xl` / `--skip-jxl` : Skip building JPEG XL
* `--log-file` : Log everything to the file provided
* `--work-dir` : Download, extract & build within the directory provided
* `--build-dir` : Build target directory for ImageMagick
* `--config-dir` : Config target directory for ImageMagick
* `--force` : Force building of components, even if they are already installed in a newer or the latest version

Additional options / switches:

* `--no-sig-verify` / `--dev` : Disable signature verification on startup
* `--use-checkinstall` / `--checkinstall` : Use `checkinstall` instead of `make`
* `--no-backports` : Disable temporary installation of OS backports (they may be used anyways, depending on your server configuration)

**Default options** :

<!-- versions start -->
* ImageMagick version: `7.1.1-15 (Q16)`
* libaom version: `3.6.1`
* libheif version: `1.16.2`
* libjxl version: `0.8.2`<!-- versions end -->
* Log File: `/var/log/imei.log`
* Work Dir: `/usr/local/src/imei`
* Build Dir: `/usr/local`
* Config Dir: `/usr/local/etc`

### checkinstall vs. make

IMEI offers support for both `checkinstall` and `make` methods. While `checkinstall` enables the creation of packages that can be uninstalled at a later time, such as `apt remove imei-imagemagick`, the use of `make` does not provide the same convenience, making it potentially more difficult to remove all components installed by IMEI. However, it's important to note that `checkinstall` may not always be available and may have certain bugs that could lead to an incomplete installation of IMEI packages.

By default, IMEI utilizes the `make` method, but you have the option to use `checkinstall` by specifying it in the additional options or switches (refer to "Additional options / switches" for more details).

### OpenCL support

IMEI provides the option to install ImageMagick with OpenCL support. However, it is important to consider that according to the information provided [here](https://github.com/SoftCreatR/imei/issues/69#issuecomment-1563379174), ImageMagick's performance is significantly lower when utilizing OpenCL compared to OpenMP.

When you choose to install ImageMagick with OpenCL support using IMEI, please be aware that IMEI only compiles ImageMagick with OpenCL capabilities. It does not handle the installation of necessary drivers or any other specific requirements to enable general OpenCL support on your system.

---

## Contributing

If you have any ideas, just open an issue and describe what you would like to add/change in IMEI.

If you'd like to contribute, please fork the repository and make changes as you'd like. Pull requests are warmly welcome.

## License 🌳

[ISC](LICENSE.md) © [1-2.dev](https://1-2.dev)

This package is Treeware. If you use it in production, then we ask that you [**buy the world a tree**](https://ecologi.com/softcreatr?r=61212ab3fc69b8eb8a2014f4) to thank us for our work. By contributing to the ecologi project, you’ll be creating employment for local families and restoring wildlife habitats.
