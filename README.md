# IglooVPN Infrastructure

This repository is meant to provide local & production infrastructure code and automation code.

So far this is just a demo on local environment with two docker containers :
- one for deploying a local strongswan
- one for a deploy a client that connects to the vpn and ping other clients

## Prerequisites

Any CRI compliant software or Docker ( easier on windows )

## Build

```sh
docker build -t igloovpn/strongswan strongswan
```

## Run

```sh
docker run --rm --cap-add=NET_ADMIN -ti igloovpn/strongswan
```

_Note_: you can exit by hitting Ctrl+C