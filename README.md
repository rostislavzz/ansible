# Ansible playbooks

## OpenVPN
Generate the CA and all certificates.
```
./openvpn-genconfig -u udp://VPN.SERVERNAME.COM
./openvpn-initpki
```

Generate a client certificate without a passphrase and retrieve configuration with embedded certificates.
```
./openvpn-genclient
```

Install and upload updated OpenVNP config to remote server.
```
ansible-playbook openvpn-playbook.yml -vv
```
