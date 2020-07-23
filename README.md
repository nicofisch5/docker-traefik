# Docker traefik

This repository contains a dockerized [traefik](https://traefik.io/)
reverse-proxy, for manage all app on a server for use ports 80 / 443.

This README.md file was completely insprired by one written by Alexandre Haag (a delicious man).

## Requirements

This project uses [docker](https://www.docker.com/what-docker) and
[docker-compose](https://docs.docker.com/compose/overview/) to simplify
dependencies and deployment.

Note: Tested on Ubuntu 20.04

### Tested versions

- [docker](https://docs.docker.com/install) (Tested: v19.03.8)
- [docker-compose](https://docs.docker.com/compose/install) (Tested: v1.25.0)

## Configuration

### Env variables

In order to copy the default environment variables and set your local configuration, copy the .env.example file

```bash
cp .env.example .env
```

Once done, you can edit all the environment variables in the newly generated `.env`.

## Hostname

Make sure to add the hostnames configured in `.env` file to you `/etc/hosts` file:

```bash
127.0.0.1 traefik.devl # check value in .env
```

## Installation

### Traefik

Simply run the docker-compose command below:

```bash
docker-compose up -d
```

Make sure that ports 80 / 443 are free on your local machine!

Then, navigate to https://traefik.devl/ in your favorite browser.

## Configuration Traefik (traefik.toml)

## Active valid ssl certificate on local

### Create manually certificate

First install this tool [mkcert](https://github.com/FiloSottile/mkcert).
And run this command :

```bash
mkcert -install
```

#### Create manually wildcard certificate

Replace `*.traefik.devl` :
```bash
cd certs
mkcert "*.traefik.devl"
cd ..
```

Then copy command behind and replace CERTNAME var with the wildcard domain eq for `*.traefik.devl` => `traefik.devl` :

```bash
cd config

CERTNAME=traefik.devl; echo "
tls:
  certificates:
    - certFile: /etc/traefik/certs/_wildcadrd.${CERTNAME}.pem
      keyFile: /etc/traefik/certs/_wildcard.${CERTNAME}-key.pem
" > "tls-certs-${CERTNAME}.yml"
```

You may need to restart your browser to take the new certificate.
