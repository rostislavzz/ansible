# Ansible playbooks

## Configure Ansible vault
```
ansible-vault edit vars/prod.vault.yml
```

```
ansible-galaxy install -r requirements.yml
```

## Install Proxmox VE 6 on Debian 10
```
ansible-playbook proxmox-playbook.yml --ask-pass --ask-become-pass -vv
```

## Install Proxmox VE 7 on Debian 11
Install Proxmox VE on Debian 11 Bullseye: https://pve.proxmox.com/wiki/Install_Proxmox_VE_on_Debian_11_Bullseye
```
ansible-playbook proxmox7-playbook.yml --ask-pass --ask-become-pass --ask-vault-pass -vv
```
### iGPU Full Passthrough to VM
https://pve.proxmox.com/wiki/PCI_Passthrough
https://pve.proxmox.com/wiki/PCI(e)_Passthrough
https://3os.org/infrastructure/proxmox/gpu-passthrough/igpu-passthrough-to-vm/

Need to pin kernel to `5.11.22-7-pve`:
https://forum.proxmox.com/threads/pci-passthrough-error-since-kernel-5-13-19-1-upgrade-from-7-0-to-7-1.100961/

```
ansible-playbook proxmox7-gpu-passthrough-playbook.yml -vv
```

## Configure OpenMediaVault 6
```
ansible-playbook openmediavault6-playbook.yml --ask-pass --ask-vault-pass -vv
```

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

Install and upload updated OpenVPN config to remote server.
```
ansible-playbook openvpn-playbook.yml --ask-vault-pass -vv
```

## WireGuard VPN Server
```
ansible-playbook wireguard-playbook.yml --ask-vault-pass -vv
```
