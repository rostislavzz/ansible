# ansible

## OpenVPN
Generate the CA and all certificates.
```
./openvpn-genconfig -u udp://VPN.SERVERNAME.COM
./openvpn-initpki
```

Generate a client certificate without a passphrase
```
docker run -v $PWD/roles/openvpn/files/data:/etc/openvpn --rm -it kylemanna/openvpn easyrsa build-client-full CLIENTNAME nopass
```

Retrieve the client configuration with embedded certificates
```
docker run -v $PWD/roles/openvpn/files/data:/etc/openvpn --rm kylemanna/openvpn ovpn_getclient CLIENTNAME > $PWD/roles/openvpn/files/clients/CLIENTNAME.ovpn
```

Install and upload updated OpenVNP config to remote server.
```
ansible-playbook openvpn-playbook.yml -vv
```
