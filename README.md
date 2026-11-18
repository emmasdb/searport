[![Automatic version updates](https://github.com/zopencommunity/searport/actions/workflows/bump.yml/badge.svg)](https://github.com/ZOSOpenTools/searport/actions/workflows/bump.yml)

# sear

SEAR (Security API for RACF) - A unified and standardized interface to RACF callable services.

# Installation and Usage

Use the zopen package manager ([QuickStart Guide](https://zopen.community/#/Guides/QuickStart)) to install:
```bash
zopen install sear
```

# Building from Source

1. Clone the repository:
```bash
git clone https://github.com/zopencommunity/searport.git
cd searport
```
2. Build using zopen:
```bash
zopen build -vv
```

See the [zopen porting guide](https://zopen.community/#/Guides/Porting) for more details.

## Python Wheels

GitHub pull-request validation builds and tests the `pysear` wheel on the
zopen Jenkins runner. It does not publish to the wheel index. Local builds
and Jenkins release builds still select the native `sear` package by default.

To reproduce the wheel build from a separate checkout on z/OS Unix with
zopen and Python 3.13 available, run:

```sh
SEAR_BUILD_PYTHON=1 zopen build -vv
```

The build stages wheels under `install/dist/`. A separate checkout keeps the
Python and native builds from sharing patched source and build state.

# Documentation


# Troubleshooting

# Contributing
Contributions are welcome! Please follow the [zopen contribution guidelines](https://github.com/zopencommunity/meta/blob/main/CONTRIBUTING.md).
