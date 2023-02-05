Generate the CA and all certificates on a secure machine and then copy only the needed files to the server(s) and clients.
```
docker run --net=none --rm -t -i -v $PWD/roles/openvpn/files/data:/etc/openvpn kylemanna/openvpn ovpn_genconfig -C 'AES-256-CBC' -a 'SHA384' -u udp://VPN.SERVERNAME.COM
docker run --net=none --rm -t -i -v $PWD/roles/openvpn/files/data:/etc/openvpn kylemanna/openvpn ovpn_initpki
```

Generate a client certificate without a passphrase
```
docker run -v $PWD/roles/openvpn/files/data:/etc/openvpn --rm -it kylemanna/openvpn easyrsa build-client-full CLIENTNAME nopass
```

Retrieve the client configuration with embedded certificates
```
docker run -v $PWD/roles/openvpn/files/data:/etc/openvpn --rm kylemanna/openvpn ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn
```
