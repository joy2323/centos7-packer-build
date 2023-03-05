# packer-centos7-kvm-image
Packer is an open source tool for creating identical machine images for multiple platforms from a single source configuration called a template. It uses different plugins as builders, provisioners or post-processors.


## Pre-requisites
To run this project with success, you need a virtualization server and packer installed:

- Libvirt/KVM,

- Packer


### Libvirt and Packer Installation
**Install Livirt/KVM on your server:**

`if [ -f /etc/debian_version ]; then
apt-get update && apt-get -y upgrade
apt-get -y install qemu-kvm libvirt-dev virtinst virt-viewer libguestfs-tools virt-manager uuid-runtime curl linux-source libosinfo-bin
virsh net-start default
virsh net-autostart default
elif [ -f /etc/redhat-release ]; then
yum -y install epel-release
yum -y upgrade
yum -y group install "Virtualization Host"
yum -y install virt-manager libvirt virt-install qemu-kvm xauth dejavu-lgc-sans-fonts virt-top libguestfs-tools virt-viewer virt-manager curl
ln -s /usr/libexec/qemu-kvm /usr/bin/qemu-system-x86_64
fi`


**Install the Packer binary :**

`yum -y install wget unzip || apt update && apt -y install wget unzip
latest=$(curl -L -s https://releases.hashicorp.com/packer | grep 'packer_' | sed 's/^.*<.*\">packer_\(.*\)<\/a>/\1/' | head -1)
wget https://releases.hashicorp.com/packer/${latest}/packer_${latest}_linux_amd64.zip
unzip packer*.zip
chmod +x packer
mv packer /usr/local/bin/`

### Build with Packer

To build a CentOS 7 virtual machine image using Packer on a virtual server, you will need to follow these general steps:

- Connect to the virtual server via SSH as described.

- Install Packer on the virtual server by following the instructions provided in the Packer documentation.

- Create a new directory to hold the Packer configuration files and change into that directory:
    `mkdir centos7-packer
     cd centos7-packer`
- Create a new file named centos7-base.json in the packer-build directory with the following contents:
