# uphold/litecoin-core

A Litecoin Core docker image.

[![uphold/litecoin-core][docker-pulls-image]][docker-hub-url] [![uphold/litecoin-core][docker-stars-image]][docker-hub-url] [![uphold/litecoin-core][docker-size-image]][docker-hub-url] [![uphold/litecoin-core][docker-layers-image]][docker-hub-url]

## Supported tags and respective `Dockerfile` links
- `0.14.2`, `0.14`, `latest` ([0.14/Dockerfile](https://github.com/uphold/docker-litecoind/blob/master/0.14/Dockerfile))
- `0.13.2`, `0.13`, `latest` ([0.13/Dockerfile](https://github.com/uphold/docker-litecoind/blob/master/0.13/Dockerfile))
- `0.10.4`, `0.10` ([0.10/Dockerfile](https://github.com/uphold/docker-litecoind/blob/master/0.10/Dockerfile))

## What is Litecoin Core?

Litecoin Core is a program that implements the Litecoin protocol for remote procedure call (RPC) use. Learn more about [Litecoin Core](https://litecoin.info/Litecoin).

## Usage

### How to use this image

This image contains the main binaries from the Litecoin Core project - `litecoind`, `litecoin-cli` and `litecoin-tx`. It behaves like a binary, so you can pass any arguments to the image and they will be forwarded to the `litecoind` binary:

```sh
❯ docker run --rm uphold/litecoin-core \
  -printtoconsole \
  -regtest=1 \
  -rpcallowip=172.17.0.0/16 \
  -rpcpassword=bar \
  -rpcuser=foo
```

By default, `litecoind` will run as user `litecoin` for security reasons and with its default data dir (`~/.litecoin`). If you'd like to customize where `litecoind` stores its data, you must use the `LITECOIN_DATA` environment variable. The directory will be automatically created with the correct permissions for the `litecoin` user and `litecoind` automatically configured to use it.

```sh
❯ docker run -e LITECOIN_DATA=/var/lib/litecoind --rm uphold/litecoin-core \
  -printtoconsole \
  -regtest=1
```

You can also mount a directory in a volume under `/home/litecoin/.litecoin` in case you want to access it on the host:

```sh
❯ docker run -v ${PWD}/data:/home/litecoin/.litecoin --rm uphold/litecoin-core \
  -printtoconsole \
  -regtest=1
```

You can optionally create a service using `docker-compose`:

```yml
litecoin-core:
  image: uphold/litecoin-core
  command:
    -printtoconsole
    -regtest=1
```

## Images
The `uphold/litecoin-core` image comes in multiple flavors:

### `uphold/litecoin-core:latest`
Points to the latest release available of Litecoin Core. Occasionally pre-release versions will be included.

### `uphold/litecoin-core:<version>`
Based on a slim Debian image, targets a specific version branch or release of Litecoin Core.

## Supported Docker versions

This image is officially supported on Docker version 17.09.0-ce, with support for older versions provided on a best-effort basis.

## License

The [uphold/docker-litecoind][docker-hub-url] docker project is under MIT license.

[docker-hub-url]: https://hub.docker.com/r/uphold/litecoin-core
[docker-layers-image]: https://img.shields.io/imagelayers/layers/uphold/litecoin-core/latest.svg?style=flat-square
[docker-pulls-image]: https://img.shields.io/docker/pulls/uphold/litecoin-core.svg?style=flat-square
[docker-size-image]: https://img.shields.io/imagelayers/image-size/uphold/litecoin-core/latest.svg?style=flat-square
[docker-stars-image]: https://img.shields.io/docker/stars/uphold/litecoin-core.svg?style=flat-square
