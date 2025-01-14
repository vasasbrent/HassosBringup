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
  

## USB Ethernet Adapter Bridge Cannot Acquire DHCP Lease

Partially Resolved

* `systemctl restart networking.service` resolved issue, lease acquired.
* Would like to automate acquisition, odd that it didn't work.


## Domain Has Interface, but No Address

[Relevant Step](#set-up-networking-for-vm)

* Domain not set to use DHCP, which the adapter and bridge are set up with. [Link](https://stackoverflow.com/questions/73549741/virsh-domifaddr-domain-name-does-not-show-kvm-ips).
  * Mine is currently set to `<interface type='bridge'>`, unclear whether this is causing an issue.

