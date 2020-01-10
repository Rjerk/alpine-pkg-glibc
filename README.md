# alpine-pkg-glibc (2.30-r0 arm64)

[![CircleCI](https://circleci.com/gh/sgerrand/alpine-pkg-glibc/tree/master.svg?style=svg)](https://circleci.com/gh/sgerrand/alpine-pkg-glibc/tree/master) ![x86_64](https://img.shields.io/badge/x86__64-supported-brightgreen.svg)

This is the [GNU C Library](https://gnu.org/software/libc/) as a Alpine Linux package to run binaries linked against `glibc`. This package utilizes a custom built glibc binary based on the vanilla glibc source. Built binary artifacts come from https://github.com/sgerrand/docker-glibc-builder.

## Usage

Requirements: [Creating an Alpine package](https://wiki.alpinelinux.org/wiki/Creating_an_Alpine_package)

Then you can build apk:

```
# abuild checksum

# abuild -r

# ls ~/packages/
APKINDEX.tar.gz         glibc-bin-2.30-r0.apk   glibc-i18n-2.30-r0.apk
glibc-2.30-r0.apk       glibc-dev-2.30-r0.apk
```

## Releases

See the [releases page](https://github.com/Rjerk/alpine-pkg-glibc/releases) for the latest download links. If you are using tools like `localedef` you will need the `glibc-bin` and `glibc-i18n` packages in addition to the `glibc` package.

## Installing

The current installation method for these packages is to pull them in using `wget` or `curl` and install the local file with `apk`:

    apk --no-cache add ca-certificates wget
    wget -q -O /etc/apk/keys/rjerk.rsa.pub https://raw.githubusercontent.com/Rjerk/alpine-pkg-glibc/2.30-r0-aarch64/rjerk.rsa.pub
    wget https://github.com/Rjerk/alpine-pkg-glibc/releases/download/2.30-r0-arm64/glibc-2.30-r0.apk
    apk add glibc-2.30-r0.apk

## Locales

You will need to generate your locale if you would like to use a specific one for your glibc application. You can do this by installing the `glibc-i18n` package and generating a locale using the `localedef` binary. An example for en_US.UTF-8 would be:

    apk add glibc-bin-2.30-r0.apk glibc-i18n-2.30-r0.apk
    /usr/glibc-compat/bin/localedef -i en_US -f UTF-8 en_US.UTF-8
