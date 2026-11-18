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

See the [zopen porting guide](https://zopen.community/Guides/Porting) for more details.

## Building the Python Bindings

On z/OS Unix, source your zopen configuration and make IBM Open Enterprise
SDK for Python 3.13 and the IBM Open XL C/C++ compiler available. From the
port checkout, run:

```sh
SEAR_BUILD_PYTHON=1 zopen build -vv
```

This builds the `pysear` distribution separately from the native `sear`
package. Zopen checks that the installed wheel can load `sear._C` without
issuing RACF requests and stages the wheel under `install/dist/`. Set
`ZOPEN_PYTHON_VERSIONS` to select other installed interpreters, for example
`ZOPEN_PYTHON_VERSIONS='3.13 3.14'`. Build in a separate checkout when
switching between native and Python builds, since zopen reuses the patched
upstream source tree and build state.

See the [zopen Python porting guide](https://zopen.community/Guides/PythonPorting).

### Validating the Python Port

Before proposing a separate port, check the [package request board](https://zopen.community/PackageRequests),
[Python candidate status](https://zopen.community/Guides/PythonCandidates),
and the [zopen wheel index](https://repo.zopen.community/pypi/wheels/simple/)
for `pysear`. Then try the normal install path on z/OS Unix in a fresh
environment:

```sh
export PIP_EXTRA_INDEX_URL=https://repo.zopen.community/pypi/wheels/simple/
export PIP_CONSTRAINT=https://repo.zopen.community/pulp/content/constraints/zopen-constraints.txt
verify_dir=$(mktemp -d) && python3.13 -m venv --system-site-packages "$verify_dir" &&
	. "$verify_dir/bin/activate" && python -m pip install pysear &&
	python -I -c 'import sear._C; from sear import sear'
```

The import checks that the native extension loads. Also run a read-only SEAR
operation against a known test profile on an authorized z/OS system. The build
smoke test does not run the RACF integration suite. Record the resolved package
version, interpreter version, and results. If the normal install meets the
need, record that outcome instead of requesting a separate port.

If the normal install fails, validate the wheel built by this recipe in another
fresh environment using the interpreter it was built for. Repeat the import
and read-only checks. `pysear` is the [PyPI distribution](https://pypi.org/project/pysear/);
`sear` is the import name. The [upstream source](https://github.com/Mainframe-Renewal-Project/sear)
is Apache-2.0 licensed and uses setuptools to build a native extension with
IBM Open XL C/C++, the z/OS assembler, OpenSSL, and ZOSLIB. The port patch
uses the zopen dependency paths and lets setuptools tag the wheel as native.

Use the [Python contribution guide](https://zopen.community/Guides/PythonContributing)
to submit the z/OS build and test evidence before enabling wheel publication.

# Documentation


# Troubleshooting

# Contributing
Contributions are welcome! Please follow the [zopen contribution guidelines](https://github.com/zopencommunity/meta/blob/main/CONTRIBUTING.md).
