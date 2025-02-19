# OpenVPN and Deluge with WebUI

![Build/Push (master)](https://github.com/ebrianne/docker-deluge-openvpn/workflows/Build/Push%20(master)/badge.svg?branch=master)
[![Docker Pulls](https://img.shields.io/docker/pulls/ebrianne/docker-deluge-openvpn.svg)](https://hub.docker.com/r/ebrianne/docker-deluge-openvpn/)

## Acknowledgments

This project is based heavily on the fork of [docker-transmission-openvpn](https://github.com/haugene/docker-transmission-openvpn). 

## Quick Start

This container contains OpenVPN and Deluge with a configuration
where Deluge is running only when OpenVPN has an active tunnel.
It bundles configuration files for many popular VPN providers to make the setup easier.

```
$ docker run --cap-add=NET_ADMIN -d \
              -v /your/storage/path/:/data \
              -e OPENVPN_PROVIDER=PIA \
              -e OPENVPN_CONFIG=France \
              -e OPENVPN_USERNAME=user \
              -e OPENVPN_PASSWORD=pass \
              -e LOCAL_NETWORK=192.168.0.0/16 \
              --log-driver json-file \
              --log-opt max-size=10m \
              -p 8112:8112 \
              ebrianne/docker-deluge-openvpn
```

## Docker Compose
```
version: '3.2'
services:
    deluge-openvpn:
        volumes:
            - '/your/storage/path/:/data'
        environment:
            - OPENVPN_PROVIDER=PIA
            - OPENVPN_CONFIG=France
            - OPENVPN_USERNAME=user
            - OPENVPN_PASSWORD=pass
            - LOCAL_NETWORK=192.168.0.0/16
        cap_add:
            - NET_ADMIN
        sysctls:
            - net.ipv6.conf.all.disable_ipv6=0
        logging:
            driver: json-file
            options:
                max-size: 10m
        ports:
            - '8112:8112'
        image: ebrianne/docker-deluge-openvpn
```

## Documentation
The full documentation is available at https://haugene.github.io/docker-transmission-openvpn/.

## Environment variables

| Variable           | Value         |
| -------------------|:-------------:|
| OPENVPN_USERNAME   | **None**      |
| OPENVPN_PASSWORD   | **None**      |
| OPENVPN_PROVIDER   | **None**      |
| CREATE_TUN_DEVICE  | true          |
| ENABLE_UFW         | false         |
| UFW_EXTRA_PORTS    | **None**      |
| UFW_ALLOW_GW_NET   | false         |
| PUID               | **None**      |
| PGID               | **None**      |
| DROP_DEFAULT_ROUTE | **None**      |
| HEALTH_CHECK_HOST  | google.com    |
| LANG               | en_US.UTF-8   |
| LANGUAGE           | en_US.UTF-8   |
| TERM               | xterm         |
| LOCAL_NETWORK      | **None**      |
