# Ansible playbooks

## Configure Ansible vault

```
ansible-vault edit vars/prod.vault.yml
```

```
ansible-galaxy install -r requirements.yml
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
https://gist.github.com/scyto/e4e3de35ee23fdb4ae5d5a3b85c16ed3

Need to pin kernel to `5.11.22-7-pve`:  
https://forum.proxmox.com/threads/pci-passthrough-error-since-kernel-5-13-19-1-upgrade-from-7-0-to-7-1.100961/

```
ansible-playbook proxmox7-gpu-passthrough-playbook.yml -vv
```

## LXC

Create containers:

```
ansible-playbook proxmox7-lxc-playbook.yml --ask-vault-pass -vv
```

### Plex

```
ansible-playbook lxc-docker-plex-playbook.yml -vv
```

Check Intel GPU usage with `intel-gpu-tools` package and `intel_gpu_top` command.

### Photoprism

```
ansible-playbook lxc-docker-photoprism-playbook.yml --ask-vault-pass -vv
```

### Immich
```
docker compose run --rm ansible ansible-galaxy install -r requirements.yml && ansible-playbook lxc-docker-immich-playbook.yml --ask-vault-pass -vv
```

## Configure OpenMediaVault 6

For first run, to copy ssh-key:

```
ansible-playbook omv6-playbook.yml --ask-pass -vv
```

When ssh-key already on host:

```
ansible-playbook omv6-playbook.yml --ask-vault-pass -vv
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

## Xray VPN Server

For first run, to copy ssh-key:

```
ansible-playbook xray-playbook.yml --ask-pass --ask-vault-pass -vv
```

When ssh-key already on host:

```
ansible-playbook xray-playbook.yml --ask-vault-pass -vv
```

## ASUS RT-N66U

Base on https://github.com/msielicki/ansible-role-asus-merlin/tree/master

```
ansible-playbook asus-rt-n66u.yml --ask-pass -vv
```
