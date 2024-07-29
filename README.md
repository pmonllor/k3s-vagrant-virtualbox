# k3s-vagrant-virtualbox
The purpose of this repo is to provide a simple way to launch a multi-node Kubernetes cluster for local development, both in Windows with WSL2 & natively on Linux

# Index
- [k3s-vagrant-virtualbox](#k3s-vagrant-virtualbox)
- [Index](#index)
- [Infrastructure configuration](#infrastructure-configuration)
- [Windows considerations](#windows-considerations)
- [Launch](#launch)
  - [Windows](#windows)
  - [Linux](#linux)
- [Kubeconfig](#kubeconfig)
- [Tech stack](#tech-stack)

# Infrastructure configuration
- Clone this repo

- Edit ```vars/infra.yml``` as prefered

```bash
---
# VMs hostnames (FQDN) - Example: pier.terrapin.ch
master_server: master.juna
worker_node_1: worker1.juna
worker_node_2: worker2.juna

# IP addreses
master_server_ip: "10.0.1.10"
worker_node_1_ip: "10.0.1.20"
worker_node_2_ip: "10.0.1.30"

# Disk sizes
master_server_disk: "100GB"
worker_node_1_disk: "80GB"
worker_node_2_disk: "80GB"

# Hardware - RAM specified in MB
master_server_cpus: "4"
master_server_ram: 8192

worker_nodes_cpus: "2"
worker_nodes_ram: 4096

# OS - Ubuntu 24.04
vagrant_box: "bento/ubuntu-24.04"

# VirtualBox for Ubuntu 22.04 - https://www.virtualbox.org/wiki/Linux_Downloads
# Will be installed on the host that launches the playbooks (localhost by default)
vbox_ubuntu: "https://download.virtualbox.org/virtualbox/7.0.20/virtualbox-7.0_7.0.20-163906~Ubuntu~noble_amd64.deb"
```

# Windows considerations

- Install on your windows machine: [Vagrant](https://developer.hashicorp.com/vagrant/downloads), [VirtualBox](https://www.virtualbox.org/wiki/Downloads) & [WSL2](https://docs.microsoft.com/en-us/windows/wsl/install)
- Create Ubuntu distribution: `wsl --install -d ubuntu`
- Convert distribution to use WSL2: `wsl --set-version ubuntu 2`
- Enter the machine `wsl -d Ubuntu`
- Install Ansible `python3 -m pip install ansible`

# Launch

## Windows
**Inside WSL**
```bash
ansible-playbook deploy_infra_windows.yml
```
**Outside WSL**
```bash
vagrant up
```
**Inside WSL - After vagrant up finishes**
```bash
ansible-playbook setup_k3s.yml
```
## Linux
```bash
ansible-playbook deploy_infra.yml
```
```bash
ansible-playbook setup_k3s.yml
```

# Kubeconfig

Your kubeconfig file will be in ~/.kube/k3s.yaml to use it you can set the **KUBECONFIG** environment variable with this command

```bash
export KUBECONFIG="~/.kube/k3s.yaml"
```

Verify you have access to the cluster

```bash
kubectl get nodes
```

And you're all set

# Tech stack

<table>
    <tr>
        <th>Logo</th>
        <th>Name</th>
        <th>Description</th>
    </tr>
    <tr>
        <td><img width="32" src="https://icon.icepanel.io/Technology/svg/K3s.svg"></td>
        <td><a href="https://k3s.io">K3s</a></td>
        <td>Lightweight Kubernetes</td>
    </tr>
    <tr>
        <td><img width="32" src="https://static-00.iconduck.com/assets.00/file-type-ansible-icon-2048x2042-jf1amk4h.png"></td>
        <td><a href="https://www.ansible.com">Ansible</a></td>
        <td>Automate VM provisioning and configuration</td>
    </tr>
    <tr>
        <td><img width="32" src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Vagrant.png/150px-Vagrant.png"></td>
        <td><a href="https://www.vagrantup.com/">Vagrant</a></td>
        <td>Automate VM creation in Virtualbox</td>
    </tr>
    <tr>
        <td><img width="32" src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/Virtualbox_logo.png/121px-Virtualbox_logo.png"></td>
        <td><a href="https://www.virtualbox.org/">VirtualBox</a></td>
        <td>Virtualization</td>
    </tr>
    <tr>
        <td><img width="32" src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/35/Tux.svg/84px-Tux.svg.png"></td>
        <td><a href="https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux">WSL2</a></td>
        <td>Windows Subsystem for Linux </td>
    </tr>
    <tr>
        <td><img width="32" src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ab/Logo-ubuntu_cof-orange-hex.svg/2048px-Logo-ubuntu_cof-orange-hex.svg.png"></td>
        <td><a href="https://ubuntu.com/download/server">Ubuntu Server</a></td>
        <td>Base OS for VMs</td>
    </tr>

</table>