# WireGuard installer with Full Cone NAT


If you are looking for a common WireGuard install script that supports multi-client connections, i.e. multiple devices connect to the VPN at the same time, please visit [this repository](https://github.com/angristan/wireguard-install/) to continue.

The script **Port Forwards** the local port `1024-65000` to the corresponding ports on the server side.

The script supports both IPv4 and IPv6.

Most part of this script is based on the angristan's [wireguard-install](https://github.com/angristan/wireguard-install/).

## For Advance User

IPtables full cone nat script:

```bash
# PostUp script
# DNAT 1024 to 65000

iptables -t nat -A PREROUTING -i ${SERVER_PUB_NIC} -p udp --dport 1024:65000 -j DNAT --to-destination ${CLIENT_WG_IPV4}:1024-65000
iptables -t nat -A PREROUTING -i ${SERVER_PUB_NIC} -p tcp --dport 1024:65000 -j DNAT --to-destination ${CLIENT_WG_IPV4}:1024-65000
ip6tables -t nat -A PREROUTING -i ${SERVER_PUB_NIC} -p udp --dport 1024:65000 -j DNAT --to-destination [${CLIENT_WG_IPV6}]:1024-65000
ip6tables -t nat -A PREROUTING -i ${SERVER_PUB_NIC} -p tcp --dport 1024:65000 -j DNAT --to-destination [${CLIENT_WG_IPV6}]:1024-65000
``` 
## Requirements

Supported distributions:

- Ubuntu >= 16.04
- Debian/Raspbian 10

## Usage

Download and execute the script. Answer the questions asked by the script and it will take care of the rest. For most VPS providers, you can just enter through all the questions.

```bash
wget https://raw.githubusercontent.com/TalalMash/wg_fullnat_installer/main/wg-fullnat-installer.sh
bash ./wg-fullnat-installer.sh
```

It will install WireGuard (kernel module and tools) on the server, configure it, create a systemd service and a client configuration file.

## Stop / Restart / Uninstall

Run the script again will give you these options!
