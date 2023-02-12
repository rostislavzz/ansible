# Ansible playbooks

## OpenVPN
Generate the config, CA and all certificates.
```
./bin/openvpn-genconfig -u udp://VPN.SERVERNAME.COM
./bin/openvpn-initpki
```

Generate a client certificate without a passphrase and retrieve configuration with embedded certificates.
```
./bin/openvpn-genclient
```

Install and upload updated OpenVNP config to remote server.
```
ansible-playbook openvpn-playbook.yml -vv
```

## WireGuard
```
ansible-playbook wireguard-playbook.yml --ask-vault-pass -vv
```
