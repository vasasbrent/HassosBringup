# Bringup Steps

**Lots of missing steps**
Mostly following [this guide](https://community.home-assistant.io/t/install-home-assistant-os-with-kvm-on-ubuntu-headless-cli-only/254941).

## Set Up Networking for VM



# Issues

## USB Ethernet Adapter Not Showing

Unresolved

### Symptom(s)
1. Boot
1. Run `lsusb`

* adapter does not show up in list

### Attempted Solution(s)

#### Hotplug

1. Unplug and replug adapter

* device shows up
  * temporary solution

#### Supress Hotplug, See if Boot Brings Up

Per: https://forums.debian.net/viewtopic.php?t=157146#top
1. Suppressed `allow-hotplug` for adapter in `etc/network/interfaces`
2. Reboot

* device did not show up
* hotplug still worked, odd

#### Update Firmware

https://unix.stackexchange.com/questions/384403/debian-stretch-failed-to-load-firmware-rtl-nic-rtl8168g-3-fw-2#:~:text=apt%2Dget%20install%20firmware%2Drealtek
  

## USB Ethernet Adapter Bridge Cannot Acquire DHCP Lease

Partially Resolved

* `systemctl restart networking.service` resolved issue, lease acquired.
* Would like to automate acquisition, odd that it didn't work.


## Domain Has Interface, but No Address

[Relevant Step](#set-up-networking-for-vm)

Running `virsh domifaddr <domain-name>` does not return any IP addresses.

* Domain not set to use DHCP, which the adapter and bridge are set up with. [Link](https://stackoverflow.com/questions/73549741/virsh-domifaddr-domain-name-does-not-show-kvm-ips).
  * Mine is currently set to `<interface type='bridge'>`, unclear whether this is causing an issue.
  * Seems unlikely to be the issue. Searching for results with the interface type I'm using.
* [This feller](https://serverfault.com/questions/208019/no-ipv4-address-assigned-to-kvm-vm) seems more like what I'm dealing with.
  * Attempting [first response](https://serverfault.com/questions/208019/no-ipv4-address-assigned-to-kvm-vm#:~:text=This%20is%20most%20likely%20the%20solution.%20Alternatively%20add%20these%20lines%20to%20/etc/sysctl.conf%3A%20net.bridge.bridge%2Dnf%2Dcall%2Dip6tables%20%3D%200%20net.bridge.bridge%2Dnf%2Dcall%2Diptables%20%3D%200%20net.bridge.bridge%2Dnf%2Dcall%2Darptables%20%3D%200) to top solution. Top solution itself seems to be for another distro.
    * This did not resolve the symptom after reboot.
* Trying the top solution from [this](https://serverfault.com/questions/627238/kvm-libvirt-how-to-configure-static-guest-ip-addresses-on-the-virtualisation-ho). Seems like it might be what I'm dealing with.
  * jk, this is for nat or route net types, the search continues.
* Edited default network, getting tired, stopping for now.
 