# FreeRadius Docker Container

[![Docker Build Status](https://img.shields.io/docker/cloud/build/wellsgz/docker-freeradius.svg)](https://hub.docker.com/r/wellsgz/docker-freeradius/) [![Docker Pulls](https://img.shields.io/docker/pulls/wellsgz/docker-freeradius.svg)](https://hub.docker.com/r/goofball222/freeradius/) [![Docker Stars](https://img.shields.io/docker/stars/goofball222/freeradius.svg)](https://hub.docker.com/r/wellsgz/docker-freeradius/) [![MB Layers](https://images.microbadger.com/badges/image/goofball222/freeradius.svg)](https://microbadger.com/images/wellsgz/docker-freeradius) [![MB Commit](https://images.microbadger.com/badges/commit/wellsgz/docker-freeradius.svg)](https://microbadger.com/images/wellsgz/docker-freeradius) [![MB License](https://images.microbadger.com/badges/license/wellsgz/docker-freeradius.svg)](https://microbadger.com/images/wellsgz/docker-freeradius)

## Docker tags:
| Tag | freeradius Version | Description | Release Date |
| --- | :---: | --- | :---: |
| [latest](https://github.com/wellsgz/freeradius/blob/master/stable/Dockerfile) | 3.0.19 | Latest stable release | 2019-06-28 |


---

## Description

FreeRadius container built on Alpine Linux.

See: [https://wiki.freeradius.org/guide/Basic-configuration-HOWTO](https://wiki.freeradius.org/guide/Basic-configuration-HOWTO) and the rest of the FreeRadius Wiki for setup help.

---

## Usage

This container exposes the following two ports:
* `1812/udp` freeradius authorization service port
* `1813/udp` freeradius accounting service port

---

**Basic docker-compose.yml to launch a FreeRadius instance and make it accessible*

```bash

version: '3'

services:
  freeradius:
    image: wellsgz/docker-freeradius
    container_name: freeradius
    network_mode: bridge
    restart: unless-stopped
    ports:
      - 1812:1812/udp
      - 1813:1813/udp
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /home/wells/data/freeradius/clients.conf:/etc/raddb/clients.conf
      - /home/wells/data/freeradius/radiusd.conf:/etc/raddb/radiusd.conf
      - /home/wells/data/freeradius/authorize:/etc/raddb/mods-config/files/authorize
      - /home/wells/data/freeradius/sites-enabled:/etc/raddb/sites-enabled
      - /home/wells/data/freeradius/certs:/etc/raddb/certs
    environment:
      - TZ=Asia/Hong_Kong

```

---


**Environment variables:**

| Variable | Default | Description |
| :--- | :---: | --- |
| `DEBUG` | ***false*** | Set to *true* for extra entrypoint script verbosity for debugging |
| `PGID` | ***999*** | Specifies the GID for the container internal radius group (used for file ownership) |
| `PUID` | ***999*** | Specifies the UID for the container internal radius user (used for process and file ownership) |
| `RADIUSD_OPTS` | ***unset*** |  Any additional custom run options for the container radiusd process |

[//]: # (Licensed under the Apache 2.0 license)
[//]: # (Revised from https://github.com/goofball222/freeradius)
