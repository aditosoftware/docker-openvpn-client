# openvpn-client

## docker-compose

The following docker-compose.yml provides a sample configuration.

The service alpine will use the network-interface from the service openvpn and should now have access to servers behind the vpn.

```
services:
  alpine:
    image: alpine
    network_mode: service:openvpn
  openvpn:
    cap_add:
    - NET_ADMIN
    command: openvpn --config /opt/openvpn/openvpn-config.ovpn
    devices:
    - /dev/net/tun
    image: adito/openvpn-client
    volumes:
    - ./config/openvpn-config.ovpn:/opt/openvpn/openvpn-config.ovpn:ro
version: '3.0'
```
